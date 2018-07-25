**2.Gün  21.07.2018**

Sızma Testleri:

- Güvenlik testleri
- Web uygulama testleri
- Mobil test
- Kablosuz ağ testleri
- Cloud (bulut) testleri

## OSI Modeli:

**1. Application layer** (Uygulama katmanı): Firefox, FTP, SMTP, HTTP

**2. Presentation layer** (Sunum Katmanı): Veriyi uygun hale getiren katmandır, format dönüşümü bu katmanda yapılır. 
  
  Örnek: HTTP (ASCII/text ) Binary datayı ASCII formatına çevirme

Base64 veya SSL (şifreleme yöntemi) format değiştirmek için kullanılan yöntem. 
- fotograf (PNG) --> base64 --> text 
- text --> base64 --> fotograf (PNG) 

**3. Session layer** (Oturum katmanı): Oturumu yönetme, uygulama katmanında bir işlem yapıcaksın ama başka bir servise de ihtiyacın var, başka servislerle ve uygulamalarla konuşarak işlem gerçekleştireceğimiz oturumları kendi içerisinde barındırıyor. Başka bir deyişle; servislerin birbirleriyle iletişimini sağlayan katmandır.
  
  Örnek:  SSH,RDP,SMB

**4. Transportation layer** (Taşıma katmanı): TCP ve UDP, iletişimi sağlayan, mesajları gönderen katman.

  - UDP: Hızlıdır, streaming işlerinde kullanılır. Bir veri ya da mesaj gönderdiğinizde, iletildiğinden haberiniz olmaz. Mesaj iletilirken bozulma veya kaybolma yaşanabilir.
  - TCP: Bağlantı oryantasyonludur yani bir dosya ya da mesajın iletilmesi için bağlantı olması gerekir. Eğer bağlantı koparsa, sunucu kayıp parçaları talep eder. Mesaj iletilirken herhangi bir bozulma yaşanmaz.

**5. Network layer** (Ağ katmanı): IPv4, IPv6  adreslerinin oluşturulduğu katman, görevi adresleme.
  
  - Private IP Blocks: 
    - 192.168.0.0/16
	 - 10.0.0.0/8
	 - 172.16.0.0/16
    - 169.254.0.0/16
    - 100.100.0.0/16
	
**6. Data link layer** (Veri bağlantısı katmanı): Ethernet ağı varsa MAC’ten (00:00:00:00:00:00-FF:FF:FF:FF:FF:FF) ve ARP (IP’den MAC’e dönüşüm) ve ya RARP’den (=MAC’ten IP’ye dönüşüm) bahsedilebilir. Fiziki anlamda adresleme yapabilir. 

ARP: 6 octet 48 bitlik 

MAC adresinin ilk 3 okteti: Üreteden firmayı temsil eder.

Son üç oktet: Ağ karı (NIC) için unique bir tanıtıcı numarasıdır.

MAC adresi: Fiziksel Adress

Broadcast yapmak için MAC adresinin FF:FF:FF:FF:FF:FF olarak tanımlanması gerekir.

ARP (=Address resolution protocol): Bu IP adresinin MAC adresi nedir?

ARP:   IP --> MAC

RARP: MAC --> IP

**7. Physical layer** (Fiziksel katman): Bit stream (0 ve 1) dediğimiz veri iletimi bu katmanda sağlanır.

Fiber, Bakır tel gibi aktarım yöntemleri kullanılır.

OSI katmanında protocol değişiklikleri diğer katmanları etkilemez.

OSI’de her bir katmanda sıklıkla kullandığımız çeşitli protokoller vardır.

Şahsi uygulamalar ve protokoller yazılabilir. Örneğin; şifreleme protokolleri.

ARP: İsim var ama fiziki lokasyon bilinmiyor ve iletişim kurman gerekiyor, isim söylenir ve şahıs fiziki lokasyonunu belirtir (Broadcasting).

RARP: Yerini biliyorsun ama ismini bilmiyorsun. Lokasyonunu işaret ediyorsun.

DHCP(Dynamic Host Configuration Protocol): Sistemde ki bilgisayarlara dinamik olarak ip atar.

