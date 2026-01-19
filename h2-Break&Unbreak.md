## a)

Aloitin murtautumisen kokeilemalla saanko type="number" kohdan tyhjäksi ja value="" kohtaan syötettyä teksin: 'OR+1=1--ADMIN .

<img width="1280" height="800" alt="VirtualBox_Kali Linux_19_01_2026_12_27_53" src="https://github.com/user-attachments/assets/d21b9db7-cb80-4930-a000-f9dd9d57e16b" />

Tämä onnistui, mutta se ei kuitenkaan oikeaa salasanaa mitä tehtävässä haettiin. Osaamiseni loppui tähän, joten päätin etsiä netistä apua lisää PortSwiggerin sivuilta. Sieltä löysin SQL injection UNION attacks kohdasta lisää apua. Nyt päätin jatkaa samalla lähestymisellä ja muuttaa type="number" kohdan tyhjäksi, mutta muutoksen aikaisempaan value kohtaan latoin value="' UNION SELECT password FROM pins--" .

<img width="1280" height="800" alt="VirtualBox_Kali Linux_19_01_2026_12_30_23" src="https://github.com/user-attachments/assets/b44401ec-0b3f-438a-8394-4662314fdf00" />
