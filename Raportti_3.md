# Apache2

## Johdanto

Tässä tehtävässä asennetaan virtuaalikoneelle Apache2, joka on yksi maailman laajimmin käytetyistä avoimen lähdekoodin verkkopalvelinohjelmistoista (Heinonen 2026). Tämän lisäksi Apache-palvelimeen luodaan tarvittavat VirtualHost-määritykset ja muut konfiguraatiot, joiden avulla verkkosivustoja voidaan ajaa palvelimella.

### Apachen asennus ja konfiguraatiot

Ensimmäinen tehtävä on asentaa itse Apache2:

```bash
sudo apt install apache2
```
Asennuksen jälkeen tarkistetaan, että asennus on onnistunut:

```bash
sudo systemctl status apache2
```

<p align="center">
  <img width="740" height="347" alt="Näyttökuva 2026-09-02 181139" src="https://github.com/user-attachments/assets/28ad699f-da33-4365-8316-53a9bc5869ea" />
  <br>
  <em>Kuva 1. Onnistunut Apache2-asennus.</em>
</p>

<br>

Tarkistetaan myös, että Apachen oletussivu avautuu sekä selaimessa että käyttämällä **curl**-komentoa:

<p align="center">
  <img width="1061" height="716" alt="Näyttökuva 2026-09-02 181320" src="https://github.com/user-attachments/assets/572f15ac-966e-4e18-9be9-11d5a99aad39" />
  <br>
  <em>Kuva 2. Apachen oletussivu selaimessa</em>
</p>

<br>

Ja kun käytetään curlia...

```bash
curl http://localhost
```
...konsoliin pamahtaa sivun lähdekoodi: 

<details>
<summary>Näytä lähdekoodi</summary>
  
