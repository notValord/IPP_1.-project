## Implementačná dokumentácia k 1. úlohe do IPP 2021/2022
#### Meno a priezvisko: Veronika Molnárová
#### Login: xmolna08

---

### Popis projektu
Cieľom projektu bolo vytvoriť program na lexikálnu a syntaktickú analýzu jazyka IPPcode22. Program bere kód zo štandardného vstupu a vracia na výstupe jeho XML reprezentáciu.
V prípade nastania chyby je vypísaná chybová hláška a vrátená odpovedajúca návratová hodnota. 
Program je možné spustiť s argumentom *--help*, kedy neprebieha žiadna analýza kódu.

### Lexikálna analýza

Pre potreby lexikálnej analýzy bola vytvorená štruktúra tokenu, ktorá obsahuje svoj typ a hodnotu. Typy tokenov môžu byť EOL, EOF, VAR, CONST a OTHER, všetky typy okrem EOL a EOF si so sebou nesú aj svoju hodnotu.
Pre získanie tokenov je volaná funkcia *get_token()*, ktorá simuluje končný automat. Postupne bere zo vstupu jednotlivé znaky, pokým neprečíta celý token. Komentáre a postupnosti bielych znakov sú odstraňované. V prípade nasledovania dvoch tokenov bezprostredne za sebou, je druhý token v poradí dočasne uložený v globálnej premennej *save* a navrátený v nasledujúcom tokene. Lexikálna kontrola sa vykonáva s využitím regexov.

### Syntaktická analýza
Pre jednoduchú syntax sme implementovali syntaktický strom, ktorý pozostáva z troch neterminálov, START, ktorý očakáva hlavičku ako prvý príklaz programu, nasledovanou postupnosťou INSTRUC a EOL neterminálov, kedy na jednom riadku je povolená maximálne jedna inštrukcia. Prebieha kontrola jednotlivých typov operačných kódov spoločne s ich argumentmi. Derivácia stromu sa vykonáva pokým sa nenarazí na EOF token.

### Generácia XML výstupu
Na tvorbu výstupného dokumentu bola využitá knižnica DOM, ktorá tvorí štruktúru XML dokumentu. Po uspešnej analýze je na výstup vypísaná vytvorená štruktúra.
