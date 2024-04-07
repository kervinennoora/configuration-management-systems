# h2 - Soitto kotiin
x)

**Two Machine Virtual Network With Debian 11 Bullseye and Vagrant** 
- Mahdollistaa kahden koneen virtuaaliverkon luomisen minuuteissa.
- Luo uusi hakemisto ja sinne tyhjä tiedosto *Vagrantfile*.
- Kopioi artikkelissa mainittu konfiguraatio sinne.
- Virtuaalikoneisiin voi ottaa ssh yhteyden.
- Parasta on, että tämä on niin nopeaa ja helppoa, että voit vain tuhota virtuaalikoneesi ja aloittaa alusta.

**Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux**
- Voit hallita tuhansia koneita Saltilla.
- Orjakoneet voivat olla NAT:in, palomuurin takana tai tuntemaatomassa osoitteessa, mutta voit silti hallita niitä.
- Ainoastaan Masterpalvelimen tarvitsee olla julkisella palvelimella ja tunnetulla osoitteella.
- Artikkelissa neuvotaan kuinka Master ja Slave ladataan.
- Kuinka hyväksyä orjan avain masterilla.
- Lopuksi ohjeistetaan kuinka voidaan antaa komentoja orjille.

**Hello Salt Infra-as-Code**
- Artikkelissa luodaan uusi tila, joka varmistaa, että tekstitiedosto on olemassa.
- Ladataan Salt.
- Helpottaakseen työskentelyä käytä Micro-editoria.
- Luodaan uusi kansio Hello-moduulille.
- Kirjoita infraa koodina artikkelin ohjeiden mukaan.
- Testaa ja aja koodi.
- Saata kone idempotenttiin tilaan.

## a) Asenna kaksi virtuaalikonetta samaan verkkoon
Aloitin luomalla uuden kansion tehtava, jonka jälkeen loin kansioon tyhjän tekstitiedoston *Vagrantfile*.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/a764cd55-ee1f-4f02-8e88-35dfb829f5e9)

Tekstitiedostoon lisäsin seuraavan konfiguraation 
````
Vagrant.configure("2") do |config|
		config.vm.box = "debian/bullseye64"
	config.vm.define "t001" do |t001|
		t001.vm.hostname = "t001"
		t001.vm.network "private_network", ip: "192.168.88.101"
	end
	config.vm.define "t002", primary: true do |t002|
		t002.vm.hostname = "t002"
		t002.vm.network "private_network", ip: "192.168.88.102"
	end	
end
````

Tämän jäljeen ajoin komennon ```` vagrant up ```` jonka jälkeen kokeilin toimiiko virtuaalikoneet. 
Virtuaalikoneisiin otin yhteyttä komennoilla `````vagrant ssh t001`````ja ````vagrant ssh t002````

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/4acca994-20b4-409f-a893-e60f5a026d2b)
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/781c5b63-8692-450f-8265-b0e3bc191858)

Lopuksi testasin, että virtuaalikoneet voivat pingata toisiaan. Tähän käytin komentoja ````vagrant@t001$ ping -c 1 198.168.88.102```` ja ````vagrant@t002$ ping -c 1 198.168.88.101````

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/0506d21e-08f0-4375-ba19-c145d3bc587f)
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/67714c7f-a099-4dbe-bab4-3b691776268a)

## b) Asenna Saltin herra-orja arkkitehtuuri toimimaan verkon yli
Ennen herra-orja arkkitehtuurin tekoa päätin, että virtuaalikoneesta t001 tulee herra ja koneesta t002 orja. Lisäksi ennen arkkitehtuurin luomista päivitin molemmat virtuaalikoneet komennolla ````sudo apt-get update````.

Tämän jälkeen virtuaalikoneella ajoin seuraavat komennot 
````master$ sudo apt-get update
master$ sudo apt-get -y install salt-master
master$ hostname -I
````
Otin talteen master-koneen IP-osoitteen, sillä sitä tarvitaan ladatessa orja-konetta.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/08f72de1-cc3f-48b8-9416-640cecda1e15)

Tämän jälkeen siirrtyin virtuaalikoneelle t002 ja tein siitä orjakoneen komennolla ````sudo apt-get -y install salt-minion````. Tämä ei kuitenkaan riitä, sillä orjakoneen täytyy tunnistaa master-kone. Siksi ajoin myös seuraavat komennon.
````
slave$ sudoedit /etc/salt/minion
````
Konfiguraatiotiedostoon lisäsin seuraavat tiedot:

master: 192.168.88.101
id: noora

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/5559f3f2-28b4-46e7-bc3b-9f348919cd4a)

