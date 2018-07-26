##  6.Gün 26.07.2018

##  Aktif Bilgi Toplama

**Host Discovery**
  - arp-scan -I eth0 --localnet
  - nmap -sP x.y.z.0/24 -vv
  - netdiscover -r <x.y.z.0/24>

**Network Discovery**
- nmap = İsviçre Çakısı
- nmap -sP 192.168.42.0/24 #ping sweep
- **ps aux | grep** nmap arkaplan processini gösterir.
- SYN proxy: Tüm SYN'lere SYN-ACK cevabı gönderiyor, böylece 60000 port açık olarak gözüküyor.

**nmap parametreleri**
   -  **-sC** = Script kullanımı parametresi
   -  **-sS** = Syn paketi parametresi
   -  **-sA** = Ack paketi parametresi  
   -  **-sT** = TCP paketi parametresi  - IP loglanır.
   -  **-sF** = FIN paketi parametresi 
   -  **-sU** = UDP paketi parametresi
   -  **-sV** = Port versiyon parametresi
   -  **-v** = Detayları ekranda görüntüler (az)
   -  **-vv**  = Detayları ekranda görüntüler (çok)
   -  **-O**  = Hedef sistemin işletim sistemi tespit etmeye çalışır.
   -  **f** = paketleri fragment olarak gönderir böylece güvenlik sistemini atlatmak daha olası.
   -  **system-dns** = İşletim sisteminin DNS servisini kullanır.
   -  **--top-ports** = En sık kullanulan portları içeren tarama parametresi.

**Firewall Bypass**
- nmap -f -f
- nmap --script=firewall-bypass
- nmap -D RND:5 #5 Fake random paketle beraber asıl paketi enjekte etmek için
- nmap -D 1.1.1.1
- nmap --spoof-mac=IBM <x.y.z.0/24>

**Banner Grabbing**
  - nc = Bir diğer İsviçre Çakısı
  - nc 1.1.1.1 80
  - curl
  - telnet 1.1.1.1 80

**Agressive Scan**
  - nmap -A # Aggressive
  - nmap -T (0-5)

**DNS Discovery**
  - nslookup
  - dig ns <IP>
  - dig -x <IP>
  - fierce --dns
  - dnsrecon -d

**Web Application Discovery**
  - Wapplyzer
  - WP
  - Drupal
  - Joomla
  - whatweb <domain> -v
  - builtwith.com
  - wafw00f #Paketleri analiz edip, waf tespiti yapar.

**Fuzzing**
  - dirb
  - dirbuster
  - wfuzz
  - nikto
  

-Hedef makinenin ayakta olup olmadığını anlamak ICMP ve ya ARP paketleri gönderilir.

-Firewall ICMP paketlerini düşürebilir bu yüzden ARP paketi göndermek iyi.

-nmap <IP> --top-ports 1000    -En sık kullanılan 1000 port taraması

-ls /usr/share/nmap/scripts/ #nmap için scriptler
