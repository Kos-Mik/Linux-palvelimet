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

### SSH-avaimen luonti

Nyt luodaan SSH-avain autentikointimenetelmäksi, jotta etäpalvelimelle ei tarvitse aina kirjautua salasanan avulla ja tallennetaan ne suoraan oletushakemistoon ilman salausta. Tämän jälkeen se kopioidaan etäpalvelimelle ja testataan kirjautumista:

<p align="center">
<img width="720" height="381" alt="image" src="https://github.com/user-attachments/assets/6c972bf3-344a-4ef6-8576-8fe093ffb2a9" />
<img width="721" height="232" alt="image" src="https://github.com/user-attachments/assets/998c209a-f924-4c9a-b621-40dcff749453" />
<img width="721" height="198" alt="image" src="https://github.com/user-attachments/assets/4b935f25-6c82-4f24-8f38-a9191625d38a" />

  <br>
  <em>Kuvat 2, 3 ja 4. SSH avaimen luonti, kopiointi ja onnistunut kirjautumistestaus. Kaikki siis toimii.</em>
</p>

### Apachen asennus

Apachen asennuksessa toistetaan samat toimenpiteet kuin aiemmassa aiheeseen liittyvässä raportissa (Raportti_3). 
