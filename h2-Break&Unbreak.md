## a)

Aloitin murtautumisen kokeilemalla saanko type="number" kohdan tyhjäksi ja value="" kohtaan syötettyä teksin: 'OR+1=1--ADMIN .

<img width="1280" height="800" alt="VirtualBox_Kali Linux_19_01_2026_12_27_53" src="https://github.com/user-attachments/assets/d21b9db7-cb80-4930-a000-f9dd9d57e16b" />

Tämä onnistui, mutta se ei kuitenkaan oikeaa salasanaa mitä tehtävässä haettiin. Osaamiseni loppui tähän, joten päätin etsiä netistä lisää apua PortSwiggerin sivuilta. Sieltä löysin SQL injection UNION attacks kohdasta lisää tieto miten UNION hyökkäykset toimivat. Nyt päätin jatkaa samalla lähestymisellä ja muuttaa type="number" kohdan tyhjäksi, mutta muutoksen aikaisempaan value kohtaan latoin value="' UNION SELECT password FROM pins--" .

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



