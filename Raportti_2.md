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

Nyt meidän on poistettava kolme elukkaa **docs**-kansion **animals.txt**-tiedostosta...

<p align="center">
  <img width="694" height="308" alt="Näyttökuva 2026-08-26 181456" src="https://github.com/user-attachments/assets/c07d94bb-3486-44b4-95bf-9007458e65a6">
  <br>
  <em>Kuva 6. Animals.txt-tiedosto kolmen eläimen poistamisen jälkeen.</em>
</p>

... ja poistettava **vegetables.txt**-tiedosto kokonaan:

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

## 2. Grep and Pipe  

### Grep 

Seuraavana tehtävänä testataan grep-komentoa eri valitsimilla. Grep on yksinkertaistettuna hakutyökalu, joka mahdollistaa nopean tietojen haun tiedostoista ilman, että niitä tarvitsee avata editoriin. 
Alkuun luodaan **fruits.txt**-niminen tiedosto komennolla:

```bash
echo -e “apple\nbanana\norange\nApple pie” > fruits.txt
```
Tämä loi tekstitiedoston käyttäjän kotihakemistoon. Seuraavaksi testataan grep-komentoja eri valitsimien kanssa.

<br>

Kun halutaan etsiä tiedostosta kaikki rivit, joilla esiintyy sana **apple** ja tulostaa ne näytölle:
```bash
grep apple fruits.txt 
```
<br>

**-i** tarkoittaa tässä tapauksessa **ignore case** eli kirjainkoolla ei ole väliä, kun halutaan etsiä tiedostosta rivit, jossa sana **apple** esiintyy:
```bash
grep -i apple fruits.txt  
```
<br>

**-n** tässä tapauksessa näyttää hakutuloksen rivinumeron, kun halutaan etsiä tiedostosta rivit, jossa sana **apple** esiintyy:
```bash
grep -n apple fruits.txt
```
<br>

**-ni** on kahden edellisen yhdistelmä eli haku ei katso kirjainkokoa ja näyttää rivinumeron:
```bash
grep -ni apple fruits.txt
```
<br>

**-v** tuottaa käänteisen haun eli näyttää ne rivit, jotka eivät täsmää **apple**-hakusanan kanssa:
```bash
grep -v apple fruits.txt
```

<p align="center">
  <img width="397" height="282" alt="image" src="https://github.com/user-attachments/assets/4a5078d4-fbbb-476f-bebe-2b8472a29446" />
  <br>
  <em>Kuva 10. Grep-komennolla ja eri valitsimilla suoritetut haut</em>
</p>

<br>

### wc - word count

wc eli word count on työkalu, joka kertoo kuinka monta riviä, sanaa ja merkkiä teksti tai tiedosto sisältää. 

<br>

Lasketaan tiedostossa olevien rivien (**l**) määrä:
```bash
wc -l fruits.txt
```
<br>

Lasketaan tiedostossa olevien sanojen (**w**) määrä:
```bash
wc -w fruits.txt  
```
<br>

Lasketaan tiedostossa olevien merkkien (**c**) määrä:
```bash
wc -c fruits.txt
```
<br>

<p align="center">
  <img width="299" height="129" alt="image" src="https://github.com/user-attachments/assets/c6f3f39c-215b-4229-a450-912889c19269" />
  <br>
  <em>Kuva 11. wc-komennolla ja eri valitsimilla suoritetut haut</em>
</p>

<br>

### Pipe

Pipe yhdistää komentoja siten, että ensimmäisen komennon tuloste toimii seuraavan komennon syötteenä. Se on erityisen hyödyllinen silloin, kun useita komentoja halutaan ketjuttaa yhdeksi komentoriviksi. Tässä tehtävässä tarkoituksena on testata pipe-operaattorin käyttöä eri komentojen ja valitsimien kanssa.

Ensin luodaan uusi **animals.txt**-niminen tekstitiedosto kotihakemistoon:

```bash
echo -e "dog\ncat\nhorse\ncow\ncatfish" > animals.txt 
```

Seuraavaksi kokeillaan pipen käyttöä:

<br>

