# Linux-harjoitukset

## Johdanto 

Tässä tehtävässä käytetään Azure-ympäristöön luotuja Linux-virtuaalikoneita harjoitusalustana. Työskentely tapahtuu etäyhteyden kautta palvelimelle, jolle on määritetty kiinteä julkinen IP-osoite. Osoitteet ja muut yksilöivät tiedot ovat osittain tietoturvasyistä obfuskoitu.

## Ohjelmistojen päivitykset

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

## SSH-avaimen luonti

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

## Apachen asennus

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
  <em>Kuva 9. Luotu hakemisto</em>
</p>

<br>
<br>

## Networking

Tutkitaan aluksi etäpalvelimen IP-osoitteita. Ensiksi syötetään komento:

```bash
ip addr
```

Komento toi esiin vain palvelimen sisäverkon IP-osoitteet, koska pilvialustat piilottavat julkisen IP-osoitteen virtuaalikoneelta. Siksi ip addr näyttää vain sisäisen IP-osoitteen. Julkinen IP on palvelimen verkkoasetuksissa eikä käyttöjärjestelmässä. Julkisen IP-osoitteen näkee helpoimmin kysymällä sen internetistä:

```bash
curl ifconfig.me
```

<p align="center">
<img width="723" height="290" alt="image" src="https://github.com/user-attachments/assets/2d916786-b997-4dde-8d85-137a3dcd6945" />
<img width="723" height="37" alt="image" src="https://github.com/user-attachments/assets/6486cf12-9d18-4e5a-88b5-31f18c212cc2" />
  <br>
  <em>Kuvat 10 ja 11. Sisäverkon osoitteet ja julkinen IP-osoite</em>
</p>

<br>
<br>

### Pakettianalyysi

#### Ngrep

Asennetaan ohjeiden mukaisesti **ngrep** etäpalvelimelle:

```bash
sudo apt install ngrep 
```

ja avataan toinenkin terminaali ja yhdistetään myös sillä etäpalvelimelle.

#### HTTP-liikenteen tutkiminen

Suoritetaan **1 terminaalissa** komento:

```bash
sudo ngrep -d eth0 -W byline "" host <oma-julkinen-IP> and port 80
```

ja luodaan **2 terminaalissa** http-liikennettä:

```bash
url http://<oma-julkinen-IP>
```

Tällöin saatiin seuraavanlainen tuloste:

<details>
<summary>Näytä tuloste</summary>

 ```bash
######
T 10.0.xx.xx:36222 -> 4.231.xxx.xxx:80 [AP] #6
GET / HTTP/1.1.
Host: 4.231.xxx.xxx.
User-Agent: curl/8.14.1.
Accept: */*.
.

##
T 4.231.xx.xx:36222 -> 10.0.xx.xx:80 [AP] #8
GET / HTTP/1.1.
Host: 4.231.xxx.xxx.
User-Agent: curl/8.14.1.
Accept: */*.
.

##
T 10.0.xx.xx:80 -> 4.231.xx.xx:36222 [AP] #10
HTTP/1.1 200 OK.
Date: Thu, 10 Sep 2026 15:15:19 GMT.
Server: Apache/2.4.68 (Debian).
Last-Modified: Wed, 09 Sep 2026 14:45:12 GMT.
ETag: "46-65b0de6060148".
Accept-Ranges: bytes.
Content-Length: 70.
Vary: Accept-Encoding.
Content-Type: text/html.
.
Tally-ho, chaps! This is the default page of my new REMOTE web server

##
T 4.231.xx.xx:80 -> 10.0.xx.xx:36222 [AP] #12
HTTP/1.1 200 OK.
Date: Thu, 10 Sep 2026 15:15:19 GMT.
Server: Apache/2.4.68 (Debian).
Last-Modified: Wed, 09 Sep 2026 14:45:12 GMT.
ETag: "46-65b0de6060148".
Accept-Ranges: bytes.
Content-Length: 70.
Vary: Accept-Encoding.
Content-Type: text/html.
.
Tally-ho, chaps! This is the default page of my new REMOTE web server

########

```
</details>


