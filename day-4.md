4.Gün  23.07.2018


**DNS** nasıl çalışır: 

  - Browser öncelikle kendi lokal cache’inde ilgili adres için IP’nin bulunup bulunmadığına bakar. 
  - İstenen bilgi bulunamazsa bilgisayarda tanımlı olan DNS sunucuya (bu sunucu genellikle internet sağlayıcınızın -ISP- DNS adresi     olur) recursive olarak istek atılır. 
  - İstenen bilgi burada da bulunamaz ise bir üst sunucuya istekte bulunur. 
  - İstenen cevap zincirdeki sunucularda bulunamazsa kaydı tutan asıl sunucuya kadar gidiler, cevap bulunur ve dönülür.

DNS isteğine verilen cevapta TTL (time-to-live) olarak bulunur. 

TTL süresi DNS kaydının sahibi tarafından belirlenir.

DNS kayıt tipleri: **A**, **AAA**, **NS**, **CNAME**, **SRV**, **TXT**, **MX**

**A** kaydı en çok kullanılan ve bilinen IPv4 adresi dönen kayıt sorgusudur.

**AAA** kaydı IPv6 adresi dönen kayıt sorgusudur.

**NS**: Network üzerinde bulunan ve kullanım da olan DNS Serverları tanımlar.

**CNAME** kaydı: Farklı domain'leri tek bir domain'de birleştirmek için kullanılır. 

Örnek: linux․org.tr ve www․linux.org.tr gibi iki farklı adresi CNAME ile tek linux.org․tr'de birleştirilebilir.

CNAME'i aynı zamanda farklı bir domain'e yönlendirme amacı ile de kullanılabilir. 

**SRV** kaydı sunucu tarafından sunulan bir servisin adres, protokol ve port bilgisini döner.

**TXT** kayıtları özel amaçlı kayıtlardır. Genellikle spam e-posta gönderimlerini engellemek için oluşturulmuş kurallardan biri olan “SPF” kayıtlarını tanımlamak için kullanılır.

**MX** kaydı: Alan adına ait mail adreslerinin çalıştığı mail sunucularını adresleyen bir DNS kaydıdır.

DNS kayıtlarını sorgulamak için nslookup veya dig adlı programlar kullanılabilir.

```
>>>nslookup
>>>server
>>>linux.org.tr
>>>nslookup linux.org.tr
```

**linux.org.tr**'nin DNS serverlarını listelemek için:
```
>>>dig NS linux.org.tr 
```

t=0 anı:

    TCP		 Açık		    Kapalı     Hiç cevap yoksa
    
    syn		 syn+ack	    rst	       firewall olabilir
    
    ack		 rst		    rst	       makine yok
    
    fin		 rst		    rst	       routing ve ya bağlantı problemi
    
    urg		 rst		    rst	       servis dışı kalma durumu
    
    rst		 X		     X		

    
    UDP		Açık		   Kapalı	 Hiç cevap yoksa
		        
                   cvp glrse	   icmp port	 açık olabilir, 
                     		   unreachable   firewall olabilir	  
		
Hostname: Makinaya verilen isim, kimlik bilgisi.

Domain: Bir grup bilgisayarın oluşturduğu ağa verilen isim, kimlik bilgisi.

**DHCP:**
  - Ağdaki cihazlara ip adresi, ağ maskesi, ağ geçidi ve dns adresleri gibi bilgileri otomatik olarak atamak için kullanılan servistir.
  - Bir ağda bulunan cihazlara tek tek gezip benzer ip parametrelerinin defalarca elle girilmesini engelleyerek zamandan tasarruf etmeye yarar. 
  - Bu sayede sistem yöneticisinin işini kolaylaştırır.
  - Broadcast yayınını UDP üzerinden yapar.
  - DHCP kira süresi ayarlanabilir, kira süresi tekrar yenilenebilir. 
  - Kira süresi bittikten sonra yenilenmesi durumunda aynı IP adresini atanabilir ve ya atanmayadabilir.
  
 Bir ağda iki DHCP sunucusu varsa ve bir istemci IP request ederse: Hangi DHCP sunucusu istemciden gelen requesti ilk ulaştırırsa, o DHCP'nin atamış olduğu IP istemciye verilmiş olur.

**Scapy** ile DNS paket oluşturma:
```
$ scapy
>>>ip = IP(dst=<"IP">, version=4)
>>>udp = UDP(sport=50,dport=53)
>>>dns = DNS(rd=1,qd=DNSQR(qname="linux.org.tr"))
>>>send(ip/udp/dns)
```


**Scapy** ile DHCP paket oluşturma:
```
$ scapy
>>> eth = Ether(dst="ff:ff:ff:ff:ff:ff",src=<"SRC_MAC_ADDR">)
>>> ip  = IP(src="0.0.0.0",dst="255.255.255.255")
>>> ud  = UDP(sport=68,dport=67)
>>> bootp = BOOTP(chaddr=<"SRC_MAC_ADDR">, xid=100)
>>> dhcp = DHCP(options = [ ("message-type","request"),("server_id",<IP>),("requested_addr",<"Requested_Addr">),"end"])
>>> paket=eth/ip/ud/bootp/dhcp
>>> sendp(paket,iface="eth0")
```

**OSINT:** 
  - Açık kaynak istihbaratı
  - Passive bilgi toplama (information gathering)
  - Seviye 1: Otomize araçlarla bilgi toplanır, ham veri gelir, sızma tespiti
  - Seviye 2: Kurum hakkında daha fazla bilgi gelir, bilginin anlamlandırılması işlenmesi
  - Seviye 3: Mil. Devletlerarası işlerde, askeri işlerde, ileri düzey bilgi toplama, red team(offansive)

Bilgi toplama; hedef sistemle doğrudan iletişime geçerek ve hedef sistemden bağımsız olmak üzere iki türdür. 

**1. Pasif Bilgi Toplama** : 
  - Pasif Bilgi Toplama Hedef sistem ile doğrudan iletişime geçilmez. 
  - Herhangi bir iz bırakmadan internetin imkanları kullanılarak yapılır.
  - 3rd party uygulamalar kullanılabilir.
  
**2. Aktif Bilgi Toplama** : 
  - Hedef ile iletişime geçilerek olabildiğince fazla ve işe yarayan bilgi edinilmeye çalışılır. 
  - DNS Protokolü kullanarak Bilgi Toplama DNS Protokolü internetin temel yapıtaşıdır. 
  - Genel olarak www hizmetlerinde ve e-posta servislerinde kritik rol oynar. 
  - Düzgün yapılandırılmamış bir DNS sunucu dışarıya oldukça fazla bilgi verebilir.

White box: Temel seviye test.

Gray box: İçerde bağlantı sağlayabileceğimiz bir ortam, farklı yetkiler verilerek yapılan test, verilen zararlar analiz edilir.

Black box: Sistem, kurum hakkında hiçbir bilgi verilmez, bilgiler en baştan toplanır, ileri seviye test.

whois sorgusundan elde edilebilecek bilgiler; 
  - İlgili birimde çalışanların telefon numaraları, email adresleri
  - Şirketin e-posta adresi kullanım profili(ad.soyad[at]sirket.com gibi)
  - IP Adresleri ve Domain Adları Hakkında Bilgi Edinme
  
**robtex.com** bilinen en iyi pasif bilgi toplama sitelerinden biridir. Robtex üzerinden detaylı Whois bilgisi ve dns kayıtları görülebilir. 
Bir ip adresi üzerinde çalışan web sayfalarının listesini verebilmektedir.
