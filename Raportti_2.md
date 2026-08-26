# Komentorivi

## Johdanto

Tässä tehtävässä harjoitellaan komentorivin käyttöä Linux-käyttöjärjestelmässä. Komentorivi on yksi Linuxin tärkeimpiä työkaluja, sillä Linux on alun perin suunniteltu järjestelmänvalvojien ja palvelinkäyttöön, missä tehokkuus ja automaatio ovat tärkeämpiä kuin graafinen käyttöliittymä. 

## 1. Basic Commands

Ensimmäinen tehtävänanto on luoda kuvan mukainen hakemisto:

<p align="center">
  <img width="210" height="170" alt="image" src="https://github.com/user-attachments/assets/f0c23e7b-4c68-483f-8bf8-2d9b86623ce7">
  <br>
  <em>Kuva 1. Tehtävänannossa määritelty hakemisto.</em>
</p>

Aloitetaan luomalla tehtäväannon kyseinen hakemisto seuraavilla komennoilla:

```bash
mkdir -p ~/practice/{docs,images,backups,archive}
```

```bash
touch ~/practice/docs/{notes1.txt,notes2.txt,notes3.txt,notes4.txt}
```

Seuraavaksi lisätään tekstieditorilla **notes1.txt**-tiedostoon 10 faunan edustajaa ja **notes2.txt**-tiedostoon 10 flooran edustajaa. Eläimiä on oikeasti vaaditut 10 kappaletta. Kisu vain jäi vahingossa piiloon ylimpään riviin kuvakaappausta otettaessa.

<p align="center">
  <img width="697" height="279" alt="Näyttökuva 2026-08-26 175517" src="https://github.com/user-attachments/assets/7b5a3123-6a6a-4b08-bc76-236ca6942235">
  <br>
  <em>Kuva 2. notes1.txt-tiedoston sisältö.</em>
</p>

<p align="center">
  <img width="697" height="310" alt="Näyttökuva 2026-08-26 175733" src="https://github.com/user-attachments/assets/a44d6e38-3b1b-418d-b7f1-ec6cedfa2ca7">
  <br>
  <em>Kuva 3. notes2.txt-tiedoston sisältö.</em>
</p>

Seuraavaksi vaihdetaan näiden tekstitiedostojen nimet tehtävänannon (**notes1.txt → animals.txt** ja **notes2.txt → vegetables.txt**) mukaisesti:

```bash
mv ~/practice/docs/notes1.txt ~/practice/docs/animals.txt
```

```bash
mv ~/practice/docs/notes2.txt ~/practice/docs/vegetables.txt
```

Nimet ovat nyt vaihtuneet:

<p align="center">
  <img width="796" height="587" alt="Näyttökuva 2026-08-26 175952" src="https://github.com/user-attachments/assets/c323b1fa-36d7-4bc4-9e1c-fda5efb418bf">
  <br>
  <em>Kuva 4. Tiedostot uudelleennimeämisen jälkeen.</em>
</p>

Siirretään nämä muokatut tiedostot aiemmin luomaamme **backups**-kansioon:

```bash
cp ~/practice/docs/animals.txt ~/practice/backups
```

```bash
cp ~/practice/docs/vegetables.txt ~/practice/backups
```

Siellä ne ovat nyt suojassa ikäviltä yllätyksiltä:

<p align="center">
  <img width="802" height="585" alt="Näyttökuva 2026-08-26 180329" src="https://github.com/user-attachments/assets/9db5f57e-592b-4d22-b667-3de761f40e5d">
  <br>
  <em>Kuva 5. Animals.txt- ja vegetables.txt-tiedostot backups-kansiossa.</em>
</p>

Nyt meidän on poistettava kolme elukkaa **docs**-kansion **animals.txt**-tiedostosta ja poistettava **vegetables.txt** kokonaan:

<p align="center">
  <img width="694" height="308" alt="Näyttökuva 2026-08-26 181456" src="https://github.com/user-attachments/assets/c07d94bb-3486-44b4-95bf-9007458e65a6">
  <br>
  <em>Kuva 6. Animals.txt-tiedosto kolmen eläimen poistamisen jälkeen.</em>
</p>

```bash
rm ~/practice/docs/vegetables.txt
```

Seuraavaksi korjataankin nämä tarkoitukselliset "mokat" palauttamalla varmuuskopiot backups-kansiosta takaisin docs-kansioon:

```bash
cp ~/practice/backups/* ~/practice/docs/
```
<p align="center">
  <img width="796" height="585" alt="Näyttökuva 2026-08-26 181921" src="https://github.com/user-attachments/assets/3dff9a89-7f9f-4f2a-a505-618ea9dadf16" />
  <br>
  <em>Kuva 7. Tiedostot palautettuina docs-kansiossa.</em>
</p>

Tässä kohdin tar-komennolla kootaan tiedostot yhdeksi arkistoksi ja gzip pakkaa arkiston. Käytetään valitsimia **c** = create - eli luodaan arkisto, **z** = käytetään gzip-pakkausta, **v** = verbose - eli näytetään käsiteltävät tiedostot ja **f** = file eli arkiston nimi. Siirretään vielä pakattu tiedosto **archive**-kansioon
```bash
tar -czvf backup.tar.gz ~/practice/backups
```
```bash
mv backup.tar.gz ~/practice/archive
```

<p align="center">
  <img width="799" height="585" alt="image" src="https://github.com/user-attachments/assets/54c0aced-824f-486f-9831-717b7d2498e0" />
  <br>
  <em>Kuva 8. Pakattu backup-tiedosto archive-kansiossa</em>
</p>

Luodaan uusi test-niminen hakemisto:

```bash
mkdir -p ~/test
```

Ja puretaan pakattu tiedosto sinne:

```bash
tar -xzvf ~/practice/archive/backup.tar.gz -C ~/test
```

Huppista! Nyt tulikin näköjään kaikki yläkansiotkin mukaan:

<p align="center">
  <img width="375" height="271" alt="image" src="https://github.com/user-attachments/assets/66d48cfd-37eb-4f09-ac50-859bb85319d2" />
  <br>
  <em>Kuva 9. Hieman pieleen mennyt pakkaaminen ja purkaminen</em>
</p>

Arkistointikomennot selvästikin omalla kohdallani vaativat hieman lisää opiskelua, koska en yrityksistä huolimatta ole saanut pelkkää backup-kansiota pakattua vaan koko hakemisto on mennyt kerralla sinne.






