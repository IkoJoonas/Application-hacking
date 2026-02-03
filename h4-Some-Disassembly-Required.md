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

