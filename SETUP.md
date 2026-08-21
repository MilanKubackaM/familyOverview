# Nasadenie familyOverview na GitHub Pages

Tento balík obsahuje hotovú statickú aplikáciu. Úlohou je dostať ju do repozitára
`https://github.com/MilanKubackaM/familyOverview.git` a zapnúť GitHub Pages.

## Obsah balíka

| Súbor | Popis |
|---|---|
| `index.html` | celá aplikácia (HTML + CSS + JS v jednom súbore, žiadne závislosti) |
| `data.json` | zdieľaný stav — hodnoty, ktoré appka načíta pri každom otvorení |
| `README.md` | dokumentácia projektu |
| `robots.txt` | vylúčenie z indexovania vyhľadávačmi |
| `.nojekyll` | vypnutie Jekyll spracovania na GitHub Pages |
| `SETUP.md` | tento súbor |

## Postup

1. **Cieľová zložka na disku:** `/Users/milan/Documents/Repositories/familyOverview`
   Súbory z balíka rozbaliť priamo do nej (nie do podzložky).

2. **Inicializovať git a pushnúť** na branch `main`.
   Token na push dodá Milan v chate — použiť ho iba jednorazovo v push URL,
   **nikdy ho nezapisovať do žiadneho súboru v repozitári** ani do `.git/config`:

   ```bash
   cd /Users/milan/Documents/Repositories/familyOverview
   git init
   git branch -M main
   git remote add origin https://github.com/MilanKubackaM/familyOverview.git
   git add -A
   git commit -m "Interaktívny finančný plán — appka, zdieľaný stav v data.json"
   git push https://x-access-token:<TOKEN>@github.com/MilanKubackaM/familyOverview.git main
   ```

   Ak repozitár už obsahuje commity, najprv `git pull --rebase origin main`.

3. **Repozitár musí byť public** — GitHub Pages z privátneho repa vyžaduje platený plán.
   Prepnutie viditeľnosti token neumožňuje, spraví to Milan v `Settings → General → Danger Zone`.

4. **Zapnúť GitHub Pages** — buď cez API (ak token má oprávnenie `Pages: write`):

   ```bash
   curl -X POST -H "Authorization: Bearer <TOKEN>" \
     -H "Accept: application/vnd.github+json" \
     https://api.github.com/repos/MilanKubackaM/familyOverview/pages \
     -d '{"source":{"branch":"main","path":"/"}}'
   ```

   alebo manuálne: `Settings → Pages → Source: Deploy from a branch → main → / (root) → Save`.

5. **Overiť**, že stránka beží na `https://milankubackam.github.io/familyOverview/`
   (prvý build trvá 1–3 minúty) a že sa v hlavičke zobrazí zelené
   „Zdieľané hodnoty (uložené …)" — to znamená, že sa `data.json` načítal správne.

## Ako appka ukladá dáta

Zdieľaný stav je `data.json` v repozitári. Appka ho načíta pri každom otvorení, takže
všetky zariadenia vidia to isté. Po úprave hodnôt sa objaví „Neuložené zmeny" a tlačidlo
**☁ Uložiť pre všetkých** commitne nový `data.json` cez GitHub API — na to si Milan zadá
token raz priamo v appke (tlačidlo **🔑 Token**), uloží sa len do `localStorage` prehliadača.

Ak sa neskôr menia veci v appke, upravuje sa `index.html`; `data.json` prepisuje appka sama.

## Bezpečnostná poznámka

Stránka je verejne dostupná a `data.json` obsahuje reálne finančné údaje
(príjmy, hypotéka, zostatky účtov). `robots.txt` a `noindex` meta zabránia indexovaniu
vyhľadávačmi, nie však prístupu — kto pozná URL, obsah uvidí.
