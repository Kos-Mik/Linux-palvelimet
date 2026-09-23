# Linux työkoneena

## Johdanto 

Tässä harjoituksessa Osoitteet ja muut yksilöivät tiedot ovat osittain tietoturvasyistä obfuskoitu.

## Git

Ensin on tarkistettava GitHubista omat sähköpostiasetukset - ja että GitHub on luonut anonymisoidun noreply-osoitteen sekä pitää oikean sähköpostiosoitteeni piilossa julkisuudelta:

<p align="center">
<img width="954" height="723" alt="image" src="https://github.com/user-attachments/assets/0b09cd92-4470-4c63-b457-86252afec2c9" />
  <br>
  <em>Kuva 1. Sähköpostiasetukset ja noreply-osoite.</em>
</p>
<br>
<br>

Seuraavaksi mennään paikalliselle virtuaalikoneelle ja asennetaan sinne Git komennolla ```sudo apt install git``` ja tarkastamalla sen versio komennolla ```git --version```:

<p align="center">
<img width="407" height="36" alt="image" src="https://github.com/user-attachments/assets/02771c7f-dd32-465b-8ec5-93b1cca55897" />
  <br>
  <em>Kuva 2. Asentunut Git-versio</em>
</p>
<br>
<br>

Tämän jälkeen konfiguroitiin **global user email** ja **global user name** GitHubin profiilitietojeni avulla. Tämä tehtiin komennoilla  ```git config --global user.email "99XXX9XX+Kos-Mik@users.noreply.github.com"``` ja ```git config --global user.name "Kos-Mik"```.
Global user -tiedot lisätään sen vuoksi, että nämä yhdistävät tehdyt commitit omaan profiiliini. Tarkistetaan vielä, että nämä ovat tallentuneet ```git config --global --list``` -komennolla.

<p align="center">
<img width="496" height="53" alt="image" src="https://github.com/user-attachments/assets/34798a05-3507-4aa7-a178-f32441bb3490" />
  <br>
  <em>Kuva 3. Global user email ja global user name</em>
</p>
<br>
<br>
