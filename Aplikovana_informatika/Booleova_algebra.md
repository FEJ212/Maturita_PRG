# Maturitní otázka: Logické funkce a jejich minimalizace

**Tagy:** #maturita #ops #hardware #logika
**Doba projevu:** cca 15 minut
**Zdroje:** Prezentace 231, 232, 233, 234

---

## 1. Úvod: O co tady jde?
*Na úvod musíš říct, že počítače neumí počítat s desítkovými čísly (0-9), ale jen s nulami a jedničkami.*

* **Booleova algebra** je matematický základ fungování počítačů.
* Pracuje pouze se dvěma stavy:
    * **1 (True/Pravda):** Proud teče, vysoké napětí.
    * **0 (False/Nepravda):** Proud neteče, nízké napětí.
* Booleava algebra tvrdí, že pomocí 3 základních operací (NOT, OR, AND) lze sestavit jakoukoliv funkci.
* Procesor je složen z milionů hradel v různých kombinací, čímž je programovatelný
     * Všechny obvody hradel jsou vyvedeny do "filtru", který propustí co počítač vyžaduje a nepropustí zbytek.
* **Cíl této otázky:** Máme nějakou složitou logickou funkci (obvod) a chceme ji **minimalizovat** (zjednodušit), aby dělala to samé, ale byla levnější a rychlejší.

---

## 2. Základní logické operace
*Tohle je abeceda. Musíš znát tři hlavní hradla.*