**cat** animals.txt näyttää tiedoston sisällön ja **grep cat** etsii tulosteesta rivit, joissa esiintyy sana **cat**:
```bash
cat animals.txt | grep cat
```
<br>

**cat** näyttää tiedoston sisällön ja **wc -l** laskee rivien määrän.
```bash
cat animals.txt | wc -l 
```
<br>

**cat** näyttää tiedoston sisällön, **sort** lajittelee rivit aakkosjärjestykseen ja **uniq** poistaa vierekkäiset duplikaattirivit.
```bash
cat animals.txt | sort | uniq
```
<br>

<p align="center">
  <img width="425" height="219" alt="image" src="https://github.com/user-attachments/assets/d3f78d33-521e-4f89-847c-48f2e848c8e8" />
  <br>
  <em>Kuva 12. pipe-operaattorilla tehdyt haut</em>
</p>

<br>

### GPL-2 License

Tässä tehtävässä haetaan Linuxin GPL-2 -lisenssistä tietoja käyttämällä aiemmin opittuja komentoja ja valitsimia.

<br>

Tarkastellaan kuinka monta riviä lisenssi sisältää:
```bash
wc -l /usr/share/common-licenses/GPL-2
```
Tulos: **338**

<br>

Etsitään grepillä lisenssitiedostosta kaikki rivit, jotka sisältävät sanan **GNU**, ja tulostaa ne näytölle.:
```bash
grep GNU /usr/share/common-licenses/GPL-2
```
Tulos: 
> GNU GENERAL PUBLIC LICENSE
> freedom to share and change it.  By contrast, the GNU General Public
> the GNU Lesser General Public License instead.)  You can apply it to
               >     GNU GENERAL PUBLIC LICENSE
  >  it under the terms of the GNU General Public License as published by
 >   GNU General Public License for more details.
 >   You should have received a copy of the GNU General Public License along
> library.  If this is what you want to do, use the GNU Lesser General

<br>

Lasketaan kuinka moni rivi sisältää sanan **GNU**:
```bash
grep GNU /usr/share/common-licenses/GPL-2 | wc -l
```
Tulos: **8**

<br>

Haetaan kaikki rivit, jotka sisältävät sanan **license**:
```bash
grep license /usr/share/common-licenses/GPL-2
```
Tulos:
> of this license document, but changing it is not allowed.
>  The licenses for most software are designed to take away your
> (2) offer you this license which gives you legal permission to copy,
> program will individually obtain patent licenses, in effect making the
> patent must be licensed for everyone's free use or not licensed at all.
> the term "modification".)  Each licensee is addressed as "you".
>    part thereof, to be licensed as a whole at no charge to all third
> this License, whose permissions for other licensees extend to the
>  4. You may not copy, modify, sublicense, or distribute the Program
> otherwise to copy, modify, sublicense or distribute the Program is
> this License will not have their licenses terminated so long as such
> Program), the recipient automatically receives a license from the
> license would not permit royalty-free redistribution of the Program by
> implemented by public license practices.  Many people have made
> to distribute software through any other system and a licensee cannot
>    with this program; if not, see <https://www.gnu.org/licenses/>.

<br>

