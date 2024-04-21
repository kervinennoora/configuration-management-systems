# h4 - Demoni

**x) Lue ja tiivistä**

**Karvinen 2023:**
- Artikkelissa neuvotaan luomaan kansio, joka kuvaa ajettavan tilan teemaa. Kansioon luodaan init.sls tiedosto. 
- Luomalla tekstitiedostoja, jotka sisältävät haluamasi sisällön voit ajaa tiloja orjilla helposti.
- Tiedostot kirjoitetaan YAMLilla, joten kirjoitusasu ja oikea määrä välilyöntejä on erittäin tärkeää.
- Helppo ajaa orjille state.apply -komennolla.
- Top.sls tiedostot määrää mitkä tilat ajetaan millekkin orjalle.
- Voi ajaa osalle tai kaikille.

**Salt contributors:**
- YAML on merkintäkieli, jolla on monia tehokkaita ominaisuuksia.
- YAML-renderöijän tehtävänä on ottaa YAML-tietorakenne ja kääntää se Pythonin tietorakenteeksi Saltia varten.
- YAML-säännöt:
    - Data on rakennettu avain: arvo -pareihin.
    - Kartoituksissa käytetään kaksoispistettä ja yhtä välilyöntiä (" : ") merkitsemään avain: arvo -pareja.
    - Avainten arvo voi olla monenlaisissa rakenteissa.
    - Kaikki avaimet/ominaisuudet ovat kirjainkoosta riippuvaisia.
    - Tabulaattorit EIVÄT ole sallittuja, käytä VAIN välilyöntejä.
    - Kommentit alkavat risuaidalla “#”.
- YAML koostuu kolmesta eri peruselementtityypistä:
    - Skalaarit(Scalars) - avain: arvo -kartoitukset, joissa arvo voi olla numero, merkkijono tai totuusarvo.
    - Listat(Lists) - avain, jonka jälkeen tulee lista arvoista, joissa jokainen arvo on omalla rivillään ja alkaa kahdella välilyönnillä ja viivalla.
    - Sanakirjat(Dictionaries) - kokoelma avain: arvo -kartoituksia ja listoja.
 - YAML on järjestetty lohkorakenteisiin.
 - Sisennys asettaa kontekstin!
 - Sinun TÄYTYY sisentää ominaisuudet ja lista yhdellä tai useammalla välilyönnillä, mutta kaksi välilyöntiä on standardi.
 - Kun kyse on lista tai sanakirja lohkorakenteesta, osoitetaan jokainen merkintä viivalla ja välilyönnillä "- ".

**Karvinen 2018:**
- Voit hallita suurta määrää demoneja palvelinten hallinnan avulla.
- Pkg-File-Service on yleinen malli tähän: asenna ohjelmisto, korvaa konfiguraatiotiedosto ja lopuksi uudelleenkäynnistä demoni.
- Artikkelissa neuvotaan ensimmäiseksi luomaan SSH tila. Siihen tarkat ohjeet ovat artikkelissa.
- Kun konfiguraatiotiedosto on valmis ajetaan state.aaply -komento orjille.
- Lopuksi täytyy muistaa testata onnistuiko konfiguraatio.
    - Esimerkki komento artikkelista: *nc -vz tero.example.com 8888*.
    - Jos SSH demoni vastaa portilta 8888, konfiguraatio on onnistunut!


## a) Hello SLS!

Aloitin luomalla uuden hakemiston /srv/, jonne loin hakemiston /salt/. Lopuksi tein vielä hakemiston hello, jonne asetin tiedoston init.sls.
Init.sls piti sisällään seuravaavat tiedot:

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/022c8475-6156-4b0b-b31f-09b3604693d8)

Lopuksi ajoin komennon ````sudo salt-call --local state.apply````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/17352a8c-a571-494c-bce4-cc8cb87c3b7b)

Ajoin komennon ````sudo salt-call --local state.apply```` vielä toisenkin kerran, saavuttaakseni idempotentin tilan.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/cfb722f1-6797-4ab4-8bc8-440cfe5d676a)

## b) Top

Loin top.sls tiedoston /srvt/salt hakemistoon. Top.sls tiedoston avulla voin määrittää mitä orjia tila koskee.

Lopuksi ajoin komennon ````sudo salt '*' state.apply````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/aa6f6826-cbe2-4bc0-aa76-f01ebb2345d2)

Sitten siirryin hello hakemistoon ja muokkasin init.sls tiedostoa. Tein tämän siksi, että voin testata muutosta.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/3d05e69b-c117-4878-a49b-d8307847b07e)

Lopuksi ajoin komennon ````sudo salt '*' state.apply````. Muutosta tapahtui. Kuva havainnolistaa näkymää myös orjakoneelta.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/4799c183-00e7-4a76-a7f5-67b31b62d54b)

## c) Apache easy mode

Aloitin luomalla hakemiston /salt/apache/, jonne sijoitin uuden init.sls tiedoston. Init.sls tiedosto sisälti seuraavanlaiset tiedot. 

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/3d80e379-5ffd-4c14-8c8d-feaddf6a1c49)

Siirryin hakemistoon /ect/apache2/sites-available/. Hakemistoon loin tiedoston noora.conf, joka sisälsi seuraavat tiedot. Lopuksi lisäsin noora.conf tiedoston myös hakemistoon /etc/apache2/sites-enabled/.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/e28f3419-d680-47cd-a54f-dffdd91e3198)

Lopuksi ajoin komennon ````sudo salt-call --local --state.output=terse state.apply apache````. Ajoin saman komennon toisenkin kerran saavuttaakseni idempotentin tilan. 

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/1e292b5d-ac50-429e-be6e-fbc9be6b6497)

## d) SHHouto

Menin kansioon /etc/, ja avasin tiedoston *sshd_config*. Lisäsin konfiguraatio tiedostoon portin 1234.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/76d03cb2-e67e-401c-9780-6005160296b4)

Tallensin konfiguraatio tiedoston, jonka jälkeen ajoin komennon ````sudo systemctl restart ssh````. Tämän jälkeen ajoin komennot ````nc -vz localhost 1234```` ja ````nc -vz localhost 22````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/5cb4dacc-6d7a-4ac8-97ba-a16135c06f26)

Lopuksi ajoin komennon ````sudo salt-call --local --state.output=terse state.apply apache````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/365ed175-34dd-47a3-bc03-7de2fda120af)


## References

 Salt Project. s.a. salt.states.file. https://docs.saltproject.io/en/latest/ref/states/all/salt.states.file.html#salt.states.file.keyvalue
 
 Karvinen, T. 2024. Infra as Code - Palvelinten hallinta 2024. https://terokarvinen.com/2024/configuration-management-2024-spring/

 Karvinen, T. 2024. H4 - Demoni. https://terokarvinen.com/2024/configuration-management-2024-spring/#h4-demoni

 Karvinen, T. 2023. Salt Vagrant - automatically provision one master two slaves. https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file

 Salt Project. 2021. Salt overview - Salt user guide. https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml

 Karvinen, T. 2018. Pkg-File-Servoce - Control Daemons with Salt. https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh

 Vivek Gite. 2024. How To Restart SSH Service under Linux. https://www.cyberciti.biz/faq/howto-restart-ssh/

 
