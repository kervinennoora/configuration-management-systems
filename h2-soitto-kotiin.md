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


## References
Karvinen, T. 2021. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/

Karvinen, T. 2018. Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux

Karvinen, T. 2014. Hello Salt Infra-as-Code https://terokarvinen.com/2024/hello-salt-infra-as-code/

Karvinen, T. 2024. H2 - Soitto kotiin https://terokarvinen.com/2024/configuration-management-2024-spring/#h2-soitto-kotiin

Karvinen, T. 2006. Raportin kirjoittaminen https://terokarvinen.com/2006/raportin-kirjoittaminen-4/

Karvinen, T. 2024. Infra as Code - Palvelinten hallinta 2024 https://terokarvinen.com/2024/configuration-management-2024-spring/
