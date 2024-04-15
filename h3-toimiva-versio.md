# H3 - Toimiva versio
x) 

**Chacon and Straub 2014:**
- Hajautettu versionhallintajärjestelmä.
- Auttaa hallitsemaan ja seuraamaan muutoksia projekteissa.
- Tallentaa muutokset ja mahdollistaa monien ihmisten toiminnan samassa projektissa.
- Toimii eri tavalla, kuin muut perinteiset versionhallintaohjelmat.
- Git havainnollistaa tiedon sarjana kuvakaappauksia.
- Git ei tallenna tiedostoa uudelleen, vaan vain linkin aiempaan identtiseen tallennettuun tiedostoon.
- Useimmat toiminnot Gitissä tarvitsevat vain paikallisia tiedostoja ja resursseja toimiakseen.
- Kaikki Gitissä tallennettava tieto on tarkistussummattu ennen tallentamista ja sitä viitataan sitten kyseisellä tarkistussummalla.
-  Git käyttää tarkistussummaukseen SHA-1-hajautusfunktiota.
-  Kolme eri tilaa:
    -  *Modified* tarkoittaa, että olet muuttanut tiedostoa, mutta et ole vielä sitonut sitä tietokantaasi.
    -  *Staged* tarkoittaa, että olet merkinnyt muokatun tiedoston sen nykyisessä versiossa menemään seuraavaan commit-kuvakaappaukseesi.
    -  *Committed* tarkoittaa, että tiedot on turvallisesti tallennettu paikalliseen tietokantaasi.


**Gitin käyttö:**
- git add lisää muutetut rivit staged-tilaan.
- git commit sitoo ne paikalliseen tietokantaan.
- git pull hakee uusimmat muutokset etäpalvelimelta ja yhdistää ne paikalliseen haaraan.
- git push  lähettää paikalliset commitit etäpalvelimelle jakamista varten.

**Commits:**
- Sivulla näkyy historia eli loki, kaikista muutoksista mitä Tero Karvinen on tehnyt suolax-varastoonsa.
- Karvinen on mm. lisännyt tilan, joka asentaa lempi sovellukset ja puhdistanut README-tiedoston.

## a) Online

Kuvassa on kaikki tiedot mitä käytin uuden varaston luomiseen.
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/9d4b73d1-a6e8-4af4-91b3-aa382a0a2853)

Uusi varasto näytti tältä:
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/cdc7a9d7-94eb-4f28-bf0c-1fb61b3e9b5c)

## b) Dolly

Aloitin kaiken avaamalla virtuaalikoneeni ja avamalla komennon ````sudo apt-get update````. 
Tämän jälkeen tein uuden kansion *summer*. Seuraavaa komentoa varten tarvitsen online_summer-varaston SSH-linkin.

SSH-linkki sijaitsi täällä:
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/8c2079db-beff-4040-8870-232cbf999ca9)

Suraavaksi ajoin komennon ````git clone git@github.com:kervinennoora/online_summer.git````.
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/7a79fd3d-45b2-4932-a53f-229a696aef2a)

Lopuksi loin sinne uuden tiedoston. Aloitin sen avaamalla tekstieditorin ja luomalla sinne tiedoston summer.md. Kun uusi tiedosto ja muutokset sen sisällä oli tehty, ajoin komennon ````git add . && git commit; git pull && git push````.
Tässä kohtaa on tärkeää lisätä yksi englanninkielinen lause nykyajassa ja määreisessä muodossa.
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/65373d46-1c11-46bc-b999-a2655cdffad2)

Uusi tiedosto oli ilmestynyt varastoon.
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/d804a698-757e-4e82-b550-c9f8bd44a6ff)

## c) Doh!

Aloitin luomalla tiedoston testi.md, sillä tiedoston nimeänine tuolla nimellä on tyhmää.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/0d0bc520-7ce8-4934-ac5f-b93dbc75ac1a)

Tiedosto löytyy nyt Gitistä, mutta sitä ei ole vielä Committattu.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/c91db1f1-c751-4984-bd7f-5976a2970a96)

Seuraavaksi poistin tämän tyhmän muutoksen ajamalla komennon ````git reset --hard````.
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/970f0f1d-ffb1-41db-9b72-4a5cba22e6eb)

Kun seuraavaksi katsoin komennolla ````ls````, mitä kansio sisälsi, tiedosto testi.md oli kadonnut.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/765eeea0-f65a-40f0-8062-b54397414fd2)

## d) Tukki

Aloitin ajamalla komennon ````git log````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/46a1e7a8-5b58-4ee0-9226-8384515633a0)

Kuvassa näkyy online_summer-varaston loki eli historia. Kuvasta ilmenee, että tekijä olen minä. Ihan kuvan alhaalla näkyy ensimmäinen commit, se on siitä kun kopioin varaston Gittiin. Toinen commit kertoo siitä, kun loin tiedoston summer.md. Viimeisenä, muttei vähäisimpänä näkyy, kun poistin tyhmän tiedoston testi.md.

## e) Suolattu rakki

Aloitin luomalla kansion srv, jonne loin kansion salt.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/2f794147-e214-4ba6-a4e6-11cbbd88e01c)

kansioon salt loin tiedoston init.sls.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/d06b5408-f494-4ab0-a238-0424abf67803)

Kun yritin ajaa komentoa, ilmeni ongelma.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/3ea36b90-7c6e-404a-9092-788179be64b1)

Itse en osannut tätä korjata. Joten tulin siihen tulokseen, että palaan aiheeseen myöhemmin, saatuani tähän apua.


## References


Karvinen, T. 2024. Infra as Code - Palvelinten hallinta 2024. https://terokarvinen.com/2024/configuration-management-2024-spring/

Karvinen, T. 2024. H3 - Toimiva versio. https://terokarvinen.com/2024/configuration-management-2024-spring/#h3-toimiva-versio

Git-scm. 2014. Git - Book. https://git-scm.com/book/en/v2

Git-scm. 2014. Git - What is Git? https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F

Karvinen, T. 2024 . Run Salt states from version controlled reposity. https://github.com/terokarvinen/suolax/

Karvinen, T. 2024. Commits · terokarvinen/suolax https://github.com/terokarvinen/suolax/commits/main/

Earth Lab. 2020. First steps with Git. https://www.earthdatascience.org/workshops/intro-version-control-git/basic-git-commands/

Karvinen, T. 2016. Publish Your Project with Github. https://terokarvinen.com/2016/publish-your-project-with-github/?fromSearch=publish%20your%20project%20with%20Github
