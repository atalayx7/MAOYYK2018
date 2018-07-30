##  9.Gün 29.07.2018

- Syn Cookie: Sunucu ile istemciler arasında bir makine olur, istek yapan istemcinin gerçek olduğunu anlamak için TCP three way handshake tamamlanana kadar TCP sunucuya SYN paket göndermez. TCP istemcinin isteği tamamlandıktan sonra istek sunucuya replicate edilir. Bu şekilde sunucunun state tablosu doldurulmamış olur.

- DNS default'ta UDP ile 53 portunda çalışır. UDP'de herhangi bir kontrol mekanizması olmadığı için spoofing yaparak paket yollanabilir. 

- DNS sunucularına hedefi taklit ederek büyük boyutlarda istekler yollanır. DNS sunucuları, hedefe bu isteklerin cevaplarını yollayarak hedefi servis dışı bırakır.

- DNS sunucuları recursive ve ya authoritative çalışır. Recursive DNS sunucuları her soruya cevap verir, authoritative DNS sunucuları ise her soruya cevap vermez.

- DNS zehirlenmesi: DNS sunucusunun ön bellek veritabanına veri eklenerek ve ya oradaki verileri değiştirilerek ad sunucunun yanlış IP adresleri dönmesine ve trafiğin başka bir bilgisayara yönlendirilmesine neden olan bir saldırıdır.
  - dig @8.8.8.8 google.com any

IP adresi bilmeden recursive'li sorgulamadan:
```
$~ dig ibu.edu.tr +norecurse

; <<>> DiG 9.11.3-1-Debian <<>> ibu.edu.tr +norecurse
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41663
;; flags: qr ra; QUERY: 1, ANSWER: 1, AUTHORITY: 13, ADDITIONAL: 11

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; MBZ: 0x0005, udp: 4096
;; QUESTION SECTION:
;ibu.edu.tr.			IN	A

;; ANSWER SECTION:
ibu.edu.tr.		5	IN	A	194.27.34.124

;; AUTHORITY SECTION:
.			5	IN	NS	g.root-servers.net.
.			5	IN	NS	b.root-servers.net.
.			5	IN	NS	e.root-servers.net.
.			5	IN	NS	a.root-servers.net.
.			5	IN	NS	i.root-servers.net.
.			5	IN	NS	d.root-servers.net.
.			5	IN	NS	k.root-servers.net.
.			5	IN	NS	f.root-servers.net.
.			5	IN	NS	h.root-servers.net.
.			5	IN	NS	j.root-servers.net.
.			5	IN	NS	c.root-servers.net.
.			5	IN	NS	m.root-servers.net.
.			5	IN	NS	l.root-servers.net.

;; ADDITIONAL SECTION:
h.root-servers.net.	5	IN	A	198.97.190.53
l.root-servers.net.	5	IN	A	199.7.83.42
j.root-servers.net.	5	IN	A	192.58.128.30
m.root-servers.net.	5	IN	A	202.12.27.33
g.root-servers.net.	5	IN	A	192.112.36.4
f.root-servers.net.	5	IN	A	192.5.5.241
f.root-servers.net.	5	IN	AAAA	2001:500:2f::f
a.root-servers.net.	5	IN	A	198.41.0.4
a.root-servers.net.	5	IN	AAAA	2001:503:ba3e::2:30
d.root-servers.net.	5	IN	AAAA	2001:500:2d::d

;; Query time: 11 msec
;; SERVER: 192.168.209.2#53(192.168.209.2)
;; WHEN: Mon Jul 29 11:13:34 +03 2018
;; MSG SIZE  rcvd: 462
```

