# h5 - Tekniikoita

## x) Lue ja tiivistä

**h5 - salt linux tehtävä Toni Seppä:**
- Sepän tehtävän a-osan ideana oli tehdä Salt-minion orja Windows käyttöjärjestelmällä.
- Seppä asensi Salt-minion ohjelman koneelle, ohjelmaa asentaessa ilmeni, että myös VC_Redist_2015 ohjelman täytyi olla asennettu.
- Asennuksen jälkeen Seppa testasi master-koneellaan, löytyykö orjakone. Tätä hän testasi ````sudo salt-key```` komennolla.
- Lopuksi hän testasi yhteyttä antamalla orjakoneelle komennon ````sudo salt ‘tontsa00 salt-minion’ grains.items````.
- Tehtävän b-osassa oli ideana säätää Windows konetta, ````sudo salt-call --local```` komennoilla.
- Seppä aloitti tehtävän avaamalla PowerShell ohjelman.
- Salt kansiossaan Seppä kokeili komentoa ````sudo salt-call –local system.set_computer_desc````.
- Tehtävän osassa c, oli ideana muutta jotain tietokoneen asetusta Saltin avulla. Seppä muutti koneensa kellonaikaa.
- Tehtävän d-osa oli jonkinlainen tehtävän varaus, jota ei tarvinnut dokumentoida.
- Tehtävän viimeisessä osassa, joka oli ideana asentaa Chocolatey-varasto Windows-koneelle ja suoritaa Saltin tila, joka asensi useita ohjelmia kyseiseltä varastolta.

## a) Asenna Salt Windowsille tai Macille

Olin asentanut Saltin omalle koneelleni jo aikaisemmin, joten tässä osassa tehtävää todistin Saltin olemassa olon. Tein sen ajamalla komennon ````salt-call --local -l info state.single user.present noora````.
Komento meni läpi, eli asennus on onnistunut ja Salt toimii!

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/02011df8-e6f6-463a-b3c0-262fda26363d)

## b) Kerää Windows- tai Mac-koneesta tietoa

Ensimmäinen grains.items komento jonka ajoin oli ````salt-call --local grains.item osfinger ipv4````. Tämä komento kertoi minulle koneeni käyttöjärjestelmän (Windows 11) ja IPv4-osoitteen. Osoite 10.213.104.6 on Wireless LAN adapter WLAN IP-osoite. Osoiteen 127.0.0.1 lähdettä, en valitettavasti löytänyt. Osoite 192.168.56.1 on Ethernet adapter Ethernet 2 IP-osoite. 192.168.88.1 on Ethernet adapter Ethernet 3 IP-osoite.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/32e4a1e4-c107-4630-839f-487269af48a2)

Toinen ajamani komento oli ````salt-call --local grains.item cpu_model cpuarch````. Sain selville, että koneeni CPU on mallia AMD Athlon Silver 3050U with Radeon Graphics ja CPU:n arkkitehtuuri on AMD64.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/62cc8230-9d02-4940-bc7c-b78d34a737a9)

Kolmas ja viimeinen ajamani komento oli ````salt-call --local grains.item username virtual````. Käyttäjänimeni on KANNETTAVANOORA/noora. Virtual kertoo sen onko kone fyysinen vai virtuaalinen. Sillä kyseessä on fyysinen kone, parametrin virtual arvo on physical.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/a85fffb4-fb32-44c6-9ce7-5696d62c44eb)

## c) Kokeile Saltin file -toimintoa Windowsilla tai Macilla

Testasin Saltin file -toimintoa luomalla tiedoston moikkanoora, joka sisälsi tekstin "Tanaan lauantaina 27.4.2024 on koirien keppinayttely :) <3". Tähän käytimn komentoa ```` salt-call --local -l info state.single file.managed C:/Windows/Temp/moikkanoora contents="Tanaan lauantaina 27.4.2024 on koirien keppinayttely :) <3"````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/f8f46531-cf1c-4c50-9c57-c6edcd35a755)

Toistin saman komennon vielä toisen kerran, saavuttaakseni idempotentin tilan.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/db7212cd-fcc8-4c40-89a0-d5bb638a7797)

Sitten siirryin ````C:/Windows/Temp```` kansioon ja tarkistin toiminnon varmasti toimineen. Kansiosta löytyi tiedosto moikkanoora ja se sisälsi tarvitsemani tiedot.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/1e380ec8-b8c9-4765-8b71-b48de69c61c8)