Haetaan kaikki rivit, jotka sisältävät sanan **license**, mutta tällä kertaa ei kiinnitetä huomiota kirjainkokoon:
```bash
grep -i license /usr/share/common-licenses/GPL-2
```
Tulos: 
> GNU GENERAL PUBLIC LICENSE
> of this license document, but changing it is not allowed.
>  The licenses for most software are designed to take away your
> License is intended to guarantee your freedom to share and change free
> General Public License applies to most of the Free Software
> the GNU Lesser General Public License instead.)  You can apply it to
> price.  Our General Public Licenses are designed to make sure that you
> (2) offer you this license which gives you legal permission to copy,
> program will individually obtain patent licenses, in effect making the
> patent must be licensed for everyone's free use or not licensed at all.
>                    GNU GENERAL PUBLIC LICENSE
>  0. This License applies to any program or other work which contains
> under the terms of this General Public License.  The "Program", below,
> the term "modification".)  Each licensee is addressed as "you".
> covered by this License; they are outside its scope.  The act of
> notices that refer to this License and to the absence of any warranty;
> and give any other recipients of the Program a copy of this License
>    part thereof, to be licensed as a whole at no charge to all third
>    parties under the terms of this License.
>    License.  (Exception: if the Program itself is interactive but
> themselves, then this License, and its terms, do not apply to those
> this License, whose permissions for other licensees extend to the
> the scope of this License.
>  4. You may not copy, modify, sublicense, or distribute the Program
> except as expressly provided under this License.  Any attempt
> otherwise to copy, modify, sublicense or distribute the Program is
> void, and will automatically terminate your rights under this License.
> this License will not have their licenses terminated so long as such
>  5. You are not required to accept this License, since you have not
> prohibited by law if you do not accept this License.  Therefore, by
> Program), you indicate your acceptance of this License to do so, and
> Program), the recipient automatically receives a license from the
> this License.
> otherwise) that contradict the conditions of this License, they do not
> excuse you from the conditions of this License.  If you cannot
> License and any other pertinent obligations, then as a consequence you
> license would not permit royalty-free redistribution of the Program by
> the only way you could satisfy both it and this License would be to
> implemented by public license practices.  Many people have made
> to distribute software through any other system and a licensee cannot
> be a consequence of the rest of this License.
> original copyright holder who places the Program under this License
> countries not thus excluded.  In such case, this License incorporates
> the limitation as if written in the body of this License.
> of the General Public License from time to time.  Such new versions will
> specifies a version number of this License which applies to it and "any
> this License, you may choose any version ever published by the Free Software
>   11. BECAUSE THE PROGRAM IS LICENSED FREE OF CHARGE, THERE IS NO WARRANTY
>    it under the terms of the GNU General Public License as published by
>    the Free Software Foundation; either version 2 of the License, or
>    GNU General Public License for more details.
>    You should have received a copy of the GNU General Public License along
>    with this program; if not, see <https://www.gnu.org/licenses/>.
> parts of the General Public License.  Of course, the commands you use may
> This General Public License does not permit incorporating your program into
> Public License instead of this License.

<br>

Suunnitellaan oma esimerkki. Etsitään kaikki ne rivit, joissa esiintyy sana **program** kirjainkoosta riippumatta ja lasketaan rivien sisältämien sanojen määrä:
```bash
grep -i program /usr/share/common-licenses/GPL-2 | wc -w
```
Tulos: **817**

<br>

### Tiivistelmä GPL-2-lisenssin pääkohdista

- Ohjelmistoa saa käyttää vapaasti, sen lähdekoodia saa tutkia ja sitä saa kopioida ja jakaa edelleen.
- Lähdekoodia saa muokata.
- Muokattuja versioita saa levittää edelleen, mutta ne on julkaistava samalla GPL-2-lisenssillä.
- Lähdekoodin on oltava saatavilla ohjelmiston mukana tai käyttäjien saatavissa.
- Lisenssi ei anna takuuta ohjelmiston toimivuudesta.

## 3. btop 

### Asennus

btop-asennus tapahtuisi komennolla **sudo apt-get install btop**. Tämä on kuitenkin omalla virtuaalikoneellani jo valmiina, joten käynnistetään btop suoraan:

<p align="center">
  <img width="767" height="585" alt="Näyttökuva 2026-08-27 193134" src="https://github.com/user-attachments/assets/4ef08b93-960d-4e09-9bbd-b0b53b61ffdb" />
  <br>
  <em>Kuva 13. btop käynnistettynä</em>
</p>

<br>

Kun tarkistetaan missä ohjelmatiedostot sijaitsevat käytetään seuraavaa komentoa:
```bash
which btop
```
Tulos: 
> /usr/bin/btop

<br>

Etsitään käyttäjäkohtaiset konfiguraatiotiedostot:
```bash
find ~/.config -name "*btop*"
```

Tulos:
> /home/mikko/.config/btop
>
> **/home/mikko/.config/btop/btop.conf**
>
> /home/mikko/.config/btop/btop.log

**btop.conf** oli hakemamme tiedosto.

### Konfiguraatio

Tutkitaan tällä kertaa btopin konfiguraatiotiedostoja. Listataan kaikki btop-paketin asentamat tiedostot ja niiden sijainnit Linuxissa:

