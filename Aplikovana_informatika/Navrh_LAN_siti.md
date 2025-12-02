# 🎓 Maturitní téma: Návrh LAN sítí, Topologie a Prvky

## Úvod: Rozdělení sítí podle rozlohy

- **LAN (Local Area Network):** Místní síť (domácnost, škola, jedna firma). Vysoké rychlosti, plná správa vlastníkem.

- **MAN (Metropolitan Area Network):** Městská síť. Propojuje více LAN po městě (např. síť univerzitního kampusu nebo městský kamerový systém).

- **WAN (Wide Area Network):** Rozlehlá síť (stát, kontinent, svět). Typicky internet. Využívá pronajaté linky od operátorů.

## Síťové Topologie (Struktura sítě)

Topologie určuje, jak jsou zařízení v síti vzájemně propojena.

- **Fyzická topologie:** Jak reálně vedou kabely ve zdech.
    
- **Logická topologie:** Jak reálně tečou data (např. fyzicky to může být hvězda, ale data tečou jako v kruhu).
    

![Obrázek: network topologies diagram star bus ring mesh tree](https://encrypted-tbn3.gstatic.com/licensed-image?q=tbn:ANd9GcSBFHT_ytFzEi-U9EnKgyL3Azbo4N6-iBIsGSxET1Z7R7Dt5qW5pjTR3tMuyMahnUvldvff11u_3UIiAYi4rIoV27VofaqF3IAVwiSTtDXWEqRqKl8)

Shutterstock

Prozkoumat

### A) Bus (Sběrnice) – _Historie_

- **Jak to vypadá:** Jeden hlavní koaxiální kabel (páteř/backbone), ke kterému jsou "napíchnuté" všechny počítače. Na koncích musí být **terminátory** (odpory), aby se signál neodrážel.
    
- **Výhody:** Dříve levné (málo kabelu).
    
- **Nevýhody:**
    
    - Pokud se hlavní kabel **kdekoliv** přeruší (nebo se uvolní terminátor), **celá síť spadne**.
        
    - Vysoká kolizovost (všichni "křičí" do jednoho drátu).
        
    - Dnes se v LAN nepoužívá.
        

### B) Line (Linka / Daisy Chain)

- **Jak to vypadá:** Počítače jsou zapojeny sériově za sebou (A -> B -> C -> D).
    
- **Specifikum:** Každý počítač uprostřed musí mít **dvě síťové karty** (jednou přijme, druhou pošle dál).
    
- **Nevýhody:** Pokud vypnu jeden počítač (nebo se rozbije), přeruším spojení pro všechny za ním. Velké zpoždění (latence).
    

### C) Ring (Kruh)

- **Jak to vypadá:** Uzavřený kruh, kde je poslední PC spojené s prvním.
    
- **Princip:** Data běhají jedním směrem. Dříve se používal **Token Ring** (v síti koloval "pešek", kdo ho měl, mohl vysílat = žádné kolize).
    
- **Výhoda:** Signál se na každé stanici zesílí (regeneruje).
    
- **Redundance:** V moderním pojetí (např. FDDI nebo metro-sítě) se používá **dvojitý kruh**. Když se kruh na jednom místě přeruší, data se "otočí" a pošlou druhou stranou -> síť funguje dál.
    

### D) Star (Hvězda) – _Standard dneška_

- **Jak to vypadá:** Centrální prvek (**Switch**) a k němu vede samostatný kabel od každého PC.
    
- **Výhoda:** **Nezávislost.** Když se přeruší kabel k jednomu PC, spadne jen toto jedno PC. Ostatní jedou dál. Snadná diagnostika.
    
- **Nevýhoda:** Spotřeba kabelů. **Single Point of Failure** – když shoří centrální Switch, nejde nikomu nic.
    
- **Ekonomika:** Dnes nejlevnější a nejefektivnější řešení pro LAN.
    

### E) Tree (Strom)

- **Jak to vypadá:** "Namakaná hvězda" nebo hierarchie.
    
- **Struktura:**
    
    1. **Core (Jádro):** Hlavní, super-rychlý switch.
        
    2. **Distribution:** Switche pro jednotlivá patra/budovy.
        
    3. **Access:** Switche, kam se připojují lidi.
        
- **Vlastnosti:** Každý prvek má minimálně 2 připojení (nahoru a dolů). Používá se ve velkých firmách a školách.
    

### F) Mesh (Mřížka)

- **Full Mesh (Fully Connected):** Každý s každým.
    
    - Vzoreček pro počet kabelů: $n \cdot (n-1) / 2$.
        
    - Extrémně drahé, ale nejbezpečnější.
        
- **Partial Mesh (Neuspořádaná):**
    
    - Typické pro **Wi-Fi Mesh** systémy ve městech nebo IoT (Internet věcí).
        
    - **Výhoda:** Samo-opravitelnost. Mohu přerušit klidně polovinu cest a data si najdou jinou trasu ("skákají" přes ostatní uzly).
        
    - **Nevýhoda:** Nepřehledné, složitá konfigurace.
        

> **❓ Maturitní otázka: Kdy jakou topologii použijete?**
> 
> - **Kancelář / Doma:** Topologie **Star (Hvězda)**. Jednoduchá, levná, spolehlivá pro koncové stanice.
>     
> - **Poskytovatel internetu (ISP) / Páteř:** Topologie **Ring** nebo **Mesh**. Potřebují zálohu (redundanci), aby při překopnutí optiky bagrem internet ve městě stále šel.
>     

---

## 3. Síťové prvky (Hardware)

Prvky dělíme na **Pasivní** (kabely, racky – nepotřebují proud) a **Aktivní** (potřebují napájení ⚡, pracují s daty).

Důležité je zařazení do vrstev **OSI modelu**:

![Obrázek: network switch router firewall icons](https://encrypted-tbn3.gstatic.com/licensed-image?q=tbn:ANd9GcTXL4Os2J6Df2B_Zu5w7Cp_wD_QrueqNC-JdaKKZz2eU4KGhkYWIwRtMcnI_E8wnYEyMe5R739WVaohemZqwWir6-U-pGe4_-mFvBCtRJrTP9WXJ8k)

Shutterstock

### A) Hub (Rozbočovač) – L1 (Fyzická vrstva)

- **Funkce:** Hloupé zařízení. Přijme elektrický pulz na jednom portu a zkopíruje ho na **všechny** ostatní porty.
    
- **Problém:**
    
    - Data dostanou i ti, co je nechtějí (bezpečnost).
        
    - Zbytečně zatěžuje síť.
        
    - Vznikají **kolize** (když mluví dva najednou, signál se srazí).
        
- _Dnes se nepoužívá._
    

### B) Switch (Přepínač) – L2 (Linková vrstva)

- _Pozor: Existují i moderní L3 switche (umí routovat)._
    
- **Funkce:** Inteligentní propojení v síti. Rozděluje kolizní domény (každý port je samostatná cesta).
    
- **Bridge (Most) Analogie:** Představ si switch jako soubor mostů. Každý port je jeden "ostrov". Switch funguje jako most, který spojuje jen ty dva ostrovy, které spolu chtějí mluvit.
    
- **CAM Tabulka (Content Addressable Memory):**
    
    - Switch se učí. Když mu přijde rámec, podívá se na **Zdrojovou MAC adresu** a zapíše si: _"MAC ABCD je na portu 1"_.
        
    - Příště, když půjdou data pro ABCD, pošle je **přímo** na port 1 (Unicast) a ne všem.
        
- **VLAN (Virtual LAN):**
    
    - Logické rozdělení jednoho fyzického switche na více virtuálních sítí.
        
    - Označené tagem (číslo **1 až 4096**).
        
    - Slouží k bezpečnosti (oddělení kamer od účetnictví).
        
- **Uplink port:** Speciální port (často rychlejší, např. optický) pro propojení s dalším switchem nebo routerem (směr "ven").
    

### C) Router (Směrovač) – L3 (Síťová vrstva)

- **Funkce:** Spojuje **rozdílné** sítě (např. LAN 192.168.1.0 a Internet).
    
- **Rozhodování:** Řídí se **IP adresami**. Má routovací tabulku a hledá nejlepší cestu k cíli.
    
- **Odděluje Broadcastové domény:** To, co se "vyřvává" v LAN, router nepustí ven.
    
- **NAT (Network Address Translation):** Překlad adres. Schová celou firmu za jednu veřejnou IP adresu.
    

### D) Firewall – L3 / L4 / L5 (i L7)

- **Funkce:** Bezpečnostní brána. Rozhoduje, co smí projít a co ne.
    
- **Typy:**
    
    - _Paketový filtr (L3/L4):_ Kouká jen na IP a Porty (např. povol 80, zakaž 22).
        
    - _Aplikační brána (L7):_ Rozumí obsahu (např. "zablokuj Facebook", "nepouštěj viry").
        
    - **Fortinet / Cisco ASA:** Příklady fyzických firewallů (krabice v racku).
        

### E) Access Point (AP) – L1 / L2

- **Funkce:** "Switch bez drátů". Převádí data z kabelu na rádiový signál (WiFi).
    

### F) Koncové stanice – L7 (Aplikační vrstva)

- PC, Server, Tiskárna, Mobil.
    
- Pracují na všech 7 vrstvách OSI modelu (od kabelu až po aplikaci).
    

---

## 4. Technologie kabeláže (Fyzická vrstva)

Aby to fungovalo, musíme to něčím propojit.

### A) Optika (Fiber Optic)

- **Princip:** Přenáší světlo (fotony) skleněným nebo plastovým vláknem.
    
- **Výhody:**
    
    - Absolutní odolnost vůči elektrickému rušení.
        
    - Dosah desítky kilometrů.
        
    - Obrovské rychlosti (Tbps).
        
- **Použití:** Páteřní sítě, propojení budov, přívod internetu do domu (FTTH).
    

### B) Metalika (Twisted Pair - Kroucená dvojlinka)

- **Princip:** Měděné dráty. Jsou kroucené, aby se vyrušilo elektromagnetické rušení z okolí.
    
- **Typy:**
    
    - **UTP:** Nestíněný (doma).
        
    - **FTP / STP:** Stíněný (kolem silových kabelů, v továrně).
        
- **Kategorie (Rychlosti):**
    
    - **Cat 5e:** Zvládne **1 Gbit/s**. Frekvence 100 MHz. Dnes minimum.
        
    - **Cat 6:** Zvládne **10 Gbit/s** (na kratší vzdálenost). Frekvence 250 MHz.
        
    - **Cat 6a:** Plných 10 Gbit/s na 100m.
        
    - **Cat 7/8:** Pro datacentra.
        
- **Limit:** Metalika funguje spolehlivě max do **100 metrů**!
    

### Rychlosti v síti:

- **Fast Ethernet:** 100 Mbit/s (staré).
    
- **Gigabit Ethernet:** 1 000 Mbit/s (standard).
    
- **10 Gigabit Ethernet:** 10 000 Mbit/s (servery, páteře).
    

---

## 5. IP Adresy (Logická adresace)

Zatímco Switch zajímá MAC adresa (hardware), Router a aplikace potřebují IP adresu.

- **IPv4:** 32-bitové číslo (`192.168.1.1`).
    
    - _Subnetting:_ Pomocí masky sítě (`255.255.255.0`) dělíme adresu na část **SÍTĚ** (Network ID) a část **HOSTA** (konkrétní PC).
        
- **IPv6:** 128-bitové číslo (hexadecimální). Zavádí se, protože IPv4 došly.
    
- **DHCP (Dynamic Host Configuration Protocol):** Automaticky přiděluje IP adresy, masku, bránu a DNS zařízením v síti.
    

---

## 6. Zabezpečení sítě

Jak chránit síť před útokem?

1. **Fyzická bezpečnost:** Zamčená serverovna, kamery. Útočník se nesmí dostat ke kabelu.
    
2. **Port Security (na Switchi):**
    
    - Nastavím, že do portu č. 1 se může připojit jen PC s MAC adresou `XY`.
        
    - Když se tam připojí cizí notebook, switch port okamžitě vypne (shutdown).
        
3. **VLAN (Segmentace):** Rozdělení sítě na menší části. Vir z účtárny se nedostane do výrobní linky.
    
4. **Šifrování:**
    
    - WiFi: Používat WPA2 nebo WPA3 (nikdy ne WEP!).
        
    - Web: HTTPS.
        
5. **VPN (Virtual Private Network):** Šifrovaný tunel internetem. Umožňuje bezpečně pracovat z domova, jako bych seděl v kanceláři.









































# Síťové  Topologie (Struktura síťe)
- Topologie určuje, jak jsou zařízení v síti vzájemně propojena. Dělíme ji na fyzickou (jak vedou kabely) a logickou (jak tečou data)

![Topologie](./Obrazky/Navrh_LAN_siti/Topologie.jpeg)

## Typy topologií:

### Bus
- **Jak to vypadá:** Jeden hlavní kabel (páteř), kde kterému jsou připojeny všechny počítače.
- **Vlastnosti:** Dříve velmi efektivní a levná.
- **Nevýhody:** Pokud se hlavní kabel kdekoliv přeruší, celá síť přestane fungovat. Dnes se už v LAN sítích téměř nepoužívá  (zastaralé koaxiální kabely). 
### Line
- **Jak to vypadá:** Počítače jsou zapojeny za sebou.
- **Specifikum:** Každý počítač musí mít **dvě síťové karty** (jednou příjme, druhou pošle dál).
- **Nevýhody:** Přerušení jednoho článku přeruší spojení pro všechny za ním. 

### Ring
- **Jak to vypadá:** Počítače jsou propojeny do uzavřeného kruhu.  
- **Výhoda:** Signál cestuje jedním směrem a zesiluje se na každé stanici. Existují varianty (např. FDDI), kde 

- struktura sítě (star, mesh, bus, ring, tree, line, fully Connected)
	- ring výhoda že když přestane fungovat jedna cesta stále funguje
	- line/bus byl jeden z nejefektivnější ale když se přerušila cesta tak přestalo fungovat (v linu musí mít každý pc 2 karty)
	- mesh samostatné připojení neuspořádané rozpoložení (WIFI) obvykle město výhoda mohu přerušit polovinu a bude stálo fungovat, nevýhody drahá nepraktická 
	- hvězda nejlevnější n počítaču na jeden switch když se přruší jeden spojen spadne jeden pc ale když spadne switch tak všichni
	- tree každý prvek má minimálně 2 připojení taková namakaná star topologie
	- Otázka kdy při jaké příležitosti použijete jakou topologie
## síťové prvky
- zařízení: 
	- Router(L3), 
	- Switch(!!!(L2) nový moderní i L3)(propojení vzájemné v síti), představ jsi že každý port je jakoby ostrov a potřebuji tam dostat brigde ![Switch](./Obrazky/Navrh_LAN_siti/Switch_navrh.png)
		aplink porty
		Cam tabulka
		Vlany jsou L2 je jich (4 096)
	- Hub(L1) rozšiřuje pouze elektrický pulzy a duplikuje a odevzdají zbytku síti 
	- koncové stanice (tyhle zařízení pracují na všechny 7 vrstvách ) (pc, server),
	- Apečko(L1/L2),
	- Firewall (převážně ty první dvě L3/L4/L5) (fyzický firewall (Fortinet))
- Aktivní prvky potřebují napájení 
## ip adresy
## zabezpečení 
## rychlosti k
## technologie kabelu 
- (optika, cat 6, cat 5) typ kabeláže