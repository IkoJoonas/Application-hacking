## Laitteisto

Host: Suoritin: AMD Ryzen 7 1700 (8-Core Processor) RAM: 32 Gt Näytönohjain: 8 Gt Tallennustila: 932 Gt

Guest: Oracle VM VirtualBox 7.2.4

Virtuaalikone: Debian 13.3 Cinnamon

RAM: 4GB

Levytila: 20 GB

CPU: 2

## a)

Aloitin tehtävän lataamalla ezbin-challenges.zip tiedoston Teron sivuilta (https://terokarvinen.com/application-hacking/). 

Latauksen jälkeen purin kansion.

Menin kansiossa passtr sisälle ja suoritin komennon `strings passtr`

<img width="669" height="425" alt="passtr" src="https://github.com/user-attachments/assets/54c464e9-4e97-41f6-97f1-ce33060f0b5f" />

Huomasin, että salasana `sala-hakkeri-321` oli näkyvissä, joten päätin ajaa tiedoston ja kokeilla olisiko tämä oikein.

<img width="925" height="171" alt="passtr2" src="https://github.com/user-attachments/assets/658059ca-0739-4d6e-9212-289bac1469c0" />

Salasana toimi ja myös lippu tuli näkyville.

## b)

Kysyin tekoälyltä apua miten koodi saataisiin obfuskoitua sellaiseen muotoon, että salasanaa olisi vaikeampi löytää ajettaessa `string` komento.

Päädyin yksinkertaiseen ratkaisuun ja muutin koodin seuraavanlaiseksi:

<img width="883" height="693" alt="passtr3" src="https://github.com/user-attachments/assets/4b50446a-b629-45ce-81ba-11dbdad9a22d" />

Koodissa salasanaa ei ole suoraan tallennettu, vaan se on luotu neljästä osasta.

<img width="278" height="87" alt="passtr3 1" src="https://github.com/user-attachments/assets/1471c348-fc51-41ea-858a-81ee152ab8c4" />

Osat yhdistetään `strcpy` ja `strcat` funkioilla luomaan yhtenäinen salasana.

<img width="331" height="73" alt="passtr3 2" src="https://github.com/user-attachments/assets/8621a407-e798-4cdb-87b0-b8dd10ffcaa7" />

Muutoksien jälkeen ajoin komennon `gcc -o passtr passtr.c`

Kokeilin näkyykö salasana selkeästi komennon `strings passtr` tulosteessa.

<img width="894" height="512" alt="passtr4" src="https://github.com/user-attachments/assets/e890a187-1a54-4046-b97d-668aa26e243c" />

Salasana oli nytten vaikeammin erotettavissa.

## c)

Menin kansiossa packd sisälle ja suoritin komennon `strings packd` 

<img width="725" height="38" alt="pack1" src="https://github.com/user-attachments/assets/ff0f9846-9c94-47d2-9ac1-08f82576fe57" />

Sain näkyville `piilos-An` salasanan ja päätin kokeilla tätä samalla tavalla, kuin a-kohdassa.

<img width="720" height="168" alt="pack2 0" src="https://github.com/user-attachments/assets/fc17ff0d-fa4d-4aab-bffd-724003d19cd9" />

Salasana ei jostais syystä toiminutkaan, joten päätin jatkaa strings-komennon tulosteen tarkastelemista.

Huomasin inffo kohdan.

<img width="693" height="21" alt="pack3" src="https://github.com/user-attachments/assets/6c4d1492-2e87-4ca4-9463-689ec94ea4dc" />

Nopealla googlauksella selvisi, että tiedosto oli pakattu UPX-pakkaajalla, joka pienentää tiedostokokoa.

Asensin UPX:n komennolla `sudo apt install upx-ucl`

Asennuksen jälkeen muutin tiedoston takaisin alkuperäiseen muotoon komennolla `upx -d packd`

Suoritin komennon `strings packd` uudestaan ja nyt huomasin eron ensimmäiseen kertaan. Olin saanut pidemmän salasanan näkyville tulosteessa.

<img width="209" height="56" alt="pack4" src="https://github.com/user-attachments/assets/e3ca5579-6f82-461e-a65c-1ae177e1cb5b" />

Kokeilin uutta salasanaa ja se näytti olevan oikea.

<img width="924" height="165" alt="packvika" src="https://github.com/user-attachments/assets/2641fa1f-5790-4691-940b-e3a42a3b3a16" />

## Lähteet

UPX: https://upx.github.io/

https://terokarvinen.com/application-hacking/
