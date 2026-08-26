# Komentorivi

## Johdanto

Tässä tehtävässä harjoitellaan komentorivin käyttöä Linux-käyttöjärjestelmässä. Komentorivi on yksi Linuxin tärkeimpiä työkaluja, sillä Linux on alun perin suunniteltu järjestelmänvalvojien ja palvelinkäyttöön, missä tehokkuus ja automaatio ovat tärkeämpiä kuin graafinen käyttöliittymä. 

## Basic Commands

- Ensimmäinen tehtävänanto on luoda kuvan mukainen kansiorakenne:

<img width="210" height="170" alt="image" src="https://github.com/user-attachments/assets/f0c23e7b-4c68-483f-8bf8-2d9b86623ce7" />
  
- Aloitetaan luomalla tehtäväannon kyseinen kansiorakenne seuraavilla komennoilla:

```bash
mkdir -p ~/practice/{docs,images,backups,archive}
```
```bash
touch ~/practice/docs/{notes1.txt,notes2.txt,notes3.txt,notes4.txt}
```
- Seuraavaksi lisätään tekstieditorilla **notes1.txt**-tiedostoon 10 faunan edustajaa ja **notes2.txt**-tiedostoon 10 flooran edustajaa. Eläimiä on oikeasti vaaditut 10 kappaletta. Kisu vain jäi vahingossa piiloon ylimpään riviin kuvakaappausta otettaessa.
<img width="697" height="279" alt="Näyttökuva 2026-08-26 175517" src="https://github.com/user-attachments/assets/7b5a3123-6a6a-4b08-bc76-236ca6942235" />
<img width="697" height="310" alt="Näyttökuva 2026-08-26 175733" src="https://github.com/user-attachments/assets/a44d6e38-3b1b-418d-b7f1-ec6cedfa2ca7" />

- Seuraavaksi vaihdetaan näiden tekstitiedostojen nimet tehtävänannon (notes1.txt > animals.txt & notes2.txt > vegetables.txt)  mukaisesti: 
```bash
mv ~/practice/docs/notes1.txt ~/practice/docs/animals.txt 
```
```bash
mv ~/practice/docs/notes2.txt ~/practice/docs/vegetables.txt 
```
- Nimet ovat nyt vaihtuneet:
  
<img width="796" height="587" alt="Näyttökuva 2026-08-26 175952" src="https://github.com/user-attachments/assets/c323b1fa-36d7-4bc4-9e1c-fda5efb418bf" />

- Siirretään nämä muokatut tiedostot aiemmin luomaamme **backups**-kansioon:

```bash
cp ~/practice/docs/animals.txt ~/practice/backups
```
```bash
cp ~/practice/docs/vegetables.txt ~/practice/backups
```

- Siellä ne ovat nyt suojassa ikäviltä yllätyksiltä:

<img width="802" height="585" alt="Näyttökuva 2026-08-26 180329" src="https://github.com/user-attachments/assets/9db5f57e-592b-4d22-b667-3de761f40e5d" />

- Nyt meidän on poistettava kolme elukkaa docs-kansion animals.txt-tiedostosta ja poistettava vegetables.txt kokonaan:

<img width="694" height="308" alt="Näyttökuva 2026-08-26 181456" src="https://github.com/user-attachments/assets/c07d94bb-3486-44b4-95bf-9007458e65a6" />

```bash
rm ~/practice/docs/vegetables.txt
```

  



