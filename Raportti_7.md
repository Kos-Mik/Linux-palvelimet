# Shell Scripting - perusteet

## Johdanto 

## Bash Shell

Alkuun otetaan tehtävänannon mukaisesti varmuuskopio **.bashrc**:stä ja varmistettu, että se on varmasti olemassa:

<p align="center">
<img width="648" height="97" alt="image" src="https://github.com/user-attachments/assets/5ab6fbad-ada1-4009-adde-45bafb24d43f" />
  <br>
  <em>Kuva 1. Varmuuskopio otettu.</em>
</p>
<br>
<br>

Tämän jälkeen avataan .bashrc **nano**-editorilla ja tehdään tiedostoon sellainen muokkaus, että terminaalin avautuessa tulee aina alkuun tervehdysteksti "Hello, Linuxuser". Tallennetaan tämä ja avataan uusi terminaali:

<p align="center">
<img width="726" height="393" alt="image" src="https://github.com/user-attachments/assets/4a1077c1-ef04-4a91-8994-4cd217e8fe72" />
<img width="731" height="200" alt="image" src="https://github.com/user-attachments/assets/838ce9ff-afb7-4f59-841b-9c35aa7124d2" />

  <br>
  <em>Kuvat 2 ja 3. Lisätty tervehdysteksti nano-editorilla ja testattu viesti uudella terminaalilla.</em>
</p>
<br>
<br>

Lisään tämän jälkeen nanolla vielä kaksi aliasta (**c**, joka suorittaa terminaalin tyhjennyskomennon ```clear``` ja **update** joka päivittää Linuxini ajantasalle ```sudo apt update && sudo apt upgrade -y```). Näitä komentoja on ainakin tämän kurssin aikana tullut käytettyä runsaasti. 
Ja vaikka ne eivät sellaisenaankaan kovin pitkiä ole, ajansäästöä se on pienikin ajansäästö. 

Muutan myös HISTSIZE (kuinka monta komentoa Bash pitää muistissa nykyisen istunnon aikana) ja HISTFILESIZE (kuinka monta komentoa tallennetaan pysyvästi tiedostoon) todella pieniksi (vain 2 ja 4) ja testaan miten tämä toimii:

<p align="center">
<img width="737" height="495" alt="image" src="https://github.com/user-attachments/assets/0d33a9d0-7005-4ea6-af67-11843ea5208a" />
<img width="733" height="495" alt="image" src="https://github.com/user-attachments/assets/579a12f0-d1f9-440e-b834-018969b2bafa" />
  
 <br>
  <em>Kuvat 4 ja 5. Lisätty aliakset nano-editorilla ja testattu komentohistoria, joka ei tässä tapauksessa muista <b>echo $HISTSIZE</b> -komentoa pidemmälle.</em>
</p>
<br>
<br>

Nyt tarkoitus on tehdä ./bashrc-tiedostosta omanlainen. Ensiksi kasvatan komentohistorian kokoa niin, että HISTSIZE muistaa 2000 ja HISTFILESIZE 5000 komentoa. Tämä helpottaa olennaisesti työtä, kun voi tarvittaessa vain painaa nuolinäppäintä ylös. Lisäsin myös uusina aliaksina **ll** eli listauskomennon ```ls -la```, IP-osoitteen pikatarkistuksena **myip** on alias komennolle ```ip addr show``` ja kun haluan löytää tiedoston nopeasti, olen laittanut komennolle ```find . -type f``` aliakseksi **ff**. Tervehdystekstin vaihdoin vain muotoon "Hello Minuxuser".

<p align="center">
<img width="722" height="56" alt="image" src="https://github.com/user-attachments/assets/b766631a-3a7e-4fa8-a371-adfe89b5084e" />
 <br>
  <em>Kuva 6. Testattu uutta nerokasta tiedostonhakujärjestelmää.</em>
</p>
<br>
<br>

## Shell Script

Tässä tehtävässä luodaan oma shell script. Valitsen tehtävistä a-vaihtoehdon, jossa tarkoituksena on luoda shell script, joka luo **project**-nimisen hakemiston, luo tänne **info.txt**-nimisen tiedoston, kirjoittaa tiedostoon käyttäjän **nimen** ja **kuluvan päivämäärän** ja lopuksi listaa project-hakemiston koko sisällön.

Aloitan luomalla scriptitiedoston nano-editorilla komennolla ```nano project.sh``` ja sinne lisään sisällöksi:

```bash
#!/bin/bash #Ns. "shebang" kertoo Linuxille, että scripti suoritetaan Bash-tulkilla, mikä varmistaa oikean suoritusympäristön (Geeksforgeeks, 2026).

mkdir project #Luo hakemiston

echo "Username: $USER" > project/info.txt #Luo info.txt-tiedoston käyttäjän nimellä
echo "Date: $(date)" >> project/info.txt #Lisää kuluvan päivämäärän info.txt.tiedostoon

ls -l project #Listaa hakemiston sisällön
```

Tämän jälkeen annetaan scriptille suoritusoikeus komennolla ```chmod +x project.sh```, suoritetaan scripti komennolla ```./project.sh``` ja tarkistetaan vielä info.txt-tiedoston sisältö ```cat project/info.txt```:

<p align="center">
<img width="731" height="309" alt="image" src="https://github.com/user-attachments/assets/45b58a25-96b9-4e87-b600-9881e7b9cdee" />
 <br>
  <em>Kuva 7. Suoritettu scripti ja tiedoston sisällön tarkistus.</em>
</p>
<br>
<br>


## Lähteet:

Geeksforgeeks. 2026. Shell Scripting – Understanding Shebang (#!/bin/bash). Luettavissa: https://www.geeksforgeeks.org/linux-unix/shell-scripting-define-bin-bash/. Luettu 6.10.2026.
