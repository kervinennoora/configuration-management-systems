# h6 - Benchmark

## lue ja tiivistä
### Windows Package Manager:
**Introduction:**
- Salt tarjoaa Windows-pakettienhallintatyökalun, jonka avulla voi asentaa, päivittää, poistaa ja hallita ohjelmistopaketteja etä-Windows-järjestelmissä.
- Työkalu tarjoaa ohjelmistovaraston ja paketinhallintatyökalun.
    - Vastaavat Linuxissa käytettäviä ```yum``` ja ```apt```.
- Käytä ```pkg.install``` kun haluat asentaa paketin käyttäen käyttöjärjestelmän mukaan määritettyä paketinhallintaa.
- Käytä ```pkg.installed``` -komentoa tarkistaaksesi, onko tietty paketti asennettu minionille.
- Paketinmäärittelytiedostot:
    - ladattavan ohjelmistopaketin koko nimi
    - ohjelmistopaketin versio
    - ohjelmistotiedoston lataussijainti
    - komentorivin kytkin hiljainenasennus ja hiljainenpoisto
    - käytetäänkö Windows ajastinta asentamiseen
- Pakettimäärittelytiedostot voidaan asettaa yhteen tai useampaan Git-repositioon.
- Tämän takia .sls-tiedostoja ei oletuksena jaeta Saltilla.
- Repositio täytyy kloonata ja alustaa.
- Kuka tahansa voi lähettää vetopyyntöjä.
- Paketinmäärittelytiedostoja voidaan hallinta joko Saltilla tai Gitillä.
- Ohjelmistopaketteja voidaan asentaa Git-repositiosta https- tai ftp-url-osoitteista.
    - voidaan asentaa minne tahansa, kuhan sitä voi hallita Saltilla
  
**Install libraries:**
-Jos käytät Salt Windows-paketinhallintaa pakettimäärittelytiedostoihin, jotka ovat Salt Git-repossa, asenna kirjastot ```GitPython``` tai ```pygit2```.

**Populate the local Git repository:**
- Alusta ja kloonaa salt-winrepo-ng-repositorio.
- Masterympäristössä komento ```salt-run winrepo.update_git_repos```.
- Masterittomassa ympäristössä komento ```salt-call --local winrepo.update_git_repos```.

**Update minion database:**
- Aja ```pkg.refresh_db``` kaikilla Windows-minioneilla luodaksesi tietokantaentry jokaiselle pakettimäärittelytiedostolle ja rakentaaksesi pakettitietokannan.
- Masterympäristössä komento ```salt -G 'os:windows' pkg.refresh_db```.
- Masterittomassa ympäristössä komento ```salt-call --local pkg.refresh_db```.

**Install software package:**
- Asenna ohlemistopaketti käyttäen ```pkg.install```.
- Masterympäristössä komento ```salt * pkg.install 'firefox_x64'```.
- Materittomassa ympäristössä komento ```salt-call --local pkg.install "firefox_x64"```.

**Usage:**
- Asennuksen ja alustamisen jälkeen voi käyttää Salt-komentoja Windows-pakettien hallintaan.
  - ```pkg.list_pkgs``` näyttää listan kaikista järjestelmään asennetuista paketeista.
  - ```pkg.lists_available```  näyttää listan tietyn paketin saatavilla olevista versioista.
  - ```pkg.install``` asentaa paketin.
  - ```pkg.remove``` poistaa paketin.

## a) Paketti Windowsia

Aloitin pakettien asennuksen alustamalla ja kloonaamalla reposition. Tähän käytin komentoa ```salt-call --local winrepo.update_git_repos```.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/e45ba6c3-2d81-42ed-b0e8-780bcdf990c4)

Alustamisen ja asentamisen jälkeen loin tietokantaentryn pakettimääräystiedostoille ja samalla rakensin pakettitietokannan. Tähän käytin komentoa ```salt-call --local pkg.refresh_db```.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/cd746e6c-9685-45c7-9555-2dcd4d2ba49b)

