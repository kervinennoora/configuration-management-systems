# H1 - Viisikko

x) 

  **Run Salt Command  Locally:**
  - Voit ajaa Salt komentoja paikallisesti ja nähdä tiedot välittömästi.
  - Samat Salt komennot toimii Linuxissa ja Windowsissa.
  - Tärkeimmät tilafunktiot ovat pkg, file, service, user ja cmd.
  - Käytetään yleensä hallitsemaan suuria määriä orjakoneita verkossa.
  - Loput artikkelista asennusohjeita.

  **Create a Web Page Using Github:**
  - Aloittelija ystävällinen artikkeli Github-sivujen perustamiseen.
  - Ensin kirjaudutaan Githubiin ja sitten luodaan uusi reposity.
  - Reposityn täytyy olla:
    - julkinen
    - sitä täytyy kuvata yhdellä lauseella englanniksi
    - README file, tai muuten tulevaisuudessa tulee ongelmia
    - GNU General Public License version 3
  - Reposityyn luodaan uusi tiedosto, artikkelissa kerrotaan asettelumahdollisuuksista.
  - Tiedosto tallennetaan painamalla *Commit new file*.

  **Raportin kirjoittaminen:**
  - Hyvä raportti on toistettava; Raportin ohjeilla täytyy pystyä toistaa sama tulos.
  - Raportoi myös ympäristöstä.
  - Hyvä raportti on täsmällinen; mitä teit ja kuinka? Paljon meni aikaa ja miten tehtävä sujui.
  - Hyvä raportti on helppolukuinen; väliotsikot, oikeinkirjoitus, mahdollinen tiivistelmä.
  - Hyvä raportti viittaa lähteisiin!
  - Hyvässä raportissa ei sepitetä ja tekstiä tuotetaan vain oikeiden testien pohjalta.
  - Hyvässä raportissa ei plagioida.


a) **Hello Windows Salt World!**

Avasin koneellani Windows PowerShellin järjestelmän valvojana ja ajoin $ salt-call --version 

Kyseinen komento kysyy mikä versio Saltista on asennettuna koneelle, samalla tämä todisti, että Salt on asennettuna koneelleni.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/0c237813-efd5-45d1-ba1e-b1c3d333db21)

b) **Hello Vagrant!**

Päästäkseni käsiin Vagrantiin täytyi minun ensin matkustaa PowerShellissä oikeaan hakemistoon. Matkustin hakemistosta noora hakemistoon Windows ja siellä kansioon system32. Ajoin seuraavaksi komennot $ Vagrant up $ Vagrant ssh

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/aeedd38f-4f70-405c-a86a-4d7997e59f78)

c) **Tee Vagrantilla uusi Linux-virtuaalikone**

Tässä välissä vaihdoin koneellani eri asemalle, jossa on paljon enemmän tilaa tehtävien suorittamiseen. Uudella asemalla ajoin komennot $ vagrant init debian/bullseye64 $ vagrant up $ vagrant ssh

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/4e322b60-f53f-4c09-9258-a02cde44a946)

Avaamalla Oracle VM VirtualBox Managerin, pystyin todistamaan, että uusi virtuaalikone oli luotu ja se oli käynnissä.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/ca78a158-17f7-455c-9de6-106abfd78ec5)

c.a) **Asenna Salt Linuxille**

Otin ssh yhteyden uuteen virtuaalikoneeseeni ja aloitan saltin asennuksen komennoilla $ sudo apt-get update $ sudo apt-get -y install salt-minion

Asennuksen jälkeen tarkistin Saltin version ja samalla varmistin onnistuihan sen asennus virtuaalikoneelleni.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/62e23a50-8c13-46d6-bbf2-b5b0edc6ba47)

c.b) **Viisi tärkeintä**

Aloitin tilafunktiolla pkg. Tilafunktio pkg raportoi hetkessä sovellukseen liittyviä tietoja. Aloitin testin komennolla $ sudo salt-call --local -l info state.single pkg.installed tree

Komennolla käsketään, että tree täytyy olla asennettuna koneelle. Päästäkseen kyseiseen tilaan, Salt asensi treen virtuaalikoneelle. 

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/6e66a191-ad43-49cd-a8fa-6013ad8e4100)

Seuraavaksi siirryin tilafunktioon file, joka raportoi tiedostoihin liittyviä tietoja. Testakseni tätä tilafunktiota ajoin komennon $ sudo salt-call --local -l info state.single file.managed /tmp/kissa

Komento antaa Saltille käskyn, jonka mukaan kansiossa tmp täytyy olla tiedosto nimeltään kissa. Koska tiedostoa kissa ei ollut olemassa, saavuttaakseen halutun tilan, Salt loi sinne kyseisen tiedoston.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/7a58bb84-1c15-4655-8a15-3c8e9188d844)

