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

Lisään tämän jälkeen nanolla vielä kaksi aliasta (**c**, joka suorittaa terminaalin tyhjennyskomennon **clear** ja **update** joka päivittää Linuxini ajantasalle **sudo apt update && sudo apt upgrade -y**). Näitä komentoja on ainakin tämän kurssin aikana tullut käytettyä runsaasti. 
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