1.  **Negace (NOT):** Obrací hodnotu. Z 0 udělá 1, z 1 udělá 0.
    * *Značení:* Pruh nad písmenem ($\bar{A}$) nebo apostrof ($A'$).
2.  **Logický součin (AND):** Musí platit **všechny** vstupy naraz, aby byl výstup 1.
    * *Analogie:* Aby auto jelo, musíš mít benzín **A** klíčky.
    * *Značení:* Tečka ($A \cdot B$).
3.  **Logický součet (OR):** Stačí, aby platil **alespoň jeden** vstup.
    * *Analogie:* Do kina půjdu, když bude pršet **NEBO** budu mít peníze.
    * *Značení:* Plus ($A + B$).
4.  **Exkluzivní součet (XOR):** Musí platit **pouze jeden** vstup.
    * *Analogie:* Dnes je **buď** pondělí, **nebo** pátek. (nemůže platit obojí najednou)
    * *Značení:* Plus v kroužku
> Hradle lze kombinovat, například AND + NOT = NAND

---
## 3. Pravidla a zákony (Jak s tím počítat)
*Nemusíš recitovat všechny, ale vypíchni ty nejdůležitější pro úpravy.*

* **Komutativnost:** $A + B = B + A$ (je jedno, v jakém pořadí to je).
* **Asociativnost:** $(A + B) + C = A + (B + C)$ (závorky nehrají roli u stejných znamének).
* **Absorpce:** Důležité pro zjednodušování!
    * $A \cdot (A + B) = A$ (To $B$ se "vyruší/absorbuje", protože $A$ je silnější).
    * Lze aplikovat i na složitější struktury.
* **De Morganovy zákony:** (Super důležité pro negaci celých výrazů)
    * Když znegujete celý výraz, změní se znaménko.
    * $\overline{A \cdot B} = \bar{A} + \bar{B}$ (Součin se mění na součet).
    * $\overline{A + B} = \bar{A} \cdot \bar{B}$ (Součet se mění na součin).

> [!TIP] Pomůcka pro De Morgana
> "trhni čáru, změň znaménko". Když přetrhneš negaci nad celým výrazem, musíš otočit znaménko uprostřed.

---
## 4. Vyjádření logické funkce (Formy)
*Jak tu funkci zapíšeme? Máme dvě hlavní možnosti.*

Představ si **pravdivostní tabulku** (seznam všech kombinací 0 a 1).

1.  **Úplný součtový tvar (Disjunktivní - DNF):**
    * Koukáme se na řádky, kde je výsledek **1**.
    * Z těchto řádků se vytváří implikanty
         * Když je proměnná 0 => je negovaná
         * Když je proměnná 1 => je přímá (bez negace)
    * Vytváříme tzv. **mintermy**.
2.  **Úplný součinový tvar (Konjunktivní - CNF):**
    * Koukáme se na řádky, kde je výsledek **0**.
    * Z těchto řádků se vytvoří úplný součtový tvar => překlopen pomocí De Morghanových zákonů na součinový
    * Vytváříme tzv. **maxtermy**.

---
## 5. Minimalizace (To hlavní "maso")
*Proč to děláme?*
Když navrhujeme procesor, chceme co nejméně hradel (transistorů). Méně hradel = menší spotřeba, menší teplo, nižší cena, vyšší rychlost.

Máme 3 způsoby, jak na to:
### A) Algebraická minimalizace
* Počítáme to ručně pomocí vzorečků (vytýkání, krácení, De Morgan).
* *Nevýhoda:* U složitých funkcí je to pracné a snadno uděláš chybu.
### B) Karnaughovy mapy (Grafická metoda)
* Nejpoužívanější u maturity. Je to vlastně "přeskládaná tabulka" do mřížky.
* **Princip:**
    1.  Nakreslíš tabulku.
        * Velikost tabulky = 2^n, n = počet proměnných (pro 4 proměnné je to 16 => 4x4 políčka)
    3.  Osy popíšeš v **Grayově kódu** (00, 01, 11, 10). *Pozor: 11 a 10 jsou prohozené, aby se vždy měnila jen jedna číslice!*
    4.  Doplníš jedničky tam, kde má funkce hodnotu 1.
    5.  **Smyčkování (Grupování):** Kroužkuješ skupiny jedniček.
        * Pravidlo 1: Skupina musí být obdélník nebo čtverec.
        * Pravidlo 2: Počet jedniček ve skupině musí být mocnina dvojky (1, 2, 4, 8, 16).
        * Pravidlo 3: Mapa je "zacyklená" – kraje k sobě patří (jako v Pac-Manovi, vyjedeš vpravo, vyjedeš vlevo).
        * Pravidlo 4: Všechny 1 musí být zasmyčkovány a žádná 0 (prázdné políčko) nesmí být ve smyčce.
        * Pravidlo 5: Neurčité hodnoty:
             * Do mapy se zapisují jako X
             * Mohou, ale nemusí být součástí smyček (jen pokud se hodí k vytvoření větší smyčky)
        * Pravidlo 6: Smyčky děláme co možná největší.
        * Pravidlo 7: Smyček děláme co možná nejmíň.
    6.  **Výsledek:** Z každé smyčky vznikne jeden zjednodušený výraz. Proměnná, která se v rámci smyčky mění (je tam 0 i 1), vypadává. Zůstává jen ta, co se nemění.

### C) Quine-McCluskey (Tabulková metoda)
* Používá se, když je proměnných hodně (5 a více), kde už je K-mapa nepřehledná.
* Je to algoritmus, který se dá naprogramovat do počítače.
* **Princip:**
    1.  Vypíšeš si všechny stavy (indexy), kde je 1.
    2.  Hledáš dvojice, které se liší jen v **jednom bitu**.
    3.  Tím vznikají tzv. **prostí implikanti**.
    4.  Děláš to ve více krocích, dokud to jde redukovat.
    5.  Lze nakonec sestavit tabulku pokrytí a vyberat nezbytné členy. (někdy Quine-McCluskey neminimalizuje na nejmenší možnou formu)

---
## 6. Závěr (Shrnutí)
1.  Počítače pracují v **Booleově algebře** (0 a 1).
2.  Základní hradla jsou **NOT, AND, OR**.
3.  Funkce zapisujeme buď podle jedniček (součtový tvar) nebo nul (součinový tvar).
4.  Aby byl hardware efektivní, musíme funkce **minimalizovat**.
5.  Pro člověka je nejlepší **Karnaughova mapa** (grafická), pro počítač **Quine-McCluskey** (algoritmus).
