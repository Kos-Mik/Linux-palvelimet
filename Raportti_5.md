# TLS Sertifikaatit

## Johdanto 


Osoitteet ja muut yksilöivät tiedot ovat osittain tietoturvasyistä obfuskoitu.

## DNS

Asennettu **dig**-työkalu ohjeiden mukaisesti virtuaalikoneelle ja testataan sillä DNS-asetukset:

<p align="center">
<img width="646" height="372" alt="image" src="https://github.com/user-attachments/assets/42099eed-c49c-4ad9-a4a9-24909364f1e8" />
  <br>
  <em>Kuva 1. Julkinen IP-osoite näkyy.</em>
</p>
<br>
<br>

Kun yritin **tcpdump**in avulla tutkia DNS-liikennettä komennolla ```sudo tcpdump -i eth0 port 53 -n -v```, en saanutkaan tulokseksi mitään.

<p align="center">
<img width="652" height="132" alt="image" src="https://github.com/user-attachments/assets/3c1d804e-0ca0-448a-a3a6-c1ba292d8779" />
  <br>
  <em>Kuva 2. Ei niin mitään.</em>
</p>
<br>
<br>

Syy tähän on se, että dig käytti paikallista resolveria (127.0.0.53), joten DNS-kysely ei lähtenyt ulkoiseen verkkoon lainkaan. Tästä syystä tcpdump ei havainnut liikennettä eth0-liitännällä. Kun taas suoritin komennon 
```dig tls-testXXX.linuxkurssi.xyz @8.8.8.8``` eli tein DNS-kyselyn suoraan Googlen DNS-palvelimelle, tcpdump havaitsi DNS-liikenteen: 

<p align="center">
<img width="652" height="218" alt="image" src="https://github.com/user-attachments/assets/38afb7a7-e1f7-471b-8fdb-816882f50997" />
  <br>
  <em>Kuva 3. DNS-liikennettä havaittu!</em>
</p>
<br>
<br>

Tämä johtuu siitä, että kysely lähetettiin nyt ulkoiseen verkkoon DNS-palvelimelle 8.8.8.8 sen sijaan, että se olisi käsitelty paikallisesti resolverin (127.0.0.53) kautta, kuten alun perin tein.


## Name-Based VirtualHost

Nyt pitää luoda etäpalvelimelle nimipohjainen virtuaalipalvelin. Aloitetaan ensin luomalla **nano**n avulla viime tehtävässä luotuun hakemistoon index.html-sivu komennolla ```nano /home/linuxuser/public-sites/index.html```, laittamalla sisällöksi **This is my public web server** ja tallentamalla se. 

Luodaan vielä ylimääräiset tekstitiedostot sekä linuxuser-tunnuksilla että edituser-tunnuksilla:

**linuxuser:**
```bash
echo "Luotu linuxuserilla" > ~/public-sites/linuxuser.txt
```
**edituser:**
```bash
echo "Luotu edituserilla" > /home/linuxuser/public-sites/edituser.txt
```

Tämän jälkeen avattu ne selaimella:

<p align="center">
<img width="606" height="149" alt="image" src="https://github.com/user-attachments/assets/6f343445-f120-41eb-9642-eddfa9582378" />
<img width="606" height="149" alt="image" src="https://github.com/user-attachments/assets/eed589a6-1026-4f3c-92a3-9429c6c5050e" />
<img width="606" height="149" alt="image" src="https://github.com/user-attachments/assets/9698afc8-134a-4e1f-8e29-2bb0fe1af5d7" />
  <br>
  <em>Kuvat 4, 5 ja 6. Sivustot</em>
</p>
<br>
<br>

## TLS Certificate

Asennettu certbot-työkalu komennolla ```sudo apt install certbot python3-certbot-apache``` ja sen jälkeen luodaan TLS-sertifikaatti omalle sivustolle:

```bash
sudo certbot --apache -d tls-testXXX.linuxkurssi.xyz,www.tls-testXXX.linuxkurssi.xyz
```
Kun sertifikaatti on valmis, avataan selaimella sivusto uudelleen ja https-suojaus on nyt päällä:

<p align="center">
<img width="678" height="271" alt="image" src="https://github.com/user-attachments/assets/eb2dab3c-9c64-4cb1-b48c-a36e15efef98" />
  <br>
  <em>Kuva 7. Sertifikaatti asennettu onnistuneesti.</em>
</p>
<br>
<br>

Tästä huolimatta **crt.sh**-sivusto ei havainnut sertifikaattia vaan antoi vain ilmoituksen "none found". Kuitenkin curl-tulosteesta ja sertifikaatin uusinnan dry-runista voi päätellä, että sertifikaatti on asentunut täysin onnistuneesti ja uusiutuukin oikein. Voi olla, että crt.sh-sivustolla vain kestää jonkin aikaa ennen kuin se rekisteröi vastikään asennetun sertifikaatin:

<p align="center">
<img width="576" height="323" alt="image" src="https://github.com/user-attachments/assets/ea4e8863-97ee-4a93-acd6-9c5841821847" />
<img width="632" height="177" alt="image" src="https://github.com/user-attachments/assets/9e1a8684-5cab-4b3f-a9ab-7913ff8f2fa0" />
<img width="759" height="237" alt="image" src="https://github.com/user-attachments/assets/f4a03395-0bdc-4cc3-b9d3-9f867c6d745b" />

  <br>
  <em>Kuvat 8, 9 ja 10. Tilastollisesti kaksi positiivista tulosta kolmesta ei ole huono.</em>
</p>
<br>
<br>

## Monitoring – curl in verbose mode