Lopuksi uudelleenkäynnistin orjakoneen komennolla
````slave$ sudo systemctl restart salt-minion.service````.


Tämän jälkeen siirryin taas virtuaalikoneelle t001, jotta voin hyväksyä orja-avaimen master-koneella. Tähän käytin komentoa ````master$ sudo salt-key -A````

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/3259f382-255c-4551-9569-b2a582385e9f)


Lopuksi testasin yhteyttä koneiden välillä. 
````master$ sudo salt '*' cmd.run 'whoami'````

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/1d0c4f07-d129-4b9f-9b38-b956615202d0)

## c) Aja shell-komento orjalla Saltin master-slave yhteyden yli

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/6bbe07d9-6247-4e2b-8619-47b3d1b92ceb)

## d) Aja useita idempotentteja (state.single) komentoja master-slave yhteyden yli

Ensimmäinen state.single komento, jonka ajoin oli ````master$ sudo salt '*' state.single pkg.installed httpie````. Onnekseni se oli idempotentissa tilassa.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/ace88777-9ba9-4c0c-af7f-73b21eeb12ab)

Seuraavaksi kokeilin komentoa ````master$ sudo salt '*' state.single file.managed /tmp/kissa````. Ekalla kerralla se ei ollut idempotentti, mutta ajettuani komennon toisen kerran tilanne oli muuttunut.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/57bfa6e8-ce8a-453d-a5df-f6d1aab65c5e)

## e) Kerää teknistä tietoa orjasta verkon yli
Ennenkuin etsin yksittäisiä tietoja orjakoneesta, testasin saanko koko listan koneen tiedoista esille. Tähän käytin komentoa ````master$ sudo salt '*' grains.items````. 

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/8b531ef2-c6c9-4554-807d-5568c7feffa9)
Kaikki ok, aloin etsimään  tarkkoja tietoja koneesta. 

Aloitin helpolla, halusin tietää mikä käyttöjärjestelmä orjakoneessa on. Tähän käytin komentoa ````master$ sudo salt '*' grains item osfinger````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/b6da1d41-c15d-4d7e-8960-feca898c7421)
Virtuaalikoneen käyttöjärjestelmä on Debian 11.

Seuraavaksi halusin tietää mikä orjakoneen Server ID on. Tämä selvisi komennolla ````master$ sudo salt '*' grains-item server_id````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/f433e117-cdeb-4885-a538-dd4b070df180)
Orjakoneen Server ID oli 1365912336.

## f) Hello, IaC

Ajattelin lähteä tekemään infraa koodina niin, että lopputuloksena olisi se, että orjakoneelle olisi luotu tiedosto hakemistoon.

Aloitin tämän asentamalla micro editorin orjalle. Tämä tapahtui komennolla ````sudo apt-get -y install micro````.

Tämän jälkeen ajoin vielä komennon ````export EDITOR=micro````.


Seuraavaksi loin kansion, jonne kirjoittaa infraa koodina. Tähän käytin komentoa ````sudo mkdir -p /srv/salt/hello/````.

Kansioon loin tiedoston *init.sls*. Ja laitoin sinne seuraavat tiedot ````/tmp/hellonoora:
  file.managed````.
  
![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/de9fca6c-7b89-4ccb-802c-926072ef15b8)

Tämän jälkeen ajoin komennon ````sudo salt-call --local state.apply hello````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/97929d33-c8ec-469e-84ee-d8ff36a4d95c)

Testasin vielä onhan kaikki varmasti niinkuin pitää. Tähän käytin komentoa ````ls /tmp/hellonoora````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/5c5d586f-7007-419d-994b-b224c14f870f)
Jee, kaikki toimii!

Testasin tätä vielä state.single komennolla ````sudo salt-call --local state.single file.manaaged /tmp/hellonoora````.

![image](https://github.com/kervinennoora/configuration-management-systems/assets/165003747/b20654b2-e8d3-4257-b1eb-5a9d1426328b)

## References
Karvinen, T. 2021. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/

Karvinen, T. 2018. Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux

Karvinen, T. 2014. Hello Salt Infra-as-Code https://terokarvinen.com/2024/hello-salt-infra-as-code/

Karvinen, T. 2024. H2 - Soitto kotiin https://terokarvinen.com/2024/configuration-management-2024-spring/#h2-soitto-kotiin

Karvinen, T. 2006. Raportin kirjoittaminen https://terokarvinen.com/2006/raportin-kirjoittaminen-4/

Karvinen, T. 2024. Infra as Code - Palvelinten hallinta 2024 https://terokarvinen.com/2024/configuration-management-2024-spring/
