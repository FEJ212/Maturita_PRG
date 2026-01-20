
- Funkce jsou deklarovány jako datový typ (např. matematické), pro následující využívání ve skriptech. To znamená, že se může používat jako entity první třídy (můžou mít jméno, využity jako argumenty či parametry, nebo můžou být výsledkem returnu jiné funkce. Ve zkratce, lze s nimi zacházet identicky jako s datovými typy. Je to DEKLARATIVNÍ programování. Deklarativní – CO se má udělat (imperativní – jak se to má udělat) Pro lepší pochopení, u funkcionálního programováni popisuji CÍL, mezitím co program (interpret) daného jazyka vyřeší zbytek.

- Je využívána funkce Lambda – „anonymní funkce“, která se nikde přímo nedeklaruje, ale je „deklarovaná“ přímo tam, kde se používá, pomocí syntaxe  např. func  => x*x. Kvůli tomuto způsobu zápisu se Lambda funkce využívá nejlépe u funkcí, které se využijí třeba jen jednou, pro lehčí a rychlejší chod programu, žádné jiné výhody nemá a kdekoliv je využita Lambda funkce tak by mohla fungovat i normální deklarovaná.

- Funkcionální programování je převážně akademicky než komerčně, což znamená, že se nikde nějak přímo nevyužívá, spíš jen na jednoduché výpočty. Hodí se převážně pro práci s daty, statistiky, analýzy či machine learning.

- Je pár programovacích jazyků přímo dedikovány pro funkcionální programování – Common Lisp, Haskell, Scheme a spoustu dalších.

- Haskell – 1990, Plná podpora práce se soubory i standardními vstupy a výstupy,  disponuje klasickými číselnými datovými typy, seznamy, obsahuje funkce pro práci se seznamy, a byl prvním jazykem který vymyslel typové třídy. Využívá se převážně v bankovnictví. Nemá žádné „vedlejší účinky“ spouštění funkcí, takže je považován za „čistou formu“ funkcionálního programování, kde jde jen čistě o to, co chceme vypočítat.