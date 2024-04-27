# h5 - Tekniikoita

## x) Lue ja tiivistä

**h5 - salt linux tehtävä Toni Seppä:**
- Sepän tehtävän a-osan ideana oli tehdä Salt-minion orja Windows käyttöjärjestelmällä.
- Seppä asensi Salt-minion ohjelman koneelle, ohjelmaa asentaessa ilmeni, että myös VC_Redist_2015 ohjelman täytyi olla asennettu.
- Asennuksen jälkeen Seppa testasi master-koneellaan, löytyykö orjakone. Tätä hän testasi ````sudo salt-key```` komennolla.
- Lopuksi hän testasi yhteyttä antamalla orjakoneelle komennon ````sudo salt ‘tontsa00 salt-minion’ grains.items````.
- Tehtävän b-osassa oli ideana säätää Windows konetta, ````sudo salt-call --local```` komennoilla.
- Seppä aloitti tehtävän avaamalla PowerShell ohjelman.
- Salt kansiossaan Seppä kokeili komentoa ````salt-call –local system.set_computer_desc````.
- Tehtävän osassa c, oli ideana muutta jotain tietokoneen asetusta Saltin avulla. Seppä muutti koneensa kellonaikaa.
- Tehtävän d-osa oli jonkinlainen tehtävän varaus, jota ei tarvinnut dokumentoida.
- Tehtävän viimeisessä osassa, joka oli ideana asentaa Chocolatey-varasto Windows-koneelle ja suoritaa Saltin tila, joka asensi useita ohjelmia kyseiseltä varastolta.

## a) Asenna Salt Windowsille tai Macille


## References

Karvinen, T. 2024. Infa as Code - Palvelinten hallinta 2024. https://terokarvinen.com/2024/configuration-management-2024-spring/

Karvinen, T. 2024. h5 - Tekniikoita. https://terokarvinen.com/2024/configuration-management-2024-spring/#h5-tekniikoita

Seppä, T. 2019. h5 - salt linux tehtävä toni seppä. https://salthomework.wordpress.com/h5/
