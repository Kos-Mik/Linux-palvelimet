# Linux-harjoitukset

## Johdanto 

Tässä tehtävässä käytetään Azure-ympäristöön luotuja Linux-virtuaalikoneita harjoitusalustana. Työskentely tapahtuu etäyhteyden kautta palvelimelle, jolle on määritetty kiinteä julkinen IP-osoite.

### Ohjelmistojen päivitykset

Kun omalle etäpalvelimelle on yhdistetty, kirjauduttu sinne annetuilla tunnuksilla ja salasana vaihdettu henkilökohtaiseksi onnistuneesti, onkin aika suorittaa siellä perusteellinen päivitys: 

```bash
sudo apt update
```
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

### SSH-avaimen luonti

Nyt luodaan SSH-avain autentikointimenetelmäksi, jotta etäpalvelimelle ei tarvitse aina kirjautua salasanan avulla ja tallennetaan ne suoraan oletushakemistoon ilman salausta. Tämän jälkeen se kopioidaan etäpalvelimelle ja testataan kirjautumista:

<p align="center">
<img width="720" height="381" alt="image" src="https://github.com/user-attachments/assets/6c972bf3-344a-4ef6-8576-8fe093ffb2a9" />
<img width="721" height="232" alt="image" src="https://github.com/user-attachments/assets/998c209a-f924-4c9a-b621-40dcff749453" />
<img width="721" height="198" alt="image" src="https://github.com/user-attachments/assets/4b935f25-6c82-4f24-8f38-a9191625d38a" />
  <br>
  <em>Kuvat 2, 3 ja 4. SSH avaimen luonti, kopiointi ja onnistunut kirjautumistestaus. Kaikki siis toimii.</em>
</p>

<br>
<br>

### Apachen asennus

Apachen asennuksessa toistetaan samat toimenpiteet kuin aiemmassa aiheeseen liittyvässä raportissa (Raportti_3). 

```bash
sudo apt install apache2
```
Asennuksen jälkeen tarkistetaan, että asennus on onnistunut:

```bash
sudo systemctl status apache2
```

ja muutetaan Apachen oletussivun sisältöä:

```bash
echo "Tally-ho, chaps! This is the default page of my new REMOTE web server" | sudo tee /var/www/html/index.html
```

<p align="center">
  <img width="727" height="346" alt="image" src="https://github.com/user-attachments/assets/5c3e04b0-c5c8-402b-bf26-ffab8e6aca54" />
  <img width="727" height="96" alt="image" src="https://github.com/user-attachments/assets/3f115f43-8106-4cb3-ae0b-94fffa8b622a" />
  <br>
  <em>Kuvat 5 ja 6. Onnistunut Apache2-asennus ja oletussivun muutos.</em>
</p>

<br>
<br>

Huomasin tässä vaiheessa hieman mopon keulineen, kun tunnilla olin ehtinyt viritellä jo palomuurinkin (**UFW**) päälle ja sallia vain portti 22:n siihen. Ihmettelinkin miksi julkisella IP-osoitteella yhdistettäessä ei ilmestynyt virtuaalikoneeni selaimeen mitään sisältöä, mutta sitten muistin, että myös portit 80 ja 443 pitää avata, jotta http- ja https-liikenne pääsevät läpi:

<p align="center">
<img width="449" height="107" alt="image" src="https://github.com/user-attachments/assets/6934961b-223f-4d57-8426-28632a6a4ded" />
<br>
<img width="571" height="82" alt="image" src="https://github.com/user-attachments/assets/b90e2477-4b72-426e-9936-425efb576487" />
  <br>
  <em>Kuvat 7 ja 8. Portit auki ja muokattu sivu esille!</em>
</p>

<br>
<br>

Lopuksi luodaan vielä uusi hakemisto tehtävänannon mukaisesti:

```bash
mkdir -p /home/linuxuser/public-sites
```
Ja varmistetaan vielä, että se on varmasti olemassa:

<p align="center">
<img width="719" height="39" alt="image" src="https://github.com/user-attachments/assets/fac869ca-a781-41c8-9ebd-e5b73aadd5fe" />
  <br>
  <em>Kuva 9. Luotu hakemist</em>
</p>

<br>
<br>