## d) CSI Kerava
Avasin virtuaalikoneeni, jossa ensin kotihakemistossa ja sen jälkeen /etc/ kansiossa ajoin komennon ````find -printf '%T+ %p\n'|sort````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/303e5611-fcd2-4602-b468-6ba564c8cdcd)

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/dff69c2b-be9b-4ad6-993f-d9a1cff01b05)

Find on komentoriviohjelma, joka etsii yhdestä tai useammasta hakemistorakenteesta tiedostoja käyttäjän määrittelemien kriteerien perusteella ja suorittaa jonkin toiminnon jokaiselle löydetylle tiedostolle. 
*-printf '%T+ %p\n' |sort* on argumentti *find* -käskylle. Se käskee ohjelman find tulostamaan löydetyn tiedoston aikaleiman (&T+) sekä polun (%p). Näiden jälkeen tulee rivinvaihto (/n). Putken jälkeinen parametri *sort* on komento, joka oletuksena järjestää syötelinjat aakkosjärjestyksessä.
## e) Komennus
Aloitin tehtävän siirtymällä kansioon /usr/local/bin. Tämän jälkeen loin sinne skriptitiedoston nimeltä *komento.sh*.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/22549e45-a179-40fd-a09b-1a9f85a25f90)

Tätä tehtävää varten halusin tehdä simppelin skriptitiedoston, joka asentaa koneelle lempisovellukseni cowsayn. Skriptitiedosto sisälti seuraavat tiedot:

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/f65d9cc2-aa79-4283-9239-f4199fa4147c)

Muokkasin skriptitiedoston oikeuksia komennolla ````sudo chmod +x komento.sh````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/c7581a16-44b6-4b62-8d4b-93bd4947b074)

Lopuksi ajoin skriptin masterikoneellani. Omaksi ilokseni se toimi!

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/4d6403ea-41fb-4c9f-b730-744de801526b)

Halusin kuitenkin varmistaa skriptin toimivuuden oikeasti, joten poistin cowsayn virtuaalikoneeltani ja ajoin skriptini uudelleen.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/29146869-dd98-4003-ae78-b9c5404cf2b0)
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/cda55c61-7c3d-46bd-8733-6f81d4dfb760)

Olin iloinen, että skriptini toimi ja siirryin tehtävässä seuraavaan osioon.

Avasin masterikoneellani hakemiston ````/srv/salt/```` ja loin sinne uuden hakemiston nimeltään *komento*. Siirryin uuden hakemiston sisään ja kopioin skriptitiedoston sinne komennolla ````cp /usr/local/bin/komento.sh /srv/salt/komento````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/f90a2093-16b6-4ee3-aea9-f095874cbfb7)

Tämän jälkeen loin uuden tiedoston nimeltään *komento* samaan kansioon. Tämä tiedosto sisälsi täysin samat tiedot kuin skriptitiedostokin, mutta tämä tiedosto oli tallennettu ilman .sh päätettä. 

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/da2a4899-8d43-4e4d-b47d-0bcb1b2f93d8)
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/922caaff-cb79-47cd-bc60-f211ac2c2112)

Lopuksi loin vielä init.sls tiedoston komennolla ````micro init.sls````. Tiedosto piti sisällään seuraavat tiedot:

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/b5d3a187-ca78-438f-85af-86a939cc6da9)

Seuraava askeleeni oli ajaa tila orjakoneellani. Tämän tein komennolla ````sudo salt '*' state.apply komento````. Ilokseni kaikki meni onnistuneesti, joten ajoin saman komennon vielä kertaalleen saavuttaakseni idempotentin tilan.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/e6648e26-543e-44a9-941f-55bc315b5a66)

Nyt kun tila oli ajettu onnistuneesti, oli aika ajaa itse skripti. Tähän käytin komentoa ````sudo salt '*' cmd.run komento````. 

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/30b1d54f-0cbc-474c-827d-d18bf8602dd8)

Viimeisenä avasin orjakoneeni ja kokeilin toimiiko cowsay. Sehän toimi eli tehtävä oli suoritettu onnistuneesti.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/8352d9bf-33e8-4a7d-bfd5-b76db66e38d8)


## References

Karvinen, T. 2024. Infa as Code - Palvelinten hallinta 2024. https://terokarvinen.com/2024/configuration-management-2024-spring/

Karvinen, T. 2024. h5 - Tekniikoita. https://terokarvinen.com/2024/configuration-management-2024-spring/#h5-tekniikoita

Seppä, T. 2019. h5 - salt linux tehtävä toni seppä. https://salthomework.wordpress.com/h5/

Karvinen, T. 2021. Run Salt Command Locally. https://terokarvinen.com/2021/salt-run-command-locally/?fromSearch=run%20salt%20command
