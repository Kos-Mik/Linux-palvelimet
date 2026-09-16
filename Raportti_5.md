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
