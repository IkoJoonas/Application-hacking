## Laitteisto

Host 1: MacBook Air M2 2022 16Gt

Guest: Oracle VM VirtualBox 7.2.0

Virtuaalikone: Kali Linux -> Debian ARM 64

Ram: 8GB

Levytila: 20GB

CPU: 2 

Host 2: Suoritin: AMD Ryzen 7 1700 (8-Core Processor) RAM: 32 Gt Näytönohjain: 8 Gt Tallennustila: 932 Gt

Guest: Oracle VM VirtualBox 7.2.4

Virtuaalikone: Debian 13.3 Cinnamon

RAM: 4GB

Levytila: 20 GB

CPU: 2

## x)

OWASP: OWASP Top 10: https://owasp.org/Top10/A01_2021-Broken_Access_Control/

-Yleistä on URL manipulointi ja admin-sivujen selaaminen ilman asianmukaista autentikointia

-Suojaa palvelinpuolella, älä asiakkaalla

Karvinen 2023: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/

-Ffuf on joohoi:n kehittämä webb-fuzzing-työkalu

-Pystyy fuzzaamaan muutakin kuin hakemistoja, kuten parametrejä ja HTTP-otsikoita

PortSwigger: https://portswigger.net/web-security/access-control

-Pääsynhallinta on rajoitusten soveltamista siihen, kuka saa tehdä mitäkin tai käyttää tiettyjä resursseja

-Voidaan estää auditoimalla ja testaamalla pääsynhallintaa perusteellisesti varmistaaksi, että kaikki toimii suunnitellulla tavalla.

Karvinen 2006: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/ 

-Raportointi tarkoittaa, että kerrot täsmällisesti mitä teit, ja mitä sitten tapahtui.

-Toistettavuus, täsmällisyys

## a)

Aloitin murtautumisen kokeilemalla saanko `type="number"` kohdan tyhjäksi ja value="" kohtaan syötettyä teksin: 'OR+1=1--ADMIN .

<img width="1280" height="800" alt="VirtualBox_Kali Linux_19_01_2026_12_27_53" src="https://github.com/user-attachments/assets/d21b9db7-cb80-4930-a000-f9dd9d57e16b" />

Tämä onnistui, mutta se ei kuitenkaan näyttänyt oikeaa salasanaa mitä tehtävässä haettiin. Osaamiseni loppui tähän, joten päätin etsiä netistä lisää apua PortSwiggerin sivuilta. Sieltä löysin SQL injection UNION attacks kohdasta lisää tieto miten UNION hyökkäykset toimivat. Nyt päätin jatkaa samalla lähestymisellä ja muuttaa type="number" kohdan tyhjäksi, mutta muutoksen aikaisempaan value kohtaan latoin value="' UNION SELECT password FROM pins--" .

<img width="1280" height="800" alt="VirtualBox_Kali Linux_19_01_2026_12_30_23" src="https://github.com/user-attachments/assets/b44401ec-0b3f-438a-8394-4662314fdf00" />

ONNISTUMINEN! Lippu tuli näkyville salasanakohtaan.

## b)

Korjasin haavoittuvuuden koodista: sql rivin lopun muotoon :pin;" ja res rivin lopun muotoon {"pin": pin})

<img width="1280" height="800" alt="VirtualBox_Kali Linux_19_01_2026_13_26_53" src="https://github.com/user-attachments/assets/20f27e34-1c38-4322-a8b0-333985591b9e" />

Kokeilin pystyinkö toistamaan aiemmin toimineen haavoittuvuuden.

<img width="1280" height="800" alt="VirtualBox_Kali Linux_19_01_2026_13_21_10" src="https://github.com/user-attachments/assets/415d68d7-44a1-4ba3-807f-4f822a90e5c1" />

Haavoittuvuus ei paljastanut enää lippua.

## c)

Käynnistin tehtävän verkkosivun ja suoritin komennon: ./ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ

<img width="737" height="497" alt="fuzz1" src="https://github.com/user-attachments/assets/a86f8c0e-25da-42d8-92f5-ccb8ce9ca190" />

Huomasin, että lähestulkoon kaikissa näkyi kokona 154, joten filtteröin siitä komennolla:

./ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ -fs 154

Nyt näkyvillä oli paljon vähemmän kohtia mistä jatkaa. 

<img width="732" height="674" alt="fuzz2" src="https://github.com/user-attachments/assets/302dad7b-b87c-4c28-a6ec-36c5fc7ee510" />

Lisäämällä wp-admin URLin loppuun sain ensimmäisen lipun näkyville.

<img width="1280" height="800" alt="VirtualBox_Debian_19_01_2026_18_17_14" src="https://github.com/user-attachments/assets/cf903f08-2b67-4ac9-b6da-32f0100e0a2d" />

Versionhallintaan liittyvä sivu löytyi, kun lisäsi .git/config URLin loppuun. Tämä paljasti viimeisin tarvittavan lipun.

<img width="1280" height="800" alt="VirtualBox_Debian_19_01_2026_18_39_48" src="https://github.com/user-attachments/assets/bc71c37b-ef38-4e10-8d4a-1ce53dc01be0" />

## d)

Käynnistin tehtävän verkkosivun ja aloitin kokeilemalla yleisimpiä admin-tunnuksia, mutta tuloksetta. Seuraavaksi kokeilin lisäämällä URLin loppuun robots.txt .

<img width="1280" height="800" alt="VirtualBox_Kali Linux_20_01_2026_12_03_31" src="https://github.com/user-attachments/assets/7c739174-3da0-4c9e-82e0-d401928a94c1" />

Sivu paljasti piilotetun sivuston admin-console, jota ei ollut näkyvillä verkkosivulla. Kokeilin mennä sivulle, mutta se vei uudelle kirjautumissivulle, josta en myöskään päässyt eteenpäin arvaamalla tunnuksia. Jonkin ajan kuluttua päätin testata miten kävisi, jos teen sivulle tunnukset ja kirjauduttua laitan URLin loppuun löytämäni admin-console.

<img width="1280" height="800" alt="VirtualBox_Kali Linux_20_01_2026_12_42_23" src="https://github.com/user-attachments/assets/a7b281b4-4100-4cbe-a93c-9fafb99e9eb7" />

Tämä onnistui ja pääsin admin-sivustolle normaalina käyttäjänä.

## e)

Haavoittuvuuden korjaamiseksi riitti views.py muokkaaminen lisäämällä koodin loppussa olevalle riville "and self.request.user.is_staff".

<img width="1280" height="800" alt="VirtualBox_Kali Linux_20_01_2026_14_35_40" src="https://github.com/user-attachments/assets/ce916536-cf44-4b8a-af6e-90c27a1b8a3e" />

Kirjauduin uudestaan sivulle ja kokeilin olinko saanut korjattua haavoittuvuuden estämällä pääsyn admin-sivulle normaalina käyttäjänä.

<img width="1280" height="800" alt="VirtualBox_Kali Linux_20_01_2026_14_36_56" src="https://github.com/user-attachments/assets/fa79b909-3d92-44a2-925e-cd7620cde521" />

Korjaaminen oli onnistunut.

## Lähteet

OWASP: OWASP Top 10: https://owasp.org/Top10/A01_2021-Broken_Access_Control/

Karvinen 2023: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/

PortSwigger: https://portswigger.net/web-security/access-control

Karvinen 2006: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/ 

PortSwigger: https://portswigger.net/web-security/sql-injection/union-attacks

Karvinen 2024: https://terokarvinen.com/hack-n-fix/