Peki ulaşmak istediğimiz şahıs orda değilse ve onun yerinde ise art niyetli biri varsa? Bu tarz senaryolar için güvenlik mekanizması olmadığı için ARP’ta güvenlik sıkıntıları mevcut.

IPv4 nesneyi adreslemek, v4= 4.versiyon, görevi makineyi adreslemek ve bu adresleme üzerinden ağ tanımlarını yapabilmek.

TCP ve UDP : Veri iletilirken kullanılacak yapı.

TCP’de oturum kontrolü var, UDP’de yok.

Otomatik ip adresi ataması için: **dhclient -v eth0**

ARP tablosu sorgulama: **arp -a**  

**ping -n 1 \<IP>** : 1 adet ICMP echo request paketi gönderir.

**arp -d \<IP>**  : ilgili kaydı siler

Wireshark’ta **ip.addr == \<IP>**  filtresi ilgili IP’de ki trafiği görüntüler.

ARP kayıtlarının türü dinamiktir, belli bir süre sonra ARP kaydı silenebilir.

ARP’ı kullanarak MAC adresi ve IP bilmeden keşif işlemi? Evet yapabilirsin, IP’yi keşfet ve bu ağ içerisinde ki bütün makinelere ARP paketi gönderirsek karşı makinalar otomatik olarak cevap verecektir.

IP’yi biliyorsun ve MAC adresi sorgulama için : **arping  -I eth0 \<IP>**

Bir ağın içerisinde miyim? ifconfig -> Interface **up** ve **running** ise sinyal vardır.

Interface down ise: **up** kaybolur.

Kablo takılı değil ise: **running** kaybolur.

**tcpdump -i eth0 -nnv**  : Ağı dinler, eğer bu ağ içerisinde makineler var ve iletişim halindeler ise trafiği izleyebilir.

Localhost: 127.0.0.1

Broadcast (=Yayın adresi): 255.255.255.255

IPv4 32 bitlik adresleme yapabilir

IPv4 ile (2^32) 4294967296 adres üretilebilir. Kolay ifade edilebilmesi açısından 32 bit 4’erli gruplar halinde 0-255 arasında ifade edilir.

Subnet: Alt ağ

Subnetting (Alt Ağlara Bölme)
  - Network trafiğini azaltır.
  - Network performansını optimize eder.
  - Networkün yönetimini kolaylaştırır

Sınıflara göre varsayılan subnet mask bilgisi ise aşağıdadır:
  - A sınıfı : 255.0.0.0
  - B sınıfı : 255.255.0.0
  - C sınıfı : 255.255.255.0

IP bloklarının yönetimini, rezervasyon işlemlerini IANA (=Internet Assigned Numbers Authority) adlı kurum yapar.

NAT (=Network Address Translation): Internet ortamında sadece belirli IP’ler bulunsun, kişiler veya organizasyonlar kendi iç ağlarında kullanabileceği bir ağ olsun. 

Bu ağın kullanılabilmesi için internet ile alt ağlar arasında adres dönüşümü gerçekleştirilmelidir.

10.0.0.0/8   A class adres: Yaklaşık 16 milyar, 2^(32-8), IP adreslenebilir.

172.16.0.0/12  B class adres: Yaklaşık 1 milyar,  2^(32-12), IP adreslenebilir. 

192.168.0.0/16: Yaklaşık 65 bin,  2^(32-16), IP adreslenebilir.

127.0.0.0/8:  loopback, localhost, makine içerisindeki local ağ.

224.0.0.0/4 D class: Amaç multicasting, public ortamda kuruma, şahsa ve ya bir şirkete atanması söz konusu değil.

Unicast: 1 -> 1 iletişim

Multicast: 1 -> n iletişim 

Broadcast: Herkese yaptığımız yayın

240.0.0.0/4 E class: Bilimsel testler için reserve edilmiş ip bloğu.

RFC 1918 IP adresleri 10.0.0.0/8, 172.16.0.0/12, 169.254.0.0/16, 192.168.0.0/16 olarak belirtilmiştir. Bu adresler İnternet’te bulunmamaktadır ve İnternet’e açık her yönlendirici tarafından düşürülmesi gerekmektedir.

