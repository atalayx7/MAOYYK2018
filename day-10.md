##  10.Gün 30.07.2018
## EXPLOIT AŞAMASI

- Exploit: Zafiyeti sömürme işlemi.
  - Exploit Türleri
    - Remote
    - Local
    - DoS
    - Zero day
- Metasploit Framework:
  - Ruby ile geliştirilen framework. 
  - Çeşitli exploit ve payload'ların bulunduğu,
  
- Metasploit Framework içerisinde bulunan bölümler:
  - Auxiliary: Yardımcı toollar bulundurur.
  - Exploit: Zafiyeti sömürme işlemi
  - Payload: Exploit edilen sisteme gönderilen kod.
  - Post-exploitation:  Hedef sisteme erişim sağlandıktan ve yetkiler yükseltildikten (root) sonra ki başlayan bir süreçtir. Erişimin kalıcı hale getirilmesi ve sürdürülmesi amaçlanır.
  - Encoders: Payload olarak gönderilen kodların anti virüs programlarına yakalanmaması için yapılan kriptolama işleminde kullanılan araçtır. Payload kodlarının imzalarını değiştiren bölüm.

- Staged payload: windows/meterpreter/reverse_tcp
- Stageless payload:  windows/meterpreter_reverse_tcp
 
Meterpreter:  
  - Meta-Interpreter
  - Komut satırı programıdır. 
  - Dll enjeksiyonu aracılığıyla ve doğrudan RAM hafızasında çalışır. 
  - Hard diskte herhangi bir log bırakmaz. 
  - cmd.exe ile yapılamayan üst düzey işlemleri (ekran alma, port yönlendirmeyi, port açma) yapabilmemizi sağlayan üst düzey bir payload'dır.

- Payload, eğer bağlantı kuran bir payload ise bind veya reverse olabilir.

- Shellcode: Makine dilinde hedeflediğimiz processin hafıza alanına yazılacak ve istediğimiz işlemi gerçekleştirecek koddur.

- Windows'ta en yüksek yetkili kullanıcı: nt authority/system

- Bir işletim sisteminde iki şekilde hak yükseltilir:
  - Yanlış yapılandırılmış bir eksiklikliği zafiyete çevirerek.
  - İşletim sistemininin kernel'inde bulunan bir zafiyeti sömürerek.

Makine işletim sistemi bilgisi için iki farklı komut:
  - cat /etc/issue
  - cat /etc/lsb-release 