IP adresini recursive'li sorgularsak:
```
$~ dig ibu.edu.tr           

; <<>> DiG 9.11.3-1-Debian <<>> ibu.edu.tr
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 22369
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 13, ADDITIONAL: 8

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; MBZ: 0x0005, udp: 4096
;; QUESTION SECTION:
;ibu.edu.tr.			IN	A

;; ANSWER SECTION:
ibu.edu.tr.		5	IN	A	194.27.34.124

;; AUTHORITY SECTION:
.			5	IN	NS	a.root-servers.net.
.			5	IN	NS	e.root-servers.net.
.			5	IN	NS	b.root-servers.net.
.			5	IN	NS	j.root-servers.net.
.			5	IN	NS	l.root-servers.net.
.			5	IN	NS	h.root-servers.net.
.			5	IN	NS	f.root-servers.net.
.			5	IN	NS	c.root-servers.net.
.			5	IN	NS	i.root-servers.net.
.			5	IN	NS	g.root-servers.net.
.			5	IN	NS	d.root-servers.net.
.			5	IN	NS	k.root-servers.net.
.			5	IN	NS	m.root-servers.net.

;; ADDITIONAL SECTION:
g.root-servers.net.	5	IN	A	192.112.36.4
i.root-servers.net.	5	IN	A	192.36.148.17
i.root-servers.net.	5	IN	AAAA	2001:7fe::53
k.root-servers.net.	5	IN	A	193.0.14.129
a.root-servers.net.	5	IN	A	198.41.0.4
d.root-servers.net.	5	IN	A	199.7.91.13
e.root-servers.net.	5	IN	A	192.203.230.10

;; Query time: 85 msec
;; SERVER: 192.168.209.2#53(192.168.209.2)
;; WHEN: Mon Jul 29 11:23:53 +03 2018
;; MSG SIZE  rcvd: 390

```

Recursive'li sorgulamadan sonra tekrardan recursive olmadan sorgularsak:
```
$~ dig ibu.edu.tr +norecurse

; <<>> DiG 9.11.3-1-Debian <<>> ibu.edu.tr +norecurse
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 17617
;; flags: qr ra; QUERY: 1, ANSWER: 1, AUTHORITY: 13, ADDITIONAL: 11

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; MBZ: 0x0005, udp: 4096
;; QUESTION SECTION:
;ibu.edu.tr.			IN	A

;; ANSWER SECTION:
ibu.edu.tr.		5	IN	A	194.27.34.124

;; AUTHORITY SECTION:
.			5	IN	NS	i.root-servers.net.
.			5	IN	NS	g.root-servers.net.
.			5	IN	NS	a.root-servers.net.
.			5	IN	NS	l.root-servers.net.
.			5	IN	NS	b.root-servers.net.
.			5	IN	NS	d.root-servers.net.
.			5	IN	NS	h.root-servers.net.
.			5	IN	NS	e.root-servers.net.
.			5	IN	NS	k.root-servers.net.
.			5	IN	NS	f.root-servers.net.
.			5	IN	NS	m.root-servers.net.
.			5	IN	NS	c.root-servers.net.
.			5	IN	NS	j.root-servers.net.

;; ADDITIONAL SECTION:
h.root-servers.net.	5	IN	A	198.97.190.53
l.root-servers.net.	5	IN	A	199.7.83.42
j.root-servers.net.	5	IN	A	192.58.128.30
m.root-servers.net.	5	IN	A	202.12.27.33
g.root-servers.net.	5	IN	A	192.112.36.4
f.root-servers.net.	5	IN	A	192.5.5.241
f.root-servers.net.	5	IN	AAAA	2001:500:2f::f
a.root-servers.net.	5	IN	A	198.41.0.4
a.root-servers.net.	5	IN	AAAA	2001:503:ba3e::2:30
d.root-servers.net.	5	IN	AAAA	2001:500:2d::d

;; Query time: 16 msec
;; SERVER: 192.168.209.2#53(192.168.209.2)
;; WHEN: Mon Jul 29 11:27:50 +03 2018
;; MSG SIZE  rcvd: 462

```

nmap' te -n parametresi ters DNS sorgularının olmamasını sağlar, sorgulama işlemini hızlandırır.
  - nmap -n -Pn -sV -v --open <target>
  
  