```bash
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Apache2 Debian Default Page: It works</title>
    <style type="text/css" media="screen">
  * {
    margin: 0px 0px 0px 0px;
    padding: 0px 0px 0px 0px;
  }

  body, html {
    padding: 3px 3px 3px 3px;

    background-color: #D8DBE2;

    font-family: Verdana, sans-serif;
    font-size: 11pt;
    text-align: center;
  }

  div.main_page {
    position: relative;
    display: table;

    width: 800px;

    margin-bottom: 3px;
    margin-left: auto;
    margin-right: auto;
    padding: 0px 0px 0px 0px;

    border-width: 2px;
    border-color: #212738;
    border-style: solid;

    background-color: #FFFFFF;

    text-align: center;
  }

  div.page_header {
    height: 99px;
    width: 100%;

    background-color: #F5F6F7;
  }

  div.page_header span {
    margin: 15px 0px 0px 50px;

    font-size: 180%;
    font-weight: bold;
  }

  div.page_header img {
    margin: 3px 0px 0px 40px;

    border: 0px 0px 0px;
  }

  div.table_of_contents {
    clear: left;

    min-width: 200px;

    margin: 3px 3px 3px 3px;

    background-color: #FFFFFF;

    text-align: left;
  }

  div.table_of_contents_item {
    clear: left;

    width: 100%;

    margin: 4px 0px 0px 0px;

    background-color: #FFFFFF;

    color: #000000;
    text-align: left;
  }

  div.table_of_contents_item a {
    margin: 6px 0px 0px 6px;
  }

  div.content_section {
    margin: 3px 3px 3px 3px;

    background-color: #FFFFFF;

    text-align: left;
  }

  div.content_section_text {
    padding: 4px 8px 4px 8px;

    color: #000000;
    font-size: 100%;
  }

  div.content_section_text pre {
    margin: 8px 0px 8px 0px;
    padding: 8px 8px 8px 8px;

    border-width: 1px;
    border-style: dotted;
    border-color: #000000;

    background-color: #F5F6F7;

    font-style: italic;
  }

  div.content_section_text p {
    margin-bottom: 6px;
  }

  div.content_section_text ul, div.content_section_text li {
    padding: 4px 8px 4px 16px;
  }

  div.section_header {
    padding: 3px 6px 3px 6px;

    background-color: #8E9CB2;

    color: #FFFFFF;
    font-weight: bold;
    font-size: 112%;
    text-align: center;
  }

  div.section_header_red {
    background-color: #CD214F;
  }

  div.section_header_grey {
    background-color: #9F9386;
  }

  .floating_element {
    position: relative;
    float: left;
  }

  div.table_of_contents_item a,
  div.content_section_text a {
    text-decoration: none;
    font-weight: bold;
  }

  div.table_of_contents_item a:link,
  div.table_of_contents_item a:visited,
  div.table_of_contents_item a:active {
    color: #000000;
  }

  div.table_of_contents_item a:hover {
    background-color: #000000;

    color: #FFFFFF;
  }

  div.content_section_text a:link,
  div.content_section_text a:visited,
   div.content_section_text a:active {
    background-color: #DCDFE6;

    color: #000000;
  }

  div.content_section_text a:hover {
    background-color: #000000;

    color: #DCDFE6;
  }

  div.validator {
  }
    </style>
  </head>
  <body>
    <div class="main_page">
      <div class="page_header floating_element">
        <img src="/icons/openlogo-75.png" alt="Debian Logo" class="floating_element"/>
        <span class="floating_element">
          Apache2 Debian Default Page
        </span>
      </div>
<!--      <div class="table_of_contents floating_element">
        <div class="section_header section_header_grey">
          TABLE OF CONTENTS
        </div>
        <div class="table_of_contents_item floating_element">
          <a href="#about">About</a>
        </div>
        <div class="table_of_contents_item floating_element">
          <a href="#changes">Changes</a>
        </div>
        <div class="table_of_contents_item floating_element">
          <a href="#scope">Scope</a>
        </div>
        <div class="table_of_contents_item floating_element">
          <a href="#files">Config files</a>
        </div>
      </div>
-->
      <div class="content_section floating_element">


        <div class="section_header section_header_red">
          <div id="about"></div>
          It works!
        </div>
        <div class="content_section_text">
          <p>
                This is the default welcome page used to test the correct 
                operation of the Apache2 server after installation on Debian systems.
                If you can read this page, it means that the Apache HTTP server installed at
                this site is working properly. You should <b>replace this file</b> (located at
                <tt>/var/www/html/index.html</tt>) before continuing to operate your HTTP server.
          </p>


          <p>
                If you are a normal user of this web site and don't know what this page is
                about, this probably means that the site is currently unavailable due to
                maintenance.
                If the problem persists, please contact the site's administrator.
          </p>

        </div>
        <div class="section_header">
          <div id="changes"></div>
                Configuration Overview
        </div>
        <div class="content_section_text">
          <p>
                Debian's Apache2 default configuration is different from the
                upstream default configuration, and split into several files optimized for
                interaction with Debian tools. The configuration system is
                <b>fully documented in
                /usr/share/doc/apache2/README.Debian.gz</b>. Refer to this for the full
                documentation. Documentation for the web server itself can be
                found by accessing the <a href="/manual">manual</a> if the <tt>apache2-doc</tt>
                package was installed on this server.

          </p>
          <p>
                The configuration layout for an Apache2 web server installation on Debian systems is as follows:
          </p>
          <pre>
/etc/apache2/
|-- apache2.conf
|       `--  ports.conf
|-- mods-enabled
|       |-- *.load
|       `-- *.conf
|-- conf-enabled
|       `-- *.conf
|-- sites-enabled
|       `-- *.conf
          </pre>
          <ul>
                        <li>
                           <tt>apache2.conf</tt> is the main configuration
                           file. It puts the pieces together by including all remaining configuration
                           files when starting up the web server.
                        </li>

                        <li>
                           <tt>ports.conf</tt> is always included from the
                           main configuration file. It is used to determine the listening ports for
                           incoming connections, and this file can be customized anytime.
                        </li>

                        <li>
                           Configuration files in the <tt>mods-enabled/</tt>,
                           <tt>conf-enabled/</tt> and <tt>sites-enabled/</tt> directories contain
                           particular configuration snippets which manage modules, global configuration
                           fragments, or virtual host configurations, respectively.
                        </li>

                        <li>
                           They are activated by symlinking available
                           configuration files from their respective
                           *-available/ counterparts. These should be managed
                           by using our helpers
                           <tt>
                                a2enmod,
                                a2dismod,
                           </tt>
                           <tt>
                                a2ensite,
                                a2dissite,
                            </tt>
                                and
                           <tt>
                                a2enconf,
                                a2disconf
                           </tt>. See their respective man pages for detailed information.
                        </li>

                        <li>
                           The binary is called apache2. Due to the use of
                           environment variables, in the default configuration, apache2 needs to be
                           started/stopped with <tt>/etc/init.d/apache2</tt> or <tt>apache2ctl</tt>.
                           <b>Calling <tt>/usr/bin/apache2</tt> directly will not work</b> with the
                           default configuration.
                        </li>
          </ul>
        </div>

        <div class="section_header">
            <div id="docroot"></div>
                Document Roots
        </div>

        <div class="content_section_text">
            <p>
                By default, Debian does not allow access through the web browser to
                <em>any</em> file apart of those located in <tt>/var/www</tt>,
                <a href="https://httpd.apache.org/docs/2.4/mod/mod_userdir.html" rel="nofollow">public_html</a>
                directories (when enabled) and <tt>/usr/share</tt> (for web
                applications). If your site is using a web document root
                located elsewhere (such as in <tt>/srv</tt>) you may need to whitelist your
                document root directory in <tt>/etc/apache2/apache2.conf</tt>.
            </p>
            <p>
                The default Debian document root is <tt>/var/www/html</tt>. You
                can make your own virtual hosts under /var/www. This is different
                to previous releases which provides better security out of the box.
            </p>
        </div>

        <div class="section_header">
          <div id="bugs"></div>
                Reporting Problems
        </div>
        <div class="content_section_text">
          <p>
                Please use the <tt>reportbug</tt> tool to report bugs in the
                Apache2 package with Debian. However, check <a
                href="https://bugs.debian.org/cgi-bin/pkgreport.cgi?ordering=normal;archive=0;src=apache2;repeatmerged=0"
                rel="nofollow">existing bug reports</a> before reporting a new bug.
          </p>
          <p>
                Please report bugs specific to modules (such as PHP and others)
                to respective packages, not to the web server itself.
          </p>
        </div>




      </div>
    </div>
    <div class="validator">
    </div>

<br>
  </body>
</html>

```
</details>