Tilafunktio service raportoi demonien tilasta. Sen avulla voi päättää onko jonkin demoni toiminnassa vai ei. Aloitin tilafunktion testaamisen komennolla $ sudo salt-call --local -l info state.single service.running apache2 enable=True

Komento antaa Saltille käskyn siitä, että Apache2 täytyy olla toiminassa.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/161a1ec3-43c5-4401-a92e-1748e2c6f64f)
Syy miksi komennon ajaminen ei onnistunut oli se, etten ole asentanut Apachea virtuaalikoneelleni.

User tilafunktio raportoi siitä onko kyseinen käyttäjä olemassa. Testasin tätä tilafunktiota komennolla $ sudo salt-call --local -l info state.single user.present noora

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/d9c192fe-5af9-4302-8ad2-1d301af13c35)

Savuttaakseen halutun tilan, virtuaalikoneelle ilmestyi käyttäjä noora. Jos taas haluaisimme, että koneella ei olisi käyttäjää noora voisimme kokeilla komentoa $ sudo salt-call --local -l info state.single user.absent noora

Viimeisenä on tilafunktio cmd. Kyseinen tilafunktio koskee käskyjä. Sen avulla voidaan ajaa monia käskyjä samaan aikaan. Testataan tilafunktiota komennolla $ sudo salt-call --local -l info state.single cmd.run 'touch /tmp/koira'

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/02a0e404-b483-4aa0-80b2-8aa427e887f3)

Komentoi loi uuden tiedoston nimeltään koira, mutta mielestäni olisi helpompaa vain käyttää tilafuktiota file.

d) **Idempotentti**

Idempotentti kertoo harmoonisesta tilasta. Idempotentti ilmenee kun annamme Saltissa, jonkin komennon ja savuttaakseen kyseistä tilaa, ei tarvitse tehdä muutoksia. Ajoin aikaisemmin Salt-komennon, jonka mukaan virtuaalikoneella kuului olla käyttäjä noora. Jos ajan saman komennon uudelleen, virtuaalikone saavuttaa idemponetin. 

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/8de13b92-a4d6-4c2d-a2ae-67a0a012c64f)

Testasin tätä vielä uudelleen. Tällä kertaa ajoin uudelleen komennon $ sudo salt-call --local -l info state.single file.managed /tmp/kissa

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/87aa6ec0-e444-408b-9f3c-fc2faeb4a9dc)
Tässäkin tilanteessa ilmenee idempotenssi, sillä muutosta ei tarvinnut tapahtua. Saavutin harmoonisen tilan.

e) **Tietoa koneesta**

Etsitään virtuaalikoneen tietoja hyödyntäen komentoa $ sudo salt-call --local grains.items
Komento avaa ison listan koneen eri piirteitä ja tietoja. Valitsin niistä kolme kaikista mielenkiintoisinta ja tutkin niitä tarkemmin.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/4c21b973-74f3-43ce-8781-d2a3c4247d5f)
Ajoin komennon $ sudo salt-call --local grains.item ip6_interfaces
Sen sijaan, että avaisimme kokonaisen listan koneen eri piirteistä, voimme kysyä niistä yksittäin. Kyseinen komento kysyi virtuaalikoneen ipv6-liittymistä.
Seuraavaksi halusin tietoa koneen localhostista, joten ajoin komennon $ sudo salt-call -local grains.item localhost

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/ff5f8e1f-69f1-4020-ac83-383e274f7bd6)
Komento kertoi, että koneen localhost on bullseye.

Sitten minua kiinnosti montako CPU:ta virtuaalikoneessa on, joten esitin komennon $ sudo salt-call --local grains.item num_cpus

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/609b1bd0-53a8-4e78-9d56-e912218c1e0a)
Sain selville, että koneessa on kaksi CPU:ta.

Lopuksi ajoin komennon $ sudo salt-call --local grains.item osfinger virtual

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/48bd2885-efd4-497f-9524-ff5628370e7c)

Osfinger kertoo virtuaalikoneen käyttöjärjestelmän ja virtual kertoo onko kyseessä fyysinen kone vai virtuaalikone.
## References
Karvinen, T. 2023: Run Salt Command Locally https://terokarvinen.com/2021/salt-run-command-locally/

Karvinen, T. 2023: Create a Web Page Using Github https://terokarvinen.com/2023/create-a-web-page-using-github/

Karvinen, T. 2023: Raportin kirjoittaminen https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/

Karvinen, T. 2024: H1 - Viisikko https://terokarvinen.com/2024/configuration-management-2024-spring/#h1-viisikko

Karvinen, T. 2024: Inra as Code - Palvelinten hallinta 2024 https://terokarvinen.com/2024/configuration-management-2024-spring/