APIPA (Automatic Private IP Addressing): Makinenin DHCP sunucusundan response, IP adresi alamadığı taktirde işletim sistemi tarafından otomatik olarak atanana IP adresidir.
  - 169.254.0.0/16 networkte ve 255.255.0.0 subnetinde bir ip adresi alır. 
  - Makinenin APIPA’dan IP alabilmesi için mutlaka network adaptörünün açık ve çalışıyor olması gerekmektedir.
  - Linux işletim sistemlerinde APIPA’ya otomatik düşme yok ama Windows’ta var.

Protocol nedir? Protokoller bir iletişimin kurallarıdır. Bir network’teki iletişim kuralları protokoller tarafından düzenlenir.

ICMP (=Internet Control Message Protocol: TCP/IP protokol yapısında 3. Katmanda çalışan, ağın sağlıklı bir şekilde çalıştığı, ulaşılabilirliği, hız testi veya kontrol amaçlı kullanılır.

IP HEADER

  - Destination IP: Hedef IP
  
  - Source IP: Kaynak ip
  
  - Protocol: Alıcının protokol
  
  - Version: Kullanılan IP versiyonunu belirtir - IPv4-IPv6

  - Length: Paket uzunluğu

  - Type of Service: Servis tipini belirtir, router buna göre öncelik ataması yapar

  - Total Length: Paketin toplam uzunluğu

  - Identifier: Yeniden düzenleme ve hata raporlama için gereklidir.

  - Flag: Paketin parçalanıp parçalanmayacağı bilgisi

  - Fragmented Offset: Parçalanmış paketlerin sıra numarası

  - Time to Live: Paketin yaşam süresi, ne kadar süre boyunca ağ üzerinde iletileceğini belirler

  - Header Checksum: İletim sırasında herhangi bir hatanın olup olmadığını belirlemek için kullanılır.

Switch’in görevi: Yönlendirme yok, iletim var, paketi tutmaz direk olarak gönderir.

FTP (=File Transfer Protocol): Dosya Transfer Protokolü’dür. Bilgisayar dosyalarının bir bilgisayar ağı üzerindeki bir istemci ve sunucu arasında aktarılması için kullanılan standart bir ağ protokolüdür.

Port: Dış dünyaya açılan sanal kapılar.

LAN: Local area network / yerel ağ

ICMP: İnternette herhangi bir sorun sıkıntı var mı?

Three way handshake : Oturumun başlaması için gerçekleştirilen ritual.

Firewall (=Güvenlik Duvarı) çeşitli kuralları olan bir ağ güvenlik sistemidir, bir yazılımdır, gelen ve giden ağ trafiğini kontrol eder.

Her firewall güvenli mi? Bunun araştırması pentest değil security research çalışmasıdır.


**Three Way Handshake**
      

      SYN------>
      
      <------ SYN-ACK
      
      ACK------>
      
      .
      
      .
      
      .
      
      FIN------>
      
      <------FIN+ACK
      
      ACK------>


Uygulama katmanında (Application layer) taşınan bilgiye Data denir.

Taşıma katmanından(Transportation layer) ağ katmanına (Network layer) gönderilern veri:
  - TCP ile gönderiliyorsa Segment denir.
  - UDP ile gönderiliyorsa Datagram denir. 

Internet katmanındaki (Network Layer) bilgiye Packet denir. 

Veri bağlantısı katmanındaki (Data link layer) bilgiye Frame denir. 

Fiziksel katmandaki (Physical Layer) bilgiye BitStream denir.

Scapy çeşitli network paketlerini oluşturmak için kullanılan bir pakettir.

```
>>> scapy

>>> icmpbaslik = ICMP(type=14,code=0)

>>> ipbaslik = IP(src=<"Source IP">,dst=<"Destination IP">)

>>> paket = ipbaslik/icmpbaslik

>>> send(paket) 

#Wireshark uygulaması gönderilen paketin yanıtını inceleyebiliriz.

.

Sent 1 packets.

```