Eli asennus on onnistunut ongelmitta.

<br>

### Oletussivun muokkaus

Seuraavaksi muutetaan oletussivun sisältöä. Kokeilin alkuun tehdä tehtävänannon mukaan, mutta suomeksi:

```bash
echo "Tämä on uuden web-palvelimeni oletussivu." | sudo tee /var/www/html/index.html
```

Mutta selain näyttää ääkköset virheellisesti:

<p align="center">
  <img width="491" height="174" alt="Näyttökuva 2026-09-02 184711" src="https://github.com/user-attachments/assets/4e46adc8-3d30-438d-a132-8a4407243be7" />
  <br>
  <em>Kuva 3. Ei kelvannu</em>
</p>

<br>

Pakko siis muuttaa se englanninkieliseksi:

```bash
echo "Tally-ho, chaps! This is the default page of my new web server" | sudo tee /var/www/html/index.html
```
<p align="center">
  <img width="581" height="167" alt="image" src="https://github.com/user-attachments/assets/4022eeb4-f026-4190-91e3-a5e67df8a91f" />
  <br>
  <em>Kuva 4. Parempi</em>
</p>

Mitä kyseinen komento sitten tekee? Siinä on oikeastaan kolme eri osaa, joten palastellaan niitä hieman:

echo tulostaa annetun tekstin näytölle:
```bash
echo "Tally-ho, chaps! This is the default page of my new web server"
```

Välissä on pipe, jonka avulla echo-komennon tuottama teksti lähetetään tee-komennolle:
```bash
|
```

Tässä pääkäyttäjän oikeuksilla suoritetaan tee-komento, joka puolestaan lukee syötteen ja kirjoittaa sen tiedostoon. Tiedosto /var/www/html/index.html korvataan uudella sisällöllä:
```bash
sudo tee /var/www/html/index.html
```

Muokkauksessa voidaan käyttää myös muita tapoja, kuten esim. nano-editoria, jolla voi helposti muuttaa sisältöä mieleisekseen:
```bash
sudo nano /var/www/html/index.html
```
<p align="center">
 <img width="727" height="129" alt="image" src="https://github.com/user-attachments/assets/1edc54db-98b2-4764-92de-43043fc32109" />
  <br>
  <em>Kuva 5. Nano-editori</em>
</p>

<br>

Entä miksi seuraava komento ei toimi?
```bash
sudo echo ‘This is…’ > /var/www/html/index.html
```
Vaikka siinä onkin sudo, virhe johtuu siitä, että shell käsittelee uudelleenohjauksen ennen kuin sudo suorittaa komennon. Eli echo ajetaan sudo-oikeuksilla, mutta tiedoston avaaminen kirjoitusta varten tapahtuu normaalin käyttäjän oikeuksilla eikä tavallisella käyttäjällä ei ole kirjoitusoikeutta hakemistoon