Verkkoliikenteessä näkyy HTTP-pyyntö (GET / HTTP/1.1) asiakkaalta palvelimelle sekä palvelimen HTTP-vastaus (HTTP/1.1 200 OK). Tulosteessa näkyy myös verkkosivun sisältö (Tally-ho, chaps! This is the default page of my new REMOTE web server) selkeänä, koska liikenne kulkee tavallisella HTTP-protokollalla portissa 80. HTTP-liikennettä ei ole salattu, joten sekä otsikkotiedot että sivun sisältö voidaan nähdä suoraan verkkopaketeista. 

Suoritettu ngrep-komento ```sudo ngrep -d eth0 -W byline "" host <oma-julkinen-IP> and port 80``` sisältää seuraavat parametrit:

- **sudo** suorittaa komennon pääkäyttäjän oikeuksilla.
- **ngrep** on työkalu verkkopakettien tarkasteluun.
- **-d eth0** kuuntelee verkkoliikennettä verkkoliitännältä eth0.
- **-W byline** näyttää datan rivikohtaisesti helposti luettavassa muodossa.
- **""** on tyhjä hakulauseke, joten kaikki suodattimen ehdot täyttävä liikenne näytetään.
- **host** <oma-julkinen-IP> näyttää vain määritettyyn IP-osoitteeseen liittyvän liikenteen.
- **and** yhdistää IP-osoite- ja porttiehdot samaan suodattimeen.
- **port 80** näyttää vain HTTP-liikenteen portissa 80.

#### SSH

Nyt **1 terminaalissa** suoritetaan seuraava komento:

 ```bash
sudo ngrep -d eth0 -W byline "" port 22 
```

Sisältöä syntyi paljon ja nopeasti, joten tässä pieni katkelma tulosteesta:

