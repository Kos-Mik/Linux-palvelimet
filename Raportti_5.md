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
<img width="652" height="184" alt="image" src="https://github.com/user-attachments/assets/2cf73d34-f0e4-430f-9593-009e30090411" />
  <br>
  <em>Kuva 3. DNS-liikennettä havaittu!</em>
</p>
<br>
<br>

Tämä johtuu siitä, että kysely lähetettiin nyt ulkoiseen verkkoon DNS-palvelimelle 8.8.8.8 sen sijaan, että se olisi käsitelty paikallisesti resolverin (127.0.0.53) kautta, kuten alun perin tein.


## Name-Based VirtualHost




```sudo tcpdump -i eth0 port 53 -n -v```
```bash
sudo apt upgrade -y
```


<p align="center">
<img width="718" height="111" alt="image" src="https://github.com/user-attachments/assets/958553af-29ae-4b9d-a43b-ff777e8394b7" />
  <br>
  <em>Kuva 1. Salasanan onnistunut päivitys.</em>
</p>
<br>
<br>

## SSH-avaimen luonti
