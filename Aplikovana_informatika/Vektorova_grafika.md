# Maturitní otázka: Vektorová grafika

**Tagy:** #maturita #ops #grafika #vektor
**Doba projevu:** cca 15 minut
**Zdroj:** GRAFIKA-uvod.pptx

---
## 1. Co to je Vektorová grafika?
*Nejprve definice. Musíš vysvětlit, že to nejsou tečky (pixely).*

**Definice:** Vektorová grafika je způsob ukládání obrazu pomocí **matematických objektů** a analytické geometrie.

Zatímco rastrová grafika (fotka) je mřížka barevných bodů, vektorový obrázek je vlastně **seznam instrukcí** pro počítač, jak má obrázek nakreslit.

**Skládá se z:**
* Bodů
* Přímek a křivek
* Mnohoúhelníků (geometrických tvarů)

> [!NOTE] Analogie pro pochopení
> **Rastr (fotka)** je jako mozaika z dlaždiček. Když přijdeš moc blízko, vidíš spáry a kostičky.
> **Vektor** je jako technický výkres od architekta. Jsou tam instrukce: "Udělej čáru z bodu A do bodu B". Je jedno, jak moc to přiblížíš, čára bude vždy hladká.

---
## 2. Hlavní výhody a nevýhody
*Tohle je jádro otázky. Proč se vektory používají?*

### Výhody (+)
1.  **Libovolné zmenšování a zvětšování (Škálovatelnost):** Obrázek můžeš roztáhnout na velikost paneláku a bude stále perfektně ostrý. Nedochází ke ztrátě kvality.
2.  **Malá velikost souboru:** U jednoduchých obrázků (loga) je soubor velmi malý, protože se ukládá jen matematický předpis (pár čísel), ne miliony pixelů.
3.  **Snadná editace:** Každý objekt (čtverec, kruh, čára) je v obrázku samostatný. Můžeš ho kdykoliv chytit, posunout, změnit mu barvu nebo tloušťku čáry, aniž bys zničil zbytek obrázku.

### Nevýhody (-)
1.  **Neeviduje fotorealistické detaily:** Nehodí se na fotky. Vyfotit krajinu "vektorově" nejde, protože fotka je příliš složitá a barevně pestrá.
2.  **Náročnost na procesor:** Pokud je v obrázku tisíce složitých objektů, počítač musí neustále přepočítávat jejich tvar. To může být pro procesor náročnější než jen zobrazit mřížku pixelů.
3.  **Kompatibilita:** Někdy může být problém otevřít soubor z jednoho programu v jiném (např. starší verze Corelu vs. nový Illustrator).

---
## 3. Formáty souborů (Přípony)
*Musíš vyjmenovat alespoň 3-4 hlavní formáty.*

* **.CDR (Corel Draw):** Standard pro program CorelDraw.
* **.AI (Adobe Illustrator):** Standard pro grafiky používající Adobe.
* **.SVG (Scalable Vector Graphics):** Dnes nejdůležitější formát pro **web**. Je to vlastně textový soubor (XML), který umí prohlížeč vykreslit.
* **.EPS (Encapsulated PostScript):** Univerzální formát pro přenos mezi různými programy a tiskárnami.
* **.ZMF (Zoner):** Formát programu Zoner Callisto.

---
## 4. Editory (V čem se to kreslí?)

* **Corel Draw:** Velmi rozšířený vektorový editor.
* **Adobe Illustrator:** Průmyslový standard pro profesionály.
* **Inkscape:** Nejznámější editor **zdarma** (Open Source).
* **Zoner Callisto:** Český editor.

---
## 5. Barvy a převody
*Krátká vsuvka, která ukáže, že rozumíš souvislostem.*
### Barevné modely
I ve vektorech musíme řešit barvy:
* **RGB (Red, Green, Blue):** Používáme, pokud bude grafika jen na monitoru (web, prezentace).
* **CMYK (Cyan, Magenta, Yellow, Black):** Používáme, pokud se bude grafika **tisknout** (letáky, vizitky).
### Převod (Konverze)
1.  **Vektor -> Rastr (Rastrování):** Velmi snadné. Počítač prostě "vyfotí" to, co vypočítal. Děláme to, když chceme obrázek uložit jako JPG nebo PNG na web.
2.  **Rastr -> Vektor (Vektorizace):** Velmi obtížné. Počítač se snaží v barevné fotce najít hrany a tvary a vytvořit z nich křivky. Výsledek bývá často nepřesný.

---
## 6. Závěr (Shrnutí pro komisi)
Vektorová grafika je ideální pro **loga, schémata, technické výkresy, písmo a ikony**. Její hlavní silou je, že ji můžeme libovolně zvětšovat bez ztráty kvality (je definována matematicky).