# Website van het koor

## Voor de beheerder

**Je hoeft geen programma te installeren en je hoeft de technische bestanden niet te begrijpen.**

Gebruik alleen:

- `BEWERK-HIER/ALGEMENE-GEGEVENS.yml` — naam, plaats, repetities, contact, contributie enz.
- `BEWERK-HIER/_OVER-ONS.qmd` — tekst over het koor en de dirigent
- `BEWERK-HIER/_OPTREDENS.qmd` — concertagenda en archief
- `BEWERK-HIER/_MEEZINGEN-EXTRA.qmd` — optionele extra informatie voor nieuwe leden
- `images/` — foto's

In `BEWERK-HIER/START-HIER.txt` staat een korte stap-voor-stap handleiding.

### Tekst aanpassen via GitHub

1. Open het gewenste bestand op github.com.
2. Klik rechtsboven op het potloodje.
3. Pas de tekst aan.
4. Klik op **Commit changes**.
5. De website wordt automatisch opnieuw gepubliceerd.

### Foto's

De website gebruikt vaste bestandsnamen. Vervang zo nodig:

- `images/groepsfoto.jpg`
- `images/dirigent.jpg`
- `images/galerij-1.jpg`
- `images/galerij-2.jpg`
- `images/galerij-3.jpg`

Door dezelfde bestandsnamen te behouden hoef je nergens code aan te passen.

## Voor technisch beheer

De website wordt met Quarto gebouwd via `.github/workflows/publish.yml` en gepubliceerd naar GitHub Pages. Tijdens de GitHub Action wordt `BEWERK-HIER/ALGEMENE-GEGEVENS.yml` gekopieerd naar Quarto's `_variables.yml` voordat `quarto render` wordt uitgevoerd.
