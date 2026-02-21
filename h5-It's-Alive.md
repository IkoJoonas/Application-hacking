## Laitteisto

Host: Suoritin: AMD Ryzen 7 1700 (8-Core Processor) RAM: 32 Gt Näytönohjain: 8 Gt Tallennustila: 932 Gt

Guest: Oracle VM VirtualBox 7.2.4

Virtuaalikone: Debian 13.3 Cinnamon

RAM: 4GB

Levytila: 20 GB

CPU: 2

## Lab0

Aloitin lataamalla Lab0 Moodlesta ja purin kansion.

Ajoin ohjelman.

<img width="697" height="125" alt="lab0tokavika" src="https://github.com/user-attachments/assets/6501db48-2bdb-4e12-bbbb-24f237c3f78a" />

Suoritin komennon `gcc buggy_program.c -g  -Wall -Werror -o main` ja aloin tutkimaan koodia GNU Debuggerissa.

Käytin komentoja: `break main`, 

<img width="498" height="41" alt="lab02" src="https://github.com/user-attachments/assets/d6ce85f5-d39e-4b62-af79-fea3654d1537" />

`run`, 

<img width="720" height="127" alt="lab03" src="https://github.com/user-attachments/assets/67963fcd-e3d0-4c11-a235-1eb11399452b" />

`next`, 

<img width="550" height="39" alt="lab04" src="https://github.com/user-attachments/assets/255c91cf-6e0c-4e14-9740-4e161cd76266" />

ja `step` 

<img width="785" height="56" alt="lab05" src="https://github.com/user-attachments/assets/dd6c401b-de14-497a-8d1d-c9e36cce32c2" />

Numeroiden tulostus sekoaa 5. jälkeen

Korjaaminen oli onneksi helppo, muutin koodista kohtaa `for (int = 0; i <= size; i++)` muotoon `for (int = 0; i < size; i++)`

Tallensin muutokset ja ajoin ohjelman uudestaan.

<img width="701" height="113" alt="lab0vika" src="https://github.com/user-attachments/assets/f88a039e-f04f-425e-9a50-da3299ab1824" />

Nyt toimii oikein.

## Lab1

Aloitin samalla lähestymisellä, kuin Lab0

<img width="631" height="681" alt="lab1" src="https://github.com/user-attachments/assets/9f56fcf6-27d3-455c-a3cd-f9b4679308c7" />

Kiinnitin huomiota tähän.

<img width="478" height="126" alt="lab1 1" src="https://github.com/user-attachments/assets/2dcbf342-fed0-49f5-a457-072fcef1736b" />

Ohjelman rivin 18. viittaa rivin 14. `Null` kohtaan. <img width="297" height="25" alt="lab1null" src="https://github.com/user-attachments/assets/2db675b3-bb58-4f1a-867a-055a8ec0e7ae" />

Tein tähän muutoksen vaihtamalla `Null` tilalle `fixed`.

<img width="744" height="509" alt="lab1valmis" src="https://github.com/user-attachments/assets/ed17eb38-30ca-4bec-bb70-f45b28d54374" />

Tallensin muutokset ja kokeilin ajaa uudestaan.

<img width="685" height="57" alt="lab1syöte" src="https://github.com/user-attachments/assets/5b98cfe0-07c2-40c3-8a95-b141cf6972c4" />

Näyttäisi toimivan ja "Segmentation fault" poistui.

`Fixed` korjaus toimii, koska alkuperäinen `NULL` oli pelkkä merkkijonoliteraali eikä oikea NULL-osoitin, jolloin ohjelma ei toiminut odotetulla tavalla. Muokkaamalla varmistin, että osoitin osoittaa tunnettuun muistialueeseen, jolloin print_scrambled funktio pystyy käymään merkkijonon läpi.

## Lab2 Salasanan ja lipun löytäminen

Aloitin lähestymisen käyttämällä komentoa `info functions`.

<img width="401" height="362" alt="lab2 0" src="https://github.com/user-attachments/assets/356dae28-ae9f-4323-9709-1f754f27f674" />

Huomasin kohdan `check_password`, tästä ajoin komennon `disas check_password`.

<img width="493" height="73" alt="lab2 1" src="https://github.com/user-attachments/assets/ee4d458a-3b8e-441f-8176-55690f21a7ef" />

Tämä ei auttanut eteenpäin, koska oli tyhjä. Seuraavaksi kokeilin `disas main`.

<img width="691" height="695" alt="lab2 2" src="https://github.com/user-attachments/assets/d90c10b7-c83a-402e-a57a-fc3e37491a10" />

En saanut tulosteesta juurikaan koppia, joten laitoin kaiken Copilottiin. Neuvona oli käyttää komentoa `disas mAsdf3a`.

<img width="616" height="671" alt="lab2 3" src="https://github.com/user-attachments/assets/0f0de0cf-fe06-4185-a450-0c9354f0b198" />

Tämän tulosteen laitoin myös kokonaan Copilottiin, joka teki kaikki analysoinnit ja salasananmuutoksen antamalla vastaukseksi `dgOMm-x1`. Kokeilin tätä.

<img width="634" height="163" alt="lab2 4" src="https://github.com/user-attachments/assets/f934a3d6-2300-462c-834d-a146b47fedff" />

Salasana oli oikein ja sain lipun näkyville.

## Lähteet

Terokarvinen.com. Application Hacking: https://terokarvinen.com/application-hacking/#laksyt

Käytin Copilotia koodin ymmärtämiseen