Nämä vaiheet toistaakseni asensin paketin. Tunnilla tätä testatessani asensin Adobe Readerin ja VLC media playerin, joten tätä demoa tehdessä päätin asentaa FireFoxin. Tähän käytin komentoa ```salt-call --local pkg.install "firefox_x64"```.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/01f4b26c-cc64-4a8a-83a1-2416dc4fac9f)

Lopuksi ajoin vielä komennon ```salt-call --local state.single pkg.installed "firefox_x64"```. Tällä varmistin asennuksen onnistumisen ja saavutin idempotentin tilan.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/281018af-3185-4d58-a483-492701aae7c8)

## b) Benchmark

**Krakau, Essi:**
 
Ensimmäinen arvioitava työ on Krakaun vuonna 2023 tekemä kurssitehtävä h7 - miniprojekti. Tehtävä antaa hyvän perus kuvan kurssin tärkeimmistä asioista. Siinä ilmenee idempotentti, infra koodina ja yksi totuus, kurssin pyhäkolminaisuus. Tehtävä alkaa ihan kurssin alussa opituista ruohonjuuritason asioista ja etenee loppukurssilla opittuihin skirpteihin ja niiden ajamiseen. Tehtävä on mielestäni siitä hyvä, ettei se oikein ole riippuvainen mistään, joten ohjeita seuraamalla voit suorittaa itse tehtävän täysin samalla tavalla. Tehtävä on oiva tapa näyttää mitä kaikkea Saltilla voi saada aikaan.

 **Seppä, Toni:**

Vuonna 2019 tekemässään projektissaan Seppä  loi salt moduulin, joka asentaa työaseman ohjelmat, konfiguroi ohjelmien oletus asetukset määrittämilläni asetuksilla sekä loi virtuaalisia minion orjia vagrantilla useita kappaleita. Tehtävä on Windows 10 ympäristössä ja Xubuntu ympäristössä. Tehtävä on mielestä todella oivallinen näyttääkseen kurssilla käsiteltävät aiheet. Tehtävässä hyödynnetään Salttia kaikilla tavoin mitä kurssilla meille opetetaan. Mielestäni tehtävässä on myös todella paljon soveltamista, joka kertoo tekijän ammattitiedosta. Näkisin, että tämän projektin asioita hyödynnetään myös työelämässä.

**Valkamo, Tuomas:**

Valkamon vuonna 2022 tekemässä projektissa luotiin oma Salt moduuli. Projektin ideana oli luoda moduuli, joka asentaa kaikki perusohjelmat, joita Valkamo haluisi uudelle virtuaalikoneelle. Tehtävän ohjeilla voit luoda uuden virtuaalikoneen esimerkiksi Vagrantin avulla, lisätä moduulin siihen ja päästä nopeasti käyntiin. Näin voi hallita useita kehityskoneita yhdestä paikasta. Kuten aiemmat arvioimani kussrityöt tämä on erinomainen esimerkki kurssilla opistuista asioista ja niiden hyödyntämisestä sekä soveltamisesta. Tehtävän lopussa ilmeni pieni bugi, jota Valkamo ei lähtenyt korjaamaan, sillä oli itse tyytyväinen raporttiinsa.

## c) Testbench



## d) Viisi ideaa


## References
Karvinen, T. 2024. Infra as Code - Palvelinten hallinta 2024. https://terokarvinen.com/2024/configuration-management-2024-spring/

Karvinen, T. 2024. H6 Benchmark. https://terokarvinen.com/2024/configuration-management-2024-spring/#h6-benchmark

Salt Project. 2024. Windows Package Manager. https://docs.saltproject.io/en/latest/topics/windows/windows-package-manager.html

Krakau, E. 2023. h7-miniprojekti.md. https://github.com/esskra/palvelinten_hallinta/blob/main/h7-miniprojekti.md

Seppä, T. 2019. Projektityö. https://salthomework.wordpress.com/projektityo/

Seppä, T. 2019. projectwork. https://github.com/tontsa00/projectwork

Valkamo, T. 2022. How to Create Your Own Salt Module. https://tuomasvalkamo.com/how-to-create-your-own-salt-module/

Valkamo, T. 2022. starter-module. https://github.com/tuomasvalkamo/starter-module
