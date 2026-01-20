# Maturitní otázka: Souborové systémy v Linuxu (GNU/Linux)

**Tagy:** #maturita #ops #linux #filesystem
**Doba projevu:** cca 15 minut
**Zdroj:** Prezentace 05GNULinux_souborovy_system.pdf

---

## 1. Úvod: Co je to vlastně souborový systém?

**Definice:** Souborový systém (FS - File System) je soubor pravidel, která určují, jak se data na disk ukládají a jak se čtou.
Bez něj by byl pevný disk jen hromada nul a jedniček bez ladu a skladu.

**Co FS řeší:**
1.  **Kde** data fyzicky leží.
2.  **Jak se jmenují** a v jakém jsou adresáři.
3.  **Kdo** k nim má přístup (práva čtení/zápisu).

> [!NOTE] Jak to pochopit (Analogie)
> Představ si pevný disk jako obrovskou prázdnou halu.
> **Souborový systém** jsou regály, šanony a seznam, kde co leží. Bez toho bys naházel papíry na zem a už bys je nikdy nenašel.
> Každý disk nebo fleška musí mít tento "systém regálů" naformátovaný, aby fungoval.

---

## 2. Hlavní rozdíl: Windows vs. Linux

### Windows (Co známe)
* Každý disk je zvlášť: `C:\`, `D:\`, `E:\` (např. USB).
* Je to rozdělené na písmenka.

### Linux (Stromová struktura)
* Existuje **pouze jeden kořen** (root), označuje se lomítkem `/`.
* Všechno ostatní (další disky, DVD, USB, síťové disky) se připojuje do tohoto jednoho stromu jako podadresář.
* Tento proces připojení se nazývá **Mountování (mount)**.

> [!INFO] Příklad mountování
> Když v Linuxu připojíš USB disk, neobjeví se jako `E:`. Systém ho vezme a "přilepí" ho třeba do složky `/media/usb`. Když otevřeš tuto složku, koukáš se vlastně na to USBčko.

---

## 3. Struktura adresářů (FHS)

Celý systém vypadá jako obrácený strom. Kořen `/` je nahoře.
### Klíčové adresáře v kořenu `/`:
* **/boot**: Startovací soubory, je tu jádro systému (kernel) a zavaděč (GRUB).
* **/bin** a **/sbin**: Programy (spustitelné soubory).
    * `/bin` = pro všechny uživatele (základní příkazy jako `ls`, `cp`).
    * `/sbin` = systémové programy jen pro správce (superuživatele/root).
* **/etc**: Nastavení a konfigurace. Jsou to textové soubory, které jde upravovat (všechna nastavení systému jsou zde).
* **/home**: Domovské složky uživatelů (např. `/home/pepa/`). Tady máš své Dokumenty, Hudbu atd. Je to jediné místo, kam můžeš jako běžný uživatel volně zapisovat.
* **/root**: Domovská složka hlavního správce (admina). Pozor, neplést s kořenem `/`!
* **/dev**: Zařízení (Devices). V Linuxu je **všechno soubor**, i hardware (myš, disk, tiskárna).
* **/tmp**: Dočasné soubory (temp). Po restartu se většinou promaže.
* **/proc**: Virtuální složka. Neleží na disku, ale v RAM. Jsou tu informace o běžících procesech a stavu HW.

---
## 4. Cesty k souborům
*Krátká vsuvka o tom, jak se v systému pohybujeme.*

1.  **Absolutní cesta:** Vždy začíná lomítkem `/` (od kořene). Je to kompletní adresa.
    * Např: `/home/david/docs/skola`.
2.  **Relativní cesta:** Nezačíná lomítkem. Cesta odtud, kde zrovna jsem.
    * `..` (dvě tečky) = o úroveň výš (zpět).
    * `.` (tečka) = aktuální adresář.

---
## 5. Typy souborových systémů
*Tohle je technická část zkoušky. Rozdělujeme je na 3 skupiny.*
### A) Tradiční (starší)
* **ext2**: Klasický Linuxový systém. Rychlý, ale **nebezpečný při výpadku proudu**. Pokud vypneš PC "natvrdo", musí se dlouho kontrolovat celý disk, jestli se data nepoškodila.
* **FAT/FAT32**: Známe z Windows a flešek. Linux ho umí číst i zapisovat.
### B) Žurnálovací (Moderní standard)
* Řeší problém s výpadkem proudu pomocí **Žurnálu** (deníku).
* **Princip:**
    1.  Zapíše do "deníku", co se chystá udělat.
    2.  Udělá to (zapíše data).
    3.  Škrtne to z deníku.
* **Výhoda:** Když vypadne proud, systém se podívá do deníku, co nestihl, a opraví to hned. Žádná dlouhá kontrola.
* **Zástupci:**
    * **ext3**: Žurnálovací verze ext2.
    * **ext4**: Dnešní standard, rychlejší, zvládá obří soubory.
    * **NTFS**: Systém z Windows, Linux s ním umí pracovat.
    * **Btrfs**: Moderní, umí pokročilé věci (snapshoty).
### C) Swap (Odkládací)
* Není to klasický FS pro soubory.
* Je to místo na disku, které slouží jako **rozšíření operační paměti RAM**. Když dojde RAMka, systém si "odloží" data sem.

---
## 6. Typy souborů v Linuxu
*V Linuxu není vše jen "soubor" a "složka".*

1.  **Obyčejný soubor:** Text, obrázek, program.
    * *Pozor:* V Linuxu nerozhoduje přípona (`.exe`, `.txt`), ale obsah a práva.
    * *Skrytý soubor:* Začíná tečkou (např. `.config`).
2.  **Adresář (Directory):** Seznam odkazů na jiné soubory.
3.  **Odkazy (Links):**
    * **Symbolický (Soft link):** Jako "Zástupce" ve Windows. Když smažeš originál, odkaz přestane fungovat.
    * **Pevný (Hard link):** Druhé jméno pro ten samý soubor na disku. Data zmizí, až když smažeš *všechny* odkazy na ně.
4.  **Speciální soubory zařízení (v `/dev`):**
    * **Blokové:** Čte se po kusech (blocích) – Disky, DVD.
    * **Znakové:** Čte se po písmenkách (znacích) – Klávesnice, myš, tiskárna.

> [!TIP] Zajímavé speciální soubory
> * `/dev/null`: Černá díra. Cokoliv do ní pošleš, to zmizí.
> * `/dev/random`: Generuje náhodná čísla.

---
## 7. Jak se značí disky?
*U maturity se můžou zeptat: "Co znamená sda1?"*

* **sd** = SCSI/SATA disk (dnešní standard).
* **Písmeno (a, b, c...)** = Který je to fyzický disk.
    * `sda` = První disk.
    * `sdb` = Druhý disk.
* **Číslo (1, 2, 3...)** = Oddíl (Partition) na tom disku.
    * **sda1** = První disk, první oddíl.

---
## 8. Závěr (Shrnutí pro komisi)
1.  Linux má **jeden kořenový adresář `/`**, do kterého se připojují (mountují) ostatní disky.
2.  Adresářová struktura je pevně daná (standard FHS), důležité jsou `/home` (uživatel), `/etc` (config) a `/dev` (HW).
3.  Používáme **žurnálovací systémy** (ext4) kvůli bezpečnosti dat.
4.  Všechno v Linuxu je soubor (i hardware).