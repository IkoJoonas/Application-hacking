## Laitteisto

Host: Suoritin: AMD Ryzen 7 1700 (8-Core Processor) RAM: 32 Gt Näytönohjain: 8 Gt Tallennustila: 932 Gt

Guest: Oracle VM VirtualBox 7.2.4

Virtuaalikone: Debian 13.3 Cinnamon

RAM: 4GB

Levytila: 20 GB

CPU: 2

## x)

-

## a) 

Aloitin Ghidran asentamisen käyttämällä `sudo apt install openjdk-21-jdk` komentoa. Tämän jälkeen menin [Ghidran Github](https://github.com/NationalSecurityAgency/ghidra/releases) sivulle ja latasin 12.0.1 version. Purin kansion ja käynnistin sovelluksen.

<img width="802" height="611" alt="ghidra" src="https://github.com/user-attachments/assets/0807d309-72e9-467a-a346-18ab121466e4" />

## b) 

Tarkoituksena oli käänteismallintaa packd-binääri C-kielelle Ghidran avulla, etsiä pääohjelma, antaa muuttujille kuvaavat nimet, selittää ohjelman toiminta ja ratkaista binääri ilman, että katsoo alkuperäistä lähdekoodia.

Avasin Ghidran ja loin uuden projektin, jonne importtasin packd tiedoston ja auto analysoin sen. Aloitin menemällä `Symbol Tree` kohtaan josta valitsin funktiot ja niistä `main` 

<img width="224" height="172" alt="b)1" src="https://github.com/user-attachments/assets/bc2ffd00-3d3c-40d5-9805-621f836bab17" /> 

aukesi näkymä  <img width="1053" height="570" alt="b)2" src="https://github.com/user-attachments/assets/dc7cd722-c27b-4730-a0eb-139e26d32c12" />

`int iVarl` on käyttäjän syöte ja `char local_28` on tulos jota verrataan oikeaan salasanaa, joten nimesin kohdat seuraavanlaisesti.

<img width="159" height="47" alt="b)3" src="https://github.com/user-attachments/assets/2a147666-d16f-4777-80d5-9a80f990bfa2" />

Ohjelma tulostaa tekstin `What's  the password?` jonka jälkeen käyttäjä syöttää salasanan, jota `input = strcmp` verrataan onko käyttäjän antama salasana sama mikä on määritetty.

## c)

Tarkoituksena oli muokata passtr-binääri siten, että se hyväksyy kaikki salasanat paitsi oikean ja sen jälkeen osoittaa, että ohjelma toimii.

Aloitin samanlaisella lähestymistavalla kuin b) kohdassa.

<img width="1282" height="763" alt="c)1" src="https://github.com/user-attachments/assets/069045f7-656c-4817-81d2-380050c987b6" />

Mietin, että tässä pitää jollain tavalla muokata if lauseketta. Klikkasin sitä ja `Listing` kohdassa korostui kohta:

<img width="1043" height="21" alt="c)2" src="https://github.com/user-attachments/assets/01378f4f-2d48-43fa-bdbe-a6e77d74f552" />

Aloitin puoli vahingossa ratkaisemaan vasemmalta oikealle ja päätin googlettaa `JNZ` merkityksen, eli Jump-Not-Zero siirtää ohjelman suorituksen toiseen kohtaan, jos edellisen laskun tulos ei ole nolla. Tämän vastakohta on `ZN` eli Jump-Zero
