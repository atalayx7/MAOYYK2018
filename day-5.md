##  **5.Gün 24.07.2018**

##  Pasif Bilgi Toplama - OSINT (Açık Kaynak İstihbaratı)

Subdomain tespiti için kullanılabilecek komutlar:
  - dig -x \<IP>
  - nslookup \<IP>
  - fierce -dns ankara.edu.tr
  - theharvester -d ankara.edu.tr -b all
  - dnsmap ankara.edu.tr
  
Virtualhost'ların tespiti için kullanılabilecek komut:
  - bing.com'dan IP:\<IP Addres> şeklinde arama yaptığımızda virtualhost'lara ulaşılabilir

**- E-mail tespiti için:**
  - theharvester -d ankara.edu.tr -b bing

https://www.netcraft.com : Hedefin sistemin işletim sistemini öğrenilebilir.

https://www.shodan.io : Bilgi toplamak için geliştirilmiş bir arama motoru. 
  - Parametreler: hostname:ankara.edu.tr, country:tr

**- FOCA** : Metadata analizleri ile bir çok bilgi elde edilebilir.

**- Google dorkları:**
  - exploit-db.com/google-hacking-database/
  - site:*.ankara.edu.tr
  - inurl:login site:*.ankara.edu.tr (giriş panellerine yönelik)
  
https://www.alexa.com : Domain'ler hakkında istatiksel bilgiler tutan bir servis.

http://archive.org : 1996 yılından günümüze kadar açılan bütün web sitelerin indekslerine -hâlihazırda siteler silinmiş bile olsa- ulaşmanız mümkün.

https://pastebin.com : Dump'larınpaylaşıldığı bir site.
    - site:pastebin.com intext:"password"

**- Dump:** Kötü niyetli kişiler tarafından bir database'in patlatılarak bilgilerin internette herkese açık olarak yayınlanması.

https://www.tineye.com : Görselle arama yapılabilek bir site.

https://www.wappalyzer.com : İçerik yönetim sistemlerini, e-ticaret platformlarını, web frameworklerini, sunucu yazılımlarını, analiz araçlarını tespit eden bir site.

https://macvendors.com : Cihazın MAC adresini girerek üretici firmasını tespit eden bir site.

https://haveibeenpwned.com : Girilen E-mail adresinin veri güvenliğini ihlal etmiş olup olmadığını kontrol eden bir site.

https://dnsdumpster.com : DNS keşif, araştırma, DNS kayıtlarını bulma ve arama.
