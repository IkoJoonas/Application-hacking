## Laitteisto

Host : MacBook Air M2 2022 16Gt

Guest: Oracle VM VirtualBox 7.2.0

Virtuaalikone: Kali Linux -> Debian ARM 64

Ram: 8GB

Levytila: 20GB

CPU: 2 

## 1. Decrypt firmware image

Aloitin kloonaamalla gitti repon `https://github.com/robbins/tp-link-decrypt.git` ja lataamalla annetutu tiedostot `aws s3 cp s3://download.tplinkcloud.com/firmware/Tapo_C200v3_en_1.4.2_Build_250313_Rel.40499n_up_boot-signed_1747894968535.bin Tapo_C200v4_en_1.4.2.bin --no-sign-request` ja `https://quentinkaiser.be/security/2025/07/25/rooting-tapo-c200/`.

GitHubin ohjeistuksessa oli ajaa komennot: `./preinstall.sh`, `/extract_keys.sh` ja `make`.

Näiden jälkeen decryptasin image-tiedoston.

<img width="1280" height="800" alt="decrypt image" src="https://github.com/user-attachments/assets/90c09cdd-32bb-4efd-82b3-b0741108cde0" />

## 2. Analyse the image file

Tiedostosta löytyy mm. bootloader, Linux-ydin, JBOOT-otsikko ja SquashFS-rootfs

## 3. Extract rootfs from the dump file

Decryptasin dump-tiedoston ja tutkin sitä käyttäen `binwalk`.

<img width="1280" height="800" alt="binwalk dump" src="https://github.com/user-attachments/assets/ae274fa0-f138-4b82-a97d-3d66dabcec8f" />

Erottelin rootfs dumpista käyttäen komentoa `dd if=dump-tapo-c200v3-1.4.2.bin of=rootfs.bin bs=1 skip=4456448`.

<img width="658" height="103" alt="Näyttökuva 2026-02-28 kello 13 36 18" src="https://github.com/user-attachments/assets/fa57b045-cec4-4905-8f54-e79a2e6fc014" />

Tämän jälkeen purin käyttäen `binwalk -e rootfs.bin`

<img width="1172" height="204" alt="Näyttökuva 2026-02-28 kello 13 37 40" src="https://github.com/user-attachments/assets/e13c2c63-1f47-447c-adbb-a940a35bf6d4" />

Etsin missä rootfs voisi olla.

<img width="708" height="57" alt="Näyttökuva 2026-02-28 kello 14 09 40" src="https://github.com/user-attachments/assets/91acf45c-6df5-401a-bf3c-8505f90902c2" />

Menin bin-alikansioon ja purin sieltä `main` samalla menetelmällä kuten alussa, mutta en löytänyt rootfs:ää (käyttäen Copilottia apuna).

<img width="1179" height="665" alt="Näyttökuva 2026-02-28 kello 13 57 38" src="https://github.com/user-attachments/assets/04a83b96-827f-47b7-b3ec-c3aba320b3a3" />

## 4. Extract rootfs from image file

Samalla menetelmäälä kuten 3. kohdassa.

<img width="767" height="70" alt="rootfs imagefile" src="https://github.com/user-attachments/assets/5ef110a0-e736-49cd-9316-21b599110a7b" />

Koitin löytää rootfs (käyttäen Copilottia apuana), mutta tuloksetta.

<img width="739" height="135" alt="Näyttökuva 2026-02-28 kello 20 34 05" src="https://github.com/user-attachments/assets/8e2fc398-664b-4989-bf2a-554b2c01c825" />

## 5. Search available applications

Dump-tiedostosta löydetyt:

<img width="633" height="143" alt="Näyttökuva 2026-02-28 kello 19 54 09" src="https://github.com/user-attachments/assets/dc097eac-42e0-4247-a304-aced49d21680" />

<img width="630" height="67" alt="Näyttökuva 2026-02-28 kello 19 54 18" src="https://github.com/user-attachments/assets/df92910a-7787-4b9a-a163-7733780e88e8" />

<img width="626" height="158" alt="Näyttökuva 2026-02-28 kello 19 54 37" src="https://github.com/user-attachments/assets/0929b26b-8993-499d-9ae6-6f949016fd24" />

image-tiedostosta löydetyt:

<img width="629" height="139" alt="Näyttökuva 2026-02-28 kello 19 55 50" src="https://github.com/user-attachments/assets/25095a94-257f-4202-8fbc-21bcb61fb0f8" />

<img width="636" height="74" alt="Näyttökuva 2026-02-28 kello 19 56 13" src="https://github.com/user-attachments/assets/397dcf48-fcd4-4306-a138-44aba96085fb" />

<img width="659" height="164" alt="Näyttökuva 2026-02-28 kello 19 56 27" src="https://github.com/user-attachments/assets/b0b3ef88-e15b-44f6-a8d9-90662bf07731" />

## 6. Analyse and try to open root password

En saanut salasanaa selville:

<img width="1173" height="681" alt="Näyttökuva 2026-02-28 kello 20 01 35" src="https://github.com/user-attachments/assets/e1e4440f-b7ca-40bb-a881-4aa7f6b10112" />

## Lähteet

- https://github.com/robbins/tp-link-decrypt

- Kaiser Q. Rooting the Tapo C200: https://quentinkaiser.be/security/2025/07/25/rooting-tapo-c200/

- Copilot analysointiin ja tulkitsemiseen
