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

Ohjelman rivin 18. viittaa rivin 14. `Null` kohtaan. Tein tähän muutoksen vaihtamalla `Null` tilalle `fixed`.

<img width="744" height="509" alt="lab1valmis" src="https://github.com/user-attachments/assets/ed17eb38-30ca-4bec-bb70-f45b28d54374" />

