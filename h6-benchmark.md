# h6 - Benchmark

## lue ja tiivistä
### Windows Package Manager:
**Introduction:**
- Salt tarjoaa Windows-pakettienhallintatyökalun, jonka avulla voi asentaa, päivittää, poistaa ja hallita ohjelmistopaketteja etä-Windows-järjestelmissä.
- Työkalu tarjoaa ohjelmistovaraston ja paketinhallintatyökalun.
    - Vastaavat Linuxissa käytettäviä ```yum``` ja ```apt```.
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

## References
Karvinen, T. 2024. Infra as Code - Palvelinten hallinta 2024. https://terokarvinen.com/2024/configuration-management-2024-spring/

Karvinen, T. 2024. H6 Benchmark. https://terokarvinen.com/2024/configuration-management-2024-spring/#h6-benchmark

Salt Project. 2024. Windows Package Manager. https://docs.saltproject.io/en/latest/topics/windows/windows-package-manager.html