```bash
dpkg -L btop
```

Tulos:
> /.
> 
> /usr
> 
> /usr/bin
> 
> /usr/bin/btop
> 
> /usr/share
> 
> /usr/share/applications
> 
> /usr/share/applications/btop.desktop
> 
> /usr/share/btop
> 
> /usr/share/btop/themes
> 
> /usr/share/btop/themes/HotPurpleTrafficLight.theme
> 
> /usr/share/btop/themes/adapta.theme
> 
> /usr/share/btop/themes/adwaita.theme
> 
> /usr/share/btop/themes/ayu.theme
> 
> /usr/share/btop/themes/dracula.theme
> 
> /usr/share/btop/themes/dusklight.theme
> 
> /usr/share/btop/themes/elementarish.theme
> 
> /usr/share/btop/themes/everforest-dark-hard.theme
> 
> /usr/share/btop/themes/everforest-dark-medium.theme
> 
> /usr/share/btop/themes/flat-remix-light.theme
> 
> /usr/share/btop/themes/flat-remix.theme
> 
> /usr/share/btop/themes/greyscale.theme
> 
> /usr/share/btop/themes/gruvbox_dark.theme
> 
> /usr/share/btop/themes/gruvbox_dark_v2.theme
> 
> /usr/share/btop/themes/gruvbox_material_dark.theme
> 
> /usr/share/btop/themes/horizon.theme
> 
> /usr/share/btop/themes/kyli0x.theme
> 
> /usr/share/btop/themes/matcha-dark-sea.theme
> 
> /usr/share/btop/themes/monokai.theme
> 
> /usr/share/btop/themes/night-owl.theme
> 
> /usr/share/btop/themes/nord.theme
> 
> /usr/share/btop/themes/onedark.theme
> 
> /usr/share/btop/themes/paper.theme
> 
> /usr/share/btop/themes/solarized_dark.theme
> 
> /usr/share/btop/themes/solarized_light.theme
> 
> /usr/share/btop/themes/tokyo-night.theme
> 
> /usr/share/btop/themes/tokyo-storm.theme
> 
> /usr/share/btop/themes/tomorrow-night.theme
> 
> /usr/share/btop/themes/whiteout.theme
> 
> /usr/share/doc
> 
> /usr/share/doc/btop
> 
> /usr/share/doc/btop/README.md.gz
> 
> /usr/share/doc/btop/changelog.Debian.gz
> 
> /usr/share/doc/btop/changelog.gz
> 
> /usr/share/doc/btop/copyright
> 
> /usr/share/icons
> 
> /usr/share/icons/hicolor
> 
> /usr/share/icons/hicolor/48x48
> 
> /usr/share/icons/hicolor/48x48/apps
> 
> /usr/share/icons/hicolor/48x48/apps/btop.png
> 
> /usr/share/icons/hicolor/scalable
> 
> /usr/share/icons/hicolor/scalable/apps
> 
> /usr/share/icons/hicolor/scalable/apps/btop.svg
> 
> /usr/share/man
> 
> /usr/share/man/man1
> 
> /usr/share/man/man1/btop.1.gz

Luodaan btopin conf-tiedostosta varmuuskopio:

```bash
cp ~/.config/btop/btop.conf ~/.config/btop/btop.conf.orig
```
<br>

Ja siellä on se on hyvässä tallessa:
<p align="center">
  <img width="795" height="584" alt="image" src="https://github.com/user-attachments/assets/e8c9875c-2821-48d6-b1f6-05bf1758ac31" />
  <br>
  <em>Kuva 14. alkuperäinen ja varmuuskopioitu conf-tiedosto</em>
</p>

<br>

<p align="center">
  <img width="719" height="538" alt="image" src="https://github.com/user-attachments/assets/d8a9e264-5879-4571-952f-321ad5f4e522" />
  <img width="719" height="541" alt="image" src="https://github.com/user-attachments/assets/a4c7d4d2-4c39-4cd3-824e-f2a364972888" />
  <br>
  <em>Kuvat 14 ja 15. muokattuja asetuksia conf-tiedostoissa ja niiden tulokset</em>
