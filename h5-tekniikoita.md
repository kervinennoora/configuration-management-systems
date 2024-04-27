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

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/303e5611-fcd2-4602-b468-6ba564c8cdcd)

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/dff69c2b-be9b-4ad6-993f-d9a1cff01b05)

## e) Komennus

## References

Karvinen, T. 2024. Infa as Code - Palvelinten hallinta 2024. https://terokarvinen.com/2024/configuration-management-2024-spring/

Karvinen, T. 2024. h5 - Tekniikoita. https://terokarvinen.com/2024/configuration-management-2024-spring/#h5-tekniikoita

Seppä, T. 2019. h5 - salt linux tehtävä toni seppä. https://salthomework.wordpress.com/h5/

Karvinen, T. 2021. Run Salt Command Locally. https://terokarvinen.com/2021/salt-run-command-locally/?fromSearch=run%20salt%20command