<p align="center">
 <img width="571" height="37" alt="image" src="https://github.com/user-attachments/assets/a76a29d3-36f4-4260-9813-7454098f528b" />
  <br>
  <em>Kuva 6. Ja siksi emme voi muokata tekstiä</em>
</p>

<br>

Muokkasin nanolla **/etc/hosts**-tiedostoa ja lisäsin rivin 127.0.0.1 minux.local. Tämän ansiosta käyttöjärjestelmä osaa yhdistää nimen minux.local paikalliseen koneeseen. Pingattu vielä onnistuneesti:

<p align="center">
 <img width="719" height="439" alt="Näyttökuva 2026-09-03 165837" src="https://github.com/user-attachments/assets/3b94b66b-2409-4988-a4d4-352ff31cc23b" />
 <img width="623" height="214" alt="Näyttökuva 2026-09-03 165906" src="https://github.com/user-attachments/assets/0215cfe1-eedf-4349-9e75-35a72e68e66b" />
  <br>
  <em>Kuvat 7 ja 8. hosts-lisäys ja onnistunut pingaus</em>
</p>

<br>

### Asennetaan UFW

Seuraavaksi asennetaan UFW eli uncomplicated firewall. Sallitaan portit 22, 80 ja 443 ja poistetaan nanolla IPv6 käytöstä turhaan häiritsemästä:

<p align="center">
 <img width="597" height="521" alt="image" src="https://github.com/user-attachments/assets/c5a3a52f-60fd-473a-ae49-ebd4f421fd45" />
  <br>
  <em>Kuva 9. UFW-konfiguraatioita</em>
</p>

Testasin UFW-palomuuria estämällä HTTP-portin komennolla:

```bash
sudo ufw deny 80/tcp.
```
Vaikka sääntö näkyi UFW:n tilassa, verkkosivu avautui edelleen osoitteesta http://minux.local. Tämä johtuu siitä, että minux.local on määritelty /etc/hosts-tiedostossa osoitteeseen 127.0.0.1, joka on localhostin loopback-osoite. Loopback-liikennettä ei normaalisti suodateta samalla tavalla kuin ulkoisia verkkoyhteyksiä. Tämän perusteella voidaan päätellä, että UFW estää ulkopuolelta tulevia yhteyksiä porttiin 80, mutta localhostista localhostiin kulkeva liikenne toimii edelleen.

### Luodaan nimipohjainen virtuaalipalvelin

Tässä kohdin luodaan nimipohjainen virtuaalipalvelin hakemistoon:

```bash
mkdir -p ~/public_html/minux
```

Luodaan yksinkertainen index-sivu:

```bash
echo "Tämä on minux.local-sivusto." > ~/public_html/minux/index.html
```
```bash
mkdir -p ~/public_html/minux
```
Ja luodaan myös konfiguraatiotiedosto:

```bash
<VirtualHost *:80>
    ServerName minux.local
    ServerAlias www.minux.local

    DocumentRoot /home/mikko/public_html/minux

    <Directory /home/mikko/public_html/minux>
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error-site1.log
    CustomLog ${APACHE_LOG_DIR}/access-site1.log combined
</VirtualHost>
```

Tallennetaan se ja suoritetaan:

```bash
sudo apachectl configtest
```

<p align="center">
 <img width="724" height="88" alt="image" src="https://github.com/user-attachments/assets/e03eed82-76e5-460a-98de-42b97a58a305" />
  <br>
  <em>Kuva 10. Syntaksi on OK</em>
</p>

<br>

Otetaan sivusto käyttöön:

```bash
sudo a2ensite minux.conf
```
Ja ladataan Apache uudelleen:

```bash
sudo systemctl reload apache2
```

Mutta kun yritän mennä sivulle http://minux.local, ei tämä mennytkään täysin putkeen:

<p align="center">
 <img width="1155" height="353" alt="image" src="https://github.com/user-attachments/assets/bf9bcb1f-89e3-4e84-a49d-cb8bf76fbad6" />
  <br>
  <em>Kuva 11. Ei onnistu - kielletty :(</em>
</p>

<br>

Tarkistetaan error-site1-loki:

```bash
sudo cat /var/log/apache2/error-site1.log
```

<p align="center">
 <img width="794" height="253" alt="image" src="https://github.com/user-attachments/assets/7ffbe155-4acf-4cc8-be0d-f420f81f2640" />
  <br>
  <em>Kuva 12. Lokitiedoston sisältö</em>
</p>

<br>

Syynä oli se, että kotihakemiston käyttöoikeudet estivät Apachea pääsemästä sivuston tiedostoihin. Korjaamalla hakemiston oikeudet komennolla:
```bash
chmod o+x /home/mikko 
```
Apache pystyi lukemaan sivuston tiedostot, minkä jälkeen sivu avautui onnistuneesti osoitteessa http://minux.local.

<p align="center">
 <img width="608" height="195" alt="image" src="https://github.com/user-attachments/assets/9bae4f45-fdb8-461e-a120-022c26fd8b27" />
  <br>
  <em>Kuva 13. Nyt sivu aukeaa, mutta ääkköset on edelleen ongelma</em>
</p>

Ja kun tarkistetaan vielä käyttöloki niin siitä näkee, että statuskoodi on nyt muuttunut:

<p align="center">
<img width="797" height="198" alt="image" src="https://github.com/user-attachments/assets/a374ed92-fdc4-4569-8ea6-6d0e9b9a59f1" />
  <br>
  <em>Kuva 14. 403 > 200</em>
</p>


## Challenge

Seuraavaksi luodaan toinen sivustohakemisto kotihakemistooni:
```bash
mkdir -p ~/public_html-2
```
```bash
echo "Toinen verkkosivu." > ~/public_html-2/index.html
```

Lisätään uusi nimi nanolla /etc/hosts-tiedostoon:

<p align="center">
 <img width="739" height="258" alt="Näyttökuva 2026-09-04 072354" src="https://github.com/user-attachments/assets/ae6b190f-6fc5-4ae2-812f-0685767c96a2" />
  <br>
  <em>Kuva 14. Uusi nimi</em>
</p>

<br>

Luodaan konfiguraatiotiedosto:

```bash
sudo nano /etc/apache2/sites-available/munix.local.conf
```

ja lisätään sisällöksi: 

```bash
<VirtualHost *:80>
    ServerName munix.local
    ServerAlias www.munix.local

    DocumentRoot /home/mikko/public_html-2/munix

    <Directory /home/mikko/public_html-2/munix>
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error-site2.log
    CustomLog ${APACHE_LOG_DIR}/access-site2.log combined
</VirtualHost>
```

<br>

jonka jälkeen tallennetaan konfiguraatiotiedosto.

Nyt otetaan sivusto käyttöön...
```bash
sudo a2ensite munix.local.conf
```
...ladataan Apache uudelleen...
```bash
sudo systemctl reload apache2
```
...ja tarkistetaan määritys, ettei siinä ole virheitä:
```bash
sudo apache2ctl configtest
```

<br>

<p align="center">
 <img width="726" height="107" alt="image" src="https://github.com/user-attachments/assets/0e131bc0-322b-46b6-be12-ca2d42998b94" />
  <br>
  <em>Kuva 15. Syntaksi näyttäisi olevan OK, mutta ongelmia on selvästi jo näkyvissä.</em>
</p>

<br>

Kun kokeilin avata sivua selaimelta, sivu palautti virheen 403 Forbidden. Tutkimalla asetuksia huomasin, että DocumentRoot osoitti hakemistoon /home/mikko/public_html-2/munix, mutta olin unohtanut luoda kyseisen hakemiston aiemmin. Kun hakemisto luotiin ja sivuston tiedostot sijoitettiin siihen seuraavilla komennoilla...

```bash
mkdir ~/public_html-2/munix
```

```bash
mv ~/public_html-2/index.html ~/public_html-2/munix/
```

...sivusto alkoi toimia normaalisti:

<p align="center">
 <img width="694" height="214" alt="image" src="https://github.com/user-attachments/assets/22cabeb1-0a2f-44bf-bcc9-7162b88fa1f7" />
  <br>
  <em>Kuva 16. Virhe korjattu ja kaikki toimii</em>
</p>

## Lähteet

- Heinonen, J. 2026. Apache2. Luettavissa: https://github.com/johannaheinonen/johanna-test-repo/blob/main/module_3.md. Luettu: 1.9.2026