Kun https-yhteyttä tarkasteltiin komennolla ```curl -v https://tls-test0xx.linuxkurssi.xyz```, tulosteessa näkyi TLS 1.3 -kättely (TLS handshake), palvelimen sertifikaatti, sertifikaatin myöntäjä (Let's Encrypt) sekä se, että sertifikaatin tarkistus onnistui. Tämä sai ainakin minut vakuuttuneeksi siitä, että sertifikaatti on asentunut onnistuneesti, vaikka crt.sh ei sitä näyttänytkään. 

Lisäksi näkyivät HTTP-otsakkeet ja palvelimen palauttama sisältö. Vaikka yhteyden muodostuminen ja sertifikaattitiedot ovat näkyvissä, varsinainen liikenne kulkee salattuna TLS:n sisällä. Verkkoliikennettä tarkkailemalla ei voida nähdä sivun sisältöä tai muita HTTP-pyynnön tietoja selväkielisenä ilman salauksen purkamista.

<details>
<summary>Näytä tuloste</summary>
  
```bash
* Host tls-test0xx.linuxkurssi.xyz:443 was resolved.
* IPv6: (none)
* IPv4: 4.231.xxx.xxx
*   Trying 4.231.xxx.xxx:443...
* ALPN: curl offers h2,http/1.1
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
*  CAfile: /etc/ssl/certs/ca-certificates.crt
*  CApath: /etc/ssl/certs
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.3 (IN), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384 / X25519MLKEM768 / id-ecPublicKey
* ALPN: server accepted http/1.1
* Server certificate:
*  subject: CN=tls-test0xx.linuxkurssi.xyz
*  start date: Sep 16 13:42:51 2026 GMT
*  expire date: Dec 15 13:42:50 2026 GMT
*  subjectAltName: host "tls-test0xx.linuxkurssi.xyz" matched cert's "tls-test0xx.linuxkurssi.xyz"
*  issuer: C=US; O=Let's Encrypt; CN=YE1
*  SSL certificate verify ok.
*   Certificate level 0: Public key type EC/prime256v1 (256/128 Bits/secBits), signed using ecdsa-with-SHA384
*   Certificate level 1: Public key type EC/secp384r1 (384/192 Bits/secBits), signed using ecdsa-with-SHA384
*   Certificate level 2: Public key type EC/secp384r1 (384/192 Bits/secBits), signed using ecdsa-with-SHA384
*   Certificate level 3: Public key type EC/secp384r1 (384/192 Bits/secBits), signed using ecdsa-with-SHA384
* Connected to tls-test0xx.linuxkurssi.xyz (4.231.xxx.xxx) port 443
* using HTTP/1.x
> GET / HTTP/1.1
> Host: tls-test0xx.linuxkurssi.xyz
> User-Agent: curl/8.14.1
> Accept: */*
> 
* Request completely sent off
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
< HTTP/1.1 200 OK
< Date: Wed, 16 Sep 2026 15:18:28 GMT
< Server: Apache/2.4.68 (Debian)
< Last-Modified: Wed, 16 Sep 2026 13:42:45 GMT
< ETag: "1d-65b99d79bdabc"
< Accept-Ranges: bytes
< Content-Length: 29
< Content-Type: text/html
< 
This is my public web server
* Connection #0 to host tls-test0xx.linuxkurssi.xyz left intact
```
</details>

Kun puolestaan http-yhteyttä tarkasteltiin komennolla ```curl -v http://tls-test0xx.linuxkurssi.xyz```, tulosteessa näkyivät HTTP-pyyntö ja palvelimen vastaus (GET / HTTP/1.1 ja Host: tls-test0xx.linuxkurssi.xyz) selväkielisinä. Koska HTTP ei käytä salausta, kaikki pyynnöt, vastaukset, otsakkeet sekä siirrettävä sisältö voidaan nähdä sellaisenaan verkkoliikennettä seuraamalla.

<details>
<summary>Näytä tuloste</summary>
  
```bash
* Host tls-test0xx.linuxkurssi.xyz:80 was resolved.
* IPv6: (none)
* IPv4: 4.231.xxx.xxx
*   Trying 4.231.xxx.xxx:80...
* Connected to tls-test0xx.linuxkurssi.xyz (4.231.xxx.xxx) port 80
* using HTTP/1.x
> GET / HTTP/1.1
> Host: tls-test0xx.linuxkurssi.xyz
> User-Agent: curl/8.14.1
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 200 OK
< Date: Wed, 16 Sep 2026 15:18:59 GMT
< Server: Apache/2.4.68 (Debian)
< Last-Modified: Wed, 16 Sep 2026 13:42:45 GMT
< ETag: "1d-65b99d79bdabc"
< Accept-Ranges: bytes
< Content-Length: 29
< Content-Type: text/html
< 
This is my public web server
* Connection #0 to host tls-test0xx.linuxkurssi.xyz left intact

```
</details>

Http-liikenteessä sekä pyynnön että vastauksen sisältö näkyvät selväkielisinä. Https-liikenteessä taas voidaan nähdä yhteyden muodostuminen, käytetty TLS-versio ja sertifikaattitiedot, mutta varsinainen sovellusdata on salattua eikä näy verkkoliikennettä seuraamalla. Tämä on https:n selkeä turvallisuusetu. Kuitenkin sekä http- että https-vastauksissa näkyi palvelimen tunnistetietoja sisältävä otsake (Server: Apache/2.4.68 (Debian)). Tämä voi olla turvallisuusriski, koska mahdollinen hyökkääjä saa helposti tietoa käytetystä ohjelmistosta ja sen versiosta ja näiden tietojen perusteella voidaan etsiä tunnettuja haavoittuvuuksia tai kohdistaa hyökkäyksiä tiettyä versiota vastaan.

