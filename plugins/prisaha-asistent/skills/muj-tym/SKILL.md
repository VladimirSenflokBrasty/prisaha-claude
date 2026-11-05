---
name: muj-tym
description: Představ uživateli jeho AI tým Přísahy (kdo je kdo a s čím pomáhá), odpověz na otázky typu „Jaký mám tým?“ nebo „Komu to mám zadat?“ a vysvětli, jak oslovit konkrétního člena @Jménem. Použij také pro dotaz, co tým dnes dělal.
---

Použij nástroje připojené aplikace Přísahy (klient je může zobrazit s prefixem připojení). Tým jsou skuteční serveroví AI pracovníci aplikace. Nehraj je sám v odpovědi a nevydávej svou okamžitou odpověď za práci týmu.

## Kdo je v týmu

- Seznam členů vždy načti `app_team_roster()`, nikdy ho neskládej z paměti ani z tohoto návodu. Tým se může změnit.
- Odpověz lidsky: jméno, čím se zabývá (role) a jedna věta, s čím pomůže. Seskup je srozumitelně, například:
  - **koordinace:** Jana rozděluje vaši práci, Daniel témata, Jan vede sledování zpráv;
  - **rešerše a analýza:** ověřování zdrojů, souvislosti, data;
  - **obsah a komunikace:** čeština, marketing, program;
  - **odborné pohledy:** Senát, dopad na občany, krizové situace, média;
  - **nezávislá kontrola:** Viktor.
- Řekni, že bez oslovení práci rozdělí Jana. Viktor nezávisle kontroluje každý výsledek a práci mu zadat nelze.
- Interní klíče rolí, modely ani technické údaje senátorovi nečti.

## Komu co zadat

Doporuč člena podle popisu role z `app_team_roster`, ne podle odhadu. Typicky:

- **Filip:** příspěvky a jak o věci mluvit.
- **Lucie:** čísla a výpočty.
- **David:** Senát a legislativa.
- **Petra:** program Přísahy.
- **Tomáš:** ověření tvrzení.
- **Tereza:** dopad na občany.
- **Martin:** krizová situace.
- **Klára:** srozumitelnost textu.
- **Irena:** znalosti a jejich historie.

Když si uživatel neví rady, nech to na Janě (zadání bez oslovení).

## Oslovení konkrétního člena

- Oslovení se píše přímo do textu zadání nebo navazující zprávy: `@Filip přeformuluj tento příspěvek pro Facebook`. Jméno musí odpovídat členovi ze seznamu, diakritika ani velikost písmen nevadí.
- Oslovený je hlavní řešitel. Jana mu přidělí hlavní část, ostatní pomohou a výsledek stejně projde ověřením zdrojů a nezávislou kontrolou.
- Více jmen: první je hlavní řešitel, další se přizvou.
- Navazující zprávy bez oslovení zůstávají u naposledy osloveného. `@tým` vrátí práci celému týmu pod Janinou koordinací.
- `@Viktor` samotného aplikace odmítne. Vysvětli to jednou větou a nabídni jiného člena.
- Zadání a pokračování dělej postupem `prace-s-tymem` (`app_work_create`, `app_work_follow`). Odpověď aplikace obsahuje `addressee`; potvrď uživateli, komu zadání skutečně šlo.
- Podpis „Jméno · role“ u výsledku znamená, že hlavní práci doložitelně udělal tento člen. Bez podpisu výsledek dodal tým. Podpis nedomýšlej.

## Co tým dělal

Na dotaz „co tým dnes dělal“ nebo „proč moje zadání čeká“ použij `app_team_monitoring(filters)`. Shrň jen skutečné výsledky a čekání srozumitelnými větami. Chybějící záznam neznamená nečinnost. Podrobný audit (`app_team_task`) otevírej jen na výslovnou žádost.
