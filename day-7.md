##  7.Gün 27.07.2018

## Zafiyet Tespiti

**Kavramlar**
- Sömürü/Exploit
  - Remote (Uzaktan erişim)
  - Local  (Doğrudan erişim)
  - DoS (Denial-of-Service attack)
  - Sıfırıncı gün (0 day)
- Payload
  - Reverse
  - Bind
- Post Exploitaion

**Otomatize**
  - Nessus
    - https://www.tenable.com/products/nessus/activation-code
    - https://www.tenable.com/downloads/nessus
  - OpenVAS
    - https://www.kali.org/category/penetration-testing/
    - https://www.kali.org/penetration-testing/openvas-vulnerability-scanning/
  - Core Impact
  
- Version/Patch
  - exploit-db.com
  - cvedetails.com
  - 0day.today
  - github.com

- Nmap

- Nikto
 
 **Reverse TCP Connection**
 
Ele geçirilen sunucu; netcat, yada python, perl vb programlama dilleri ile yazılmış scriptler ile saldırganın bilgisayarının dinlemede olduğu bir portuna bağlantı talebi gerçekleştirmesine dayanmaktadır.

**Bind Shell**

Ele geçirilen sunucu; netcat, yada python, perl vb programlama dilleri ile yazılmış scriptler ile saldırganın seçtiği bir port dinleme alınır. Bu işlem gerçekleştirildikten sonra saldırgan hedef sunucunun dinlemede olan portuna bağlantı talebi göndermesine dayanır.

Tahmin edebileceğiniz gibi Bind Shell saldırıları NAT arkasındaki sunucular ile problem teşkil etmektedir. Bu nedenle genellikle Post Exploitation denen saldırıların haricinde Reverse Shell tercih edilir. 

Referans: https://www.mehmetince.net/python-ile-pty-reversebind-connection/

**Zaafiyet İstismarı:**
- Kaynak Kod
- Uygulama Çatıları
  - Metasploit-Framework
    - Auxiliary
    - Exploit
    - Meterpreter
- Msfvenom
