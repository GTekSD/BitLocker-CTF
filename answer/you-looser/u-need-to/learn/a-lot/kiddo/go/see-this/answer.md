# YOU DUMB SHIT!

## BitLocker Drive Encryption CTF Challenge

## Prerequisites

- Kali Linux [Click here for quick kali](https://github.com/GTekSD/WSL2-kali-setup.git)
- Bitlocker2john tool
- Hashcat
- Dislocker

## Solution

1. Download all the `findme_encrypted` files from the [repo](https://github.com/GTekSD/BitLocker-CTF.git).
2. Change the file extensions of all the downloaded files from `.bin` to `.rar`.
```
findme_encrypted.part01.rar
findme_encrypted.part02.rar
findme_encrypted.part03.rar
findme_encrypted.paft04.rar
findme_encrypted.part05.rar
```
4. Extract the contents of the `findme_encrypted.rar` file using WinRAR or a similar tool.
5. You will get the `secret_data.vhdx` file.
6. Use [John the Ripper](https://www.kali.org/tools/john/) Tool command:
```
bitlocker2john -i secret_data.vhdx
```
This will extract 4 hashs of the `secret_data.vhdx` file, but we only need `User Password hash`.
```
User Password hash:
$bitlocker$0$16$e3a44be96aec799222409bffc2925f0d$1048576$12$40f2ca40074ed90103000000$60$1aa9824586386a31b93a5bed58b8481e80b92f0cb790d761029d904721cf1ba8f1c61ccbc0361f91a5ed0f588657ae59da4c6744a0c598ae5a215dc2
```
7. Copy User Password hash and save to `hash.txt` file
```
$bitlocker$0$16$e3a44be96aec799222409bffc2925f0d$1048576$12$40f2ca40074ed90103000000$60$1aa9824586386a31b93a5bed58b8481e80b92f0cb790d761029d904721cf1ba8f1c61ccbc0361f91a5ed0f588657ae59da4c6744a0c598ae5a215dc2
```
8. Use [Hashcat](kali.org/tools/hashcat/) to crack the obtained hash and get the password `maryjane*`. Use the following command:
```
hashcat -m 22100 hash.txt rockyou.txt
```
where `rockyou.txt` is a password list file that is commonly used for password cracking, located in `/usr/share/wordlists` directory. This may take some time depending on the strength of the password and the processing power of the machine used. Once Hashcat successfully cracks the password, it will be displayed in the terminal. The password in this case is `maryjane*`.

9. Mount the `secret_data.vhdx` drive in ur Windows system.
10. Open the `Waoh!!!.txt` file and decode the base64-encoded obtained flag.

