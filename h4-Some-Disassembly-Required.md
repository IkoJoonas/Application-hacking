## Laitteisto

Host: Suoritin: AMD Ryzen 7 1700 (8-Core Processor) RAM: 32 Gt Näytönohjain: 8 Gt Tallennustila: 932 Gt

Guest: Oracle VM VirtualBox 7.2.4

Virtuaalikone: Debian 13.3 Cinnamon

RAM: 4GB

Levytila: 20 GB

CPU: 2

## x) Tiivistä

Hammond 2022: https://www.youtube.com/watch?v=oTD_ki86c9I

- Ghidra on reverse engineering työkalu

- Ratkaisee picoCTF haasteen videossa

## a) Install Ghidra

Aloitin Ghidran asentamisen käyttämällä `sudo apt install openjdk-21-jdk` komentoa. Tämän jälkeen menin [Ghidran Github](https://github.com/NationalSecurityAgency/ghidra/releases) sivulle ja latasin 12.0.1 version. Purin kansion ja käynnistin sovelluksen.

<img width="802" height="611" alt="ghidra" src="https://github.com/user-attachments/assets/0807d309-72e9-467a-a346-18ab121466e4" />

## b) rever-C

Tarkoituksena oli käänteismallintaa packd-binääri C-kielelle Ghidran avulla, etsiä pääohjelma, antaa muuttujille kuvaavat nimet, selittää ohjelman toiminta ja ratkaista binääri ilman, että katsoo alkuperäistä lähdekoodia.

Avasin Ghidran ja loin uuden projektin, jonne importtasin packd tiedoston ja auto analysoin sen. Aloitin menemällä `Symbol Tree` kohtaan josta valitsin funktiot ja niistä `main` .

<img width="224" height="172" alt="b)1" src="https://github.com/user-attachments/assets/bc2ffd00-3d3c-40d5-9805-621f836bab17" /> 

aukesi näkymä:  <img width="1053" height="570" alt="b)2" src="https://github.com/user-attachments/assets/dc7cd722-c27b-4730-a0eb-139e26d32c12" />

`int iVarl` on käyttäjän syöte ja `char local_28` on tulos jota verrataan oikeaan salasanaa, joten nimesin kohdat seuraavanlaisesti:

<img width="159" height="47" alt="b)3" src="https://github.com/user-attachments/assets/2a147666-d16f-4777-80d5-9a80f990bfa2" />

Ohjelma tulostaa tekstin `What's  the password?` jonka jälkeen käyttäjä syöttää salasanan, jota `input = strcmp` verrataan onko käyttäjän antama salasana sama mikä on määritetty. Ratkaisu salasana on `piilos-AnAnAs`.

## c) If backwards

Tarkoituksena oli muokata passtr-binääri siten, että se hyväksyy kaikki salasanat paitsi oikean ja sen jälkeen osoittaa, että ohjelma toimii.

Aloitin samanlaisella lähestymistavalla kuin b) kohdassa.

<img width="1282" height="763" alt="c)1" src="https://github.com/user-attachments/assets/069045f7-656c-4817-81d2-380050c987b6" />

Mietin, että tässä pitää jollain tavalla muokata if lauseketta. Klikkasin sitä ja `Listing` kohdassa korostui kohta:

<img width="1043" height="21" alt="c)2" src="https://github.com/user-attachments/assets/01378f4f-2d48-43fa-bdbe-a6e77d74f552" />

Aloitin puoli vahingossa ratkaisemaan vasemmalta oikealle ja päätin googlettaa `JNZ` merkityksen, eli Jump-Not-Zero siirtää ohjelman suorituksen toiseen kohtaan, jos edellisen laskun tulos ei ole nolla. Tämän vastakohta on `ZN` eli Jump-Zero. Muuttaminen tapahtui oikea klikkaamalla ja valitsemalla `Patch Instruction`.

<img width="1045" height="17" alt="c)3" src="https://github.com/user-attachments/assets/25706b44-93f4-4030-818b-9cb279893086" />

Exporttasin ohjelman.

<img width="339" height="214" alt="c)4 0" src="https://github.com/user-attachments/assets/1a6dd5f7-878e-49a6-b4e2-f86887e39445" />

