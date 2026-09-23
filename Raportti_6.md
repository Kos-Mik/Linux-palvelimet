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

#### Local VM

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

Nyt luodaan uusi SSH avainpari GitHubia varten ja annetaan sille nimeksi **github_key**. Luodaan samalla nanon avulla SSH-konfiguraatiotiedosto ja laitetaan sinne tarvittavat asetukset, jotta SSH tietää käyttää tätä avainta eikä oletusavainta:

<p align="center">
<img width="893" height="380" alt="image" src="https://github.com/user-attachments/assets/c541831e-c16c-4ad3-83aa-7ada55af641f" />
<img width="580" height="146" alt="image" src="https://github.com/user-attachments/assets/f3fa8056-3d70-4c9e-8f45-de24675a0760" />
  <br>
  <em>Kuvat 4 ja 5. Luotu SSH-avain ja konfiguraatiotiedosto</em>
</p>
<br>
<br>

Lopuksi lisätään julkinen avain (löytyy komennolla ```cat ~/.ssh/github_key.pub```) GitHubiin ja testataan yhteys vielä komennolla ```ssh -T git@github.com```:

<p align="center">
<img width="1048" height="556" alt="image" src="https://github.com/user-attachments/assets/8b314f88-72fd-42f7-8719-2893dc2cbbbd" />
<img width="818" height="56" alt="image" src="https://github.com/user-attachments/assets/23411284-654a-406e-8db7-53af7f1a9d29" />

  <br>
  <em>Kuvat 6 ja 7. SSH-avain lisättynä GitHubiin ja onnistunut yhteystesti</em>
</p>
<br>
<br>

#### Git-testing

Avaan GitHubissa kurssia varten luodun testirepositorion osoitteesta https://github.com/linuxkurssi/git-testing/tree/main ja kopioin sieltä kloonaamista varten SSH-URLin:

<p align="center">
<img width="399" height="325" alt="image" src="https://github.com/user-attachments/assets/d508815a-9c67-4c67-aed3-ebf0b14259a1" />
  <br>
  <em>Kuva 8. SSH-URL</em>
</p>
<br>
<br>

Tämän jälkeen kloonaan virtuaalikoneen kautta repositorion ja katson, että se löytyy hakemistosta:

<p align="center">
<img width="676" height="197" alt="image" src="https://github.com/user-attachments/assets/30df192d-fb19-4602-bb2e-67c93bf85640" />
  <br>
  <em>Kuva 9. SSH-URL</em>
</p>
<br>
<br>

Tämän jälkeen loin nanolla Linux-vinkin sisältävän txt-tiedoston samaan hakemistoon, tallensin sen ja tarkistin varmuuden vuoksi mikä tiedosto on uusin komennolla ```git status```:

<p align="center">
<img width="529" height="198" alt="image" src="https://github.com/user-attachments/assets/243a1435-d53b-457d-85ac-e392ead31379" />
<img width="697" height="162" alt="image" src="https://github.com/user-attachments/assets/9e68ff4d-5e3c-4ef9-b0af-f435def6a8ea" />

  <br>
  <em>Kuva 10. Vinkki</em>
</p>
<br>
<br>

Nyt on aika lisätä vinkkini testirepositorioon. Laittamalla git add, git commit ja lopuksi git push -komennot tiedostoni on lähetetty onnistuneesti GitHubiin. Unohdin aluksi käydä hyväksymässä opettajan kutsun testirepositorioon, joten push ei onnistunut. Hyväksymisen jälkeen push onnistui:

<p align="center">
<img width="710" height="451" alt="image" src="https://github.com/user-attachments/assets/45559c1e-d4e3-45c7-b0ed-f5ffa0fd723f" />
<img width="1325" height="211" alt="image" src="https://github.com/user-attachments/assets/d7beb434-98d5-4974-be96-8a3e5f038d04" />
  <br>
  <em>Kuvat 11 ja 12. Välivaiheet ja muokkaukseni repositoriossa</em>
</p>
<br>
<br>

Lopuksi luin vielä toisten antamia Linux-vinkkejä:

<p align="center">
<img width="726" height="288" alt="image" src="https://github.com/user-attachments/assets/bae11316-f34f-4c66-a924-5f00ccde060b" />
  <br>
  <em>Kuva 13. Toisen käyttäjän luoma Linux-vinkki</em>
</p>
<br>
<br>