<details>
<summary>Näytä tuloste</summary>

 ```bash
T 10.0.xx.xx:22 -> 87.92.xx.xx:17201 [AP] #7196
...Xt..}..P..E..(.7A...%....0.i#.Q...d....q...p.........!.@.......vK....k-.f......B .i...W^....(...5!.(,.....
..|/.......XU)Y.A8..R.@..U.U..y....Y.{F.?..x...mh..-...o".[.y...6./1.^B...
M.YU....
..x.a5j-.v..B_H.l.c....q+.C..Kn%...61..e...`....L.0.E.=..........{......h.<.....y.z..v..}..._%.f.3Cw...-n#....%..........._.mL..A*YORP..........{$.a.St.x6I.No.......~.\...t+%z.f..%.^.d........IL.k..Z/..v.............l~...;.~]0........:...>.#..>e....-...4......=,..].._..y:e...O..V.....U.R....S..z.p...'7.\...7~. [...:.........u.UIB.I:t4....3....2y......0..S.K..kp..`b(..$..!..je...b.US...|.`.rS|.p...X..aJ.-... o....i.=......~.Y....KJ.*p.....v..j2p.]W....z_.._(SdR^{AyMH....f. 6.......B"&.5"=.n.S..VT....;....$._`7*u..j..}.G."...I.FF..w........R.%I....6o..0.>hc...y\..y.../..?.....3;,.....]..........`..NqL..zF#.)!.......+..q`...:{..........?.6.,.S..g.XC...~*+.$.M..T&L.a.p)........)t3...B:..?......<...v.F..PC.U.^.FR.m..K../...**.-Ny.q...45.Z.).Z\.GP.....M4.N...(X,4....`..u-r..w.R.f.8.s(.q......a...k..y.......p.).....0.a...6.d..z..ro.z.$W..........c?..(*}B<....'.k..S..{@....W...;..1..y...=X...kC........-..f."...S,.k.Z.........bv...F.A..1...o.$.A...oI<..J....c...YCb.ft}..0ix,....nh...&&<..P...WN....d./..6.R.a+.P..@U.m.b.o.&..V........Up..vX..5.|......F..../...`!.U..aM.....$.m..gAS4...x.Elf.......!...'.b2...b....tI.
..R,.z..N...~Y...j ...@.bd}.7xL..B..@........Z.....}b8...6.0..9.G.{.2oN..\**...8.J-.......~.Ev.......6x.,....v.o.....;.....|.
.
#
T 87.92.xx.xx:17201 -> 10.0.xx.xx:22 [A] #7197
......
#
T 87.92.xx.xx:17201 -> 10.0.xx.xx:22 [A] #7198
......
#
T 10.0.xx.xx:22 -> 87.92.xx.xx:17201 [AP] #7199
..e/D..{....z....jx......,g).B.u.o........Q=/.........z.P&*.........!....... u'...........^...Y.?bO...j...v.k._7..1t....80....H:&....cVJ.4.y...~.'S....v....E6zu...j.^z....g.R.s..I#..:%......g..JL.7_..0.......\Q.c1L<.D.Mw......\..v..S...._*....%
a......R............<.e..U:.v.... @..R.O|l...HV~......c..4..R...z.e.....h..L.4.b.)P.......(..L.oqf.......'......nl
.k+...O...E....M.u.......|..;...o.........=;..V.Xo|}...c...y.=.|.H.. k%..{..8......A=H#.z=*..F..b.4.k....{.z.w...e..^....1...A......E....C....s+.,..g.....".......S...!...._o..-.............G.R.....~....H5....`.......I..d.o...>.t;..:f..M_...|i(...N..&.L=..7...Q..g<.<}.m.`.t..k-.[.I\T..`w..D....4.S$....c....n...{..z..........{5Y..u.J.F......d..=.M]...f>..V+B....=#..<V...1m.&..'.......Ozu.p.J../...+...?.'...j....
....(....O..$..^.....{|..^y.$.....(."...Tk.?:2....I[.m.......'3.....QI...CU.%/(.@...{...0..m.v....h.......[xi5..\W..M#..!.s8._...f..m..JM.T#...2&...L.E#.........{6...........p....0A...D......+.....1...R.7..p...>.j.)6....3.#a}G...T.....A."ZYz..g.............i.x.?.....^K.FM5.......(.......j{...p.......Z..;..+..uq0T...f....1A.............
...D..J.<..9........mz.d..7...M..Z.T....E.\.P...[P.Ej..l...FO.C3...5t9.r....?w...$..{0.s....!m..@...Z#V..a.|.M`..0...pXL..Y.9..s."...;L....nP....)...&.q...D...S.._9`....*E..._.4...W..gd....U.LU..D....
.4-....e......3.QT..n..7.....%..e.G..v.).....s.N_%...F...e#n..(....b?.?$&.Lj.......V...)..|..[.k...<.Z.H....c{>..X.n.=C.~7.; ;o{-...hp.........u..iIf".\8}.0.
.x.Z...........:...(.]...%.....W...}Y..1..j.@.d.Z.7..B.51..f...o..I&[.;Z.|I6.l........6&$.8".....C..,Wj..V....W.j...n.W..^......|..Of.z....H.z.h.C.).C.4..w!b.....kA...kWt@`......o.O..)..M.b.W'....pG..R..L..&.z ..N<......w..$.X.?2.:.r.D..(uT.2..C...n..R&.Ff0..4MM....Q.*.U.....=_..|.1......0...#.5....^..3.\o...>.......W...,.I.^^P....%...U.&M.....y.....0;$.l........`...r..?r....TI...<...zC.L....4.]....F.;...(.vbDH....+..\'.t!X..w......~....?r..L.=/...].ZZ.D..3.t.^....J..P......'..... .I._H...s..e.g{T..):q.O.......]...T..L.\...\...PVn..r.......]
9...3...<........^./...|^..D.....{...T.ejD(6^.'./L....A3..=...2.......n.^.a.E.".CB..|...;...%.&3...t>yV.._..Zlq.....I).....@..S...S...m.2......X..?..O..i..U......;T......k@.hY....l2...}5.....Wj.....e....i.........@.>.....O.`....;.4........Nwi.^{...g..CR..F..s7Pw.w.TM......?F.,}....ce....~..e.l&=....Tp 2.......!..T._.....|W.A.kVO5.9j.G..!O...g..F.h.nZ.f..I..}.d-D..D.G..Yi...5...l_2.lL..&.d .{.3...a..Ai.g>.[<...].x1.gx.u....M..r.".~!C..}y@.....Z..rn.)..E....Qv.....v.2.!.x..Z..6qo..{[..h.......{_5|.....>....h.....JKx.n.~^.A[..M!.._.......4..?
#
T 10.0.xx.xx:22 -> 87.92.xx.xx:17201 [AP] #7200
.hR)...Z.../..%6"...N.m.J...L....d?.....R.
......Fyp.{....0..9-.U..e8....5..../....c...a!........DC..4...A......n..+..$.,..)..I*;-1.
V

```
</details>

Eli SSH-liikennettä tutkaillessa syntyi lähinnä kasa epäselvää sotkua. Silti tulosteessa näkyi lähde- ja kohde-IP-osoitteet ja portit, liikenteen kulkusuunta ja pakettien koot ja määrät. Tunnuksia, salasanoja tai muuta selvää tekstiä ei tulosteesta löytynyt. Varmaankin lienee se syy miksi tätä protokollaa kutsutaan Secure Shelliksi. Liikenteessä näkyi oma julkinen IP-osoitteeni sekä palvelimen sisäinen IP-osoite. Tämä havainto siis tukee aiemmin opittua: virtuaalikone näkee oman osoitteensa vain sisäisenä IP-osoitteena, mutta yhteyttä muodostavan tahon julkinen IP-osoite näkyy normaalisti verkkoliikenteessä.

#### Ping

Tällä kertaa **1 terminaalissa** suoritetaan komento:

```bash
sudo ngrep -d eth0 -W byline "" icmp 
```

ja **2 terminaalissa** pingataan Googlen DNS:n eli **8.8.8.8**:

```bash
64 bytes from 8.8.8.8: icmp_seq=1 ttl=113 time=0.900 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=113 time=0.903 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=113 time=0.800 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=113 time=0.816 ms
```

Tämä liikenne näkyy 1 terminaalissa:

<details>
<summary>Näytä tuloste</summary>

 ```bash
I 10.0.xx.xx -> 8.8.8.8 8:0 #1
....S..j.....)...................... !"#$%&'()*+,-./01234567
#
I 8.8.8.8 -> 10.0.xx.xx 0:0 #2
....S..j.....)...................... !"#$%&'()*+,-./01234567
#
I 10.0.xx.xx -> 8.8.8.8 8:0 #3
....T..j............................ !"#$%&'()*+,-./01234567
#
I 8.8.8.8 -> 10.0.xx.xx 0:0 #4
....T..j............................ !"#$%&'()*+,-./01234567
#
I 10.0.xx.xx -> 8.8.8.8 8:0 #5
....U..j....Y....................... !"#$%&'()*+,-./01234567
#
I 8.8.8.8 -> 10.0.xx.xx 0:0 #6
....U..j....Y....................... !"#$%&'()*+,-./01234567
#
I 10.0.xx.xx -> 8.8.8.8 8:0 #7
....V..j....%>...................... !"#$%&'()*+,-./01234567
#
I 8.8.8.8 -> 10.0.0.33 0:0 #8
....V..j....%>...................... !"#$%&'()*+,-./01234567
```
</details>


<br>
<br>

Jos käytämme tällä kertaa liikenteen tutkimiseen **tcpdump**ia komennolla: 

```bash
sudo tcpdump -i eth0 icmp
```

niin 2 terminaalissa pingaus Googlen DNS:n:

```bash
64 bytes from 8.8.8.8: icmp_seq=1 ttl=113 time=0.868 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=113 time=0.878 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=113 time=0.976 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=113 time=0.856 ms
```

liikenne näkyy 1 terminaalissa seuraavanlaisesti

<details>
<summary>Näytä tuloste</summary>

```bash
15:57:15.803145 IP tls-testxxx > dns.google: ICMP echo request, id 3, seq 1, length 64
15:57:15.803996 IP dns.google > tls-testxxx: ICMP echo reply, id 3, seq 1, length 64
15:57:16.812214 IP tls-testxxx > dns.google: ICMP echo request, id 3, seq 2, length 64
15:57:16.813072 IP dns.google > tls-testxxx: ICMP echo reply, id 3, seq 2, length 64
15:57:17.836197 IP tls-testxxx > dns.google: ICMP echo request, id 3, seq 3, length 64
15:57:17.837158 IP dns.google > tls-testxxx: ICMP echo reply, id 3, seq 3, length 64
15:57:18.837275 IP tls-testxxx > dns.google: ICMP echo request, id 3, seq 4, length 64
15:57:18.838108 IP dns.google > tls-testxxx: ICMP echo reply, id 3, seq 4, length 64
```

</details>

<br>

Sekä **ngrep** että **tcpdump** näyttivät ICMP-pakettien kulkevan palvelimen ja Googlen DNS-palvelimen (8.8.8.8) välillä. Molemmista näkyivät echo Request- ja echo reply -viestit, jotka syntyvät ping-komennon yhteydessä.
Ngrep näytti pakettien sisällöstä enemmän raakadataa ja hyötykuormaa, kun taas tcpdumpin tuloste oli helpompi tulkita. Ngrep siis soveltuu hyvin pakettien sisällön tarkasteluun ja tekstipohjaisen datan analysointiin. Tcpdump taas antaa paremman yleiskuvan verkkoliikenteestä ja esittää protokollatiedot selkeämmin.

### Challenge edituser

Tässä osiossa luodaan **edituser**-niminen käyttäjä etäpalvelimella. Tarkoituksena on, että edituserilla ei ole sudo-oikeuksia vaan tarkoituksena on ainoastaan päästä muokkaamaan web-sisältöä. 

Ensin luodaan käyttäjä: 

```bash
sudo adduser edituser 
```

sitten luodaan **webdev**-ryhmä:

```bash
sudo groupadd webdev
```

lisätään sekä linuxuser että edituser kyseiseen ryhmään ja halutessa tarkistetaan tämän jälkeen ryhmät ja oikeudet (kuva 12):

```bash
sudo usermod -aG webdev linuxuser
```
```bash
sudo usermod -aG webdev edituser
```

asetetaan hakemiston ryhmä:

```bash
sudo chgrp webdev /home/linuxuser/public-sites
```

asetetaan setgid-bitti: 

```bash
sudo chmod 2775 /home/linuxuser/public-sites
```

Kyseisessä komennossa numero 2 asettaa setgid-bitin hakemistolle ja 775 ovat normaaleja Linux-oikeuksia (7 = rwx eli **omistaja**, 7 = rwx eli **ryhmä**, 5 = r-x eli **muut**. Omistaja ja ryhmä saavat lukea, kirjoittaa ja suorittaa ja muut vain lukea ja suorittaa). 

<p align="center">
<img width="723" height="435" alt="image" src="https://github.com/user-attachments/assets/f183068e-1335-4bc7-82b3-54f5159b3be4" />
  <br>
  <em>Kuva 12. Käyttäjät, ryhmät ja oikeudet</em>
</p>

<br>
<br>

