# familyOverview

Interaktívny finančný plán pre Milana a Terku — jedna statická stránka, hostovaná na GitHub Pages.

**Živá verzia:** https://milankubackam.github.io/familyOverview/

## Čo appka robí

- **Kam ide výplata** — mesačný sumár všetkých spoločných tokov v Kč aj v % z príjmu domácnosti
- **Bankové toky** — KB (izolovaný účet na bývanie) a Air Bank (všetko ostatné)
- **Air Bank obálky** — sporenie rozdelené podľa vlastníka (spoločné / Terka / Milan) s progresom voči cieľom
- **Nastavenia modelu** — spoločné výdavky, hypotéka, rezerva, spoločné investície, scenár dieťaťa, horizont
- **Projekcie** — vývoj majetku, mesačný prebytok, splácanie hypotéky
- **Osobné financie** — samostatné stĺpce pre Milana a Terku, každý s vlastným zoznamom investícií
- **Odporúčania** — automatická kontrola optimalizácie; každý návrh je overený simuláciou, takže sa ponúkne len zmena, ktorá problém reálne odstráni

## Ako funguje ukladanie

Hodnoty sú v `data.json` v tomto repozitári — to je zdieľaný stav, ktorý sa načíta pri každom otvorení stránky, takže **na všetkých zariadeniach vidíte to isté**.

Po úprave hodnôt sa v hlavičke objaví „Neuložené zmeny". Tlačidlo **☁ Uložiť pre všetkých** commitne nový `data.json` cez GitHub API. Na to je potrebný fine-grained token s oprávnením `Contents: Read and write` na tento repozitár — zadáva sa raz cez tlačidlo **🔑 Token** a uloží sa len do `localStorage` daného prehliadača. Token nie je a nesmie byť súčasťou repozitára.

Ďalšie tlačidlá:

- **↺ Načítať zdieľané** — zahodí lokálne zmeny a načíta aktuálny `data.json`
- **⭳ Do súboru / ⭱ Zo súboru** — export a import stavu ako JSON (záloha alebo prenos bez tokenu)

Ak stránku zavriete s neuloženými zmenami, prehliadač ich podrží ako rozpracovaný stav a pri ďalšom otvorení na to upozorní.

Pri ukladaní sa kontroluje, či medzitým niekto neuložil novšiu verziu — ak áno, appka sa spýta pred prepísaním.

## Súbory

| Súbor | Popis |
|---|---|
| `index.html` | celá aplikácia (HTML + CSS + JS v jednom súbore, bez závislostí) |
| `data.json` | zdieľané hodnoty |
| `robots.txt`, `noindex` meta | stránka je vylúčená z indexovania vyhľadávačmi |
| `.nojekyll` | vypnutie Jekyll spracovania na GitHub Pages |

## Poznámka k súkromiu

Stránka je verejne dostupná na internete a `data.json` obsahuje reálne finančné údaje. `robots.txt` a `noindex` zabránia indexovaniu vyhľadávačmi, ale nie prístupu — kto pozná URL, obsah uvidí. Ak by ste to chceli zmeniť, jediné skutočné riešenia sú anonymizovať `data.json` alebo appku prevádzkovať mimo verejného hostingu.

## Poznámka k modelu

Výnosy sú nominálne a konštantné, dane z výnosov ETF sa nemodelujú (v ČR platí 3-ročný časový test). Nie je to licencované finančné poradenstvo — je to plánovací nástroj.