</p>
<br>
**update_ms** = 300, **proc_tree** = True ja **custom_cpu_name** = "Skynet" tuottivat tuloksia. Kun yritin proc_tree:n - tai mihin tahansa muuhun boolean-arvon omaavaan asetukseen laittaa jotain muuta kuin True tai False, järjestelmä korjasi itse itsensä aina, kun btopin käynnisti uudelleen ja arvot palasivat oletuksille. En onnistunut siis rikkomaan btopia ainakaan conf-tiedoston kautta.

### Testikuorman luonti

Kuormitetaan testausmielessä järjestelmää pingaamalla Googlen DNS:n lyhyillä intervalleilla:

```bash
ping -i 0.1 8.8.8.8 
```
<br>
<p align="center">
  <img width="784" height="579" alt="image" src="https://github.com/user-attachments/assets/f879a58d-0d17-4096-a9d9-fd65b8a77ef5" />
  <img width="785" height="579" alt="image" src="https://github.com/user-attachments/assets/cee6f479-39cb-4a12-9832-b906ad02c60b" />
  <br>
  <em>Kuvat 16 ja 17. btop pingi päällä ja ilman</em>
</p>

Ping lähetti ICMP-paketteja 0,1 sekunnin välein, mikä aiheutti selkeää verkkoliikennettä.

Seuraavaksi kuormitetaan prosessoria:

```bash
yes > /dev/null 
```
<br>
<p align="center">
 <img width="780" height="575" alt="image" src="https://github.com/user-attachments/assets/2fac6359-a879-440e-b06a-1d68ffe9989c" />
 <img width="782" height="578" alt="image" src="https://github.com/user-attachments/assets/1df2cacc-2cee-4b8e-8fb8-e629e06d5fc5" />
  <br>
  <em>Kuvat 18 ja 19. btop prosessorin kuormituksella ja ilman</em>
</p>

Komento yes > /dev/null kuormitti yhtä prosessoriydintä täyteen käyttöasteeseen.

<br>

Kokonaisuudessaan btopin tietojen perusteella järjestelmä toimii hyvin. Yksi prosessorin ytimistä oli 100 % käytössä yes-prosessin vuoksi, mutta kokonaiskuormitus oli siitä huolimatta melko alhainen, koska muut ytimet olivat lähes käyttämättömiä. Muistia oli runsaasti vapaana, swap-muistia ei käytetty ja levytoiminta oli vähäistä. Verkkoliikenteessä näkyi ping-komennon aiheuttama liikenne. Järjestelmällä on kuitenkin riittävästi resursseja, eikä testikuormitus selvästikään aiheuta suorituskykyongelmia.

## 4. Asennetaan oma sovellus

Asennan ncdu-levytilan analysointiohjelman, jotta voin tutkia mikä kansio vie järjestelmästäni eniten tilaa:

```bash
sudo apt install ncdu
```
<br>

Suoritetaan ncdu:
```bash
ncdu
```
<br>
<p align="center">
 <img width="783" height="576" alt="image" src="https://github.com/user-attachments/assets/3b3b667b-5f43-410e-9ddc-a4d476715207" />
  <br>
  <em>Kuva 20. ncdu:n tulokset</em>
</p>
<br>

ncdu:n perusteella suurin osa kotihakemiston levytilasta on välimuistitiedostoissa ja selaimen tiedoissa. Eniten tilaa vie .cache-hakemisto (40,2 MiB), joka sisältää ohjelmien välimuistitiedostoja. Toiseksi eniten tilaa vie .mozilla-hakemisto (19,0 MiB), joka sisältää Firefox-selaimen asetuksia ja välimuistitiedostoja. Muut kansiot ovat huomattavasti pienempiä. Kotihakemiston koko on kokonaisuudessaan melko pieni, ja uskoisin, että virtuaalikoneelle asetettu 60 gigatavun levykoko tulee olemaan enemmän kuin tarpeeksi tällä kurssilla. En onnistunut paikantamaan ncdu:n konfiguraatiotiedostoa, joten en voinut testata sen toiminnallisuutta asetuksia muokkaamalla. Käytin siis tätä pelkillä oletusasetuksilla.