Annoin oikeudet komennolla `chmod +x passtr.1`.

Testasin ensin syöttämällä väärän salasanan ja sen jälkeen oikean.

<img width="741" height="251" alt="c)4" src="https://github.com/user-attachments/assets/2b47f2eb-f154-4a00-9fe0-9d56dfa8b1d9" />

Toimi.

## d) Nora CrackMe

Kloonasin Nora CrackMe repon itselleni komennolla `git clone`.

<img width="728" height="182" alt="d)1" src="https://github.com/user-attachments/assets/1c02a40b-b373-44e0-a512-7778ae0b049e" />

Luin README.md tiedoston käyttämällä `cat` komentoa.

<img width="728" height="347" alt="d)2" src="https://github.com/user-attachments/assets/c6e17d92-9b25-4761-b8ea-c355e3385421" />

## e) Nora crackme01

Tarkoituksena oli ratkaista binääri.

Loin tiedoston komennolla `make crackme01`

<img width="628" height="113" alt="e)1" src="https://github.com/user-attachments/assets/826fbd36-de9b-4f71-a6e5-bbfbe70e0605" />

Aloitin käyttämällä `strings` komentoa.

<img width="509" height="360" alt="e)2" src="https://github.com/user-attachments/assets/3173fb6b-6885-41c7-8010-3b136e2e1624" />

Huomasin mahdollisen salasanan ja kokeilin sitä.

<img width="551" height="33" alt="e)3" src="https://github.com/user-attachments/assets/31b5b457-6ebf-4304-9763-10dc06d9a08f" />

Salasana toimi.

## e) Nora crackme01e

Tässäkin tarkoituksena oli ratkaista binääri.

Loin tiedoston ja testasin `strings` komennon niinkuin aiemmin.

<img width="521" height="348" alt="e)5" src="https://github.com/user-attachments/assets/e6ebfa40-b744-4575-8d4f-930fb9d37136" />

Mahdollinen salasana oli taas näkyvillä ja kokeilin sitä.

<img width="567" height="36" alt="e)6" src="https://github.com/user-attachments/assets/f895bbd7-83de-4304-9e49-56f086ede494" />

Tällä kertaa ei toiminutkaan vaan bash tulkitsee `!` merkin. Kokeilin yksinkertaista ratkaisua ja laitoin salasanan lainausmerkkeihin.

<img width="584" height="38" alt="e)7 0" src="https://github.com/user-attachments/assets/f9747d6b-6c3f-4490-8384-69e41f07f1dc" />

Nyt toimi :)

## f) Nora crackme02

Tarkoituksena oli nimetä pääohjelman muuttujat käänteismallinnetusta binääristä, selittää ohjelman toimita ja ratkaista binääri.

Loin tiedoston ja tein sille projektin Ghidraan. Menin pääfunktioon.

<img width="417" height="498" alt="f)1 0" src="https://github.com/user-attachments/assets/5a7d22d8-d13d-42fd-b2a3-c77c2a85c3ba" />

Nimesin `char`, `undefined8` ja `long` kohdat seuraavanlaisesti:

<img width="169" height="65" alt="f)2" src="https://github.com/user-attachments/assets/6d89fecd-756c-4bb2-a20a-8349a9858bf3" />

Tämä tosin ei ollutkaan ihan yhtä helppoa, kuin aiemmin vaan kysyin tekoälyltä apua.

Luulen, että ymmärsin ohjelman toiminnan jotenkin itse eli salasana ei olekkaan `password1` vaan se on pelkästään `o`? Päätin kokeilla tätä.

<img width="483" height="44" alt="f)3" src="https://github.com/user-attachments/assets/34a96b21-9a28-476b-9a24-142a023da4a3" />

Näyttäisi olevan oikea vastaus. (?)

## Lähteet

- Hammond 2022: https://www.youtube.com/watch?v=oTD_ki86c9I

- https://terokarvinen.com/application-hacking/

- [Tekoäly](https://chatgpt.com/)

- Tindall 2023: https://github.com/NoraCodes/crackmes

- Ghidra: https://github.com/NationalSecurityAgency/ghidra
