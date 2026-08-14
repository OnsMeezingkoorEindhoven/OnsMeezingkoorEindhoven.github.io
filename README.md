# Koorwebsite — Quarto + GitHub Pages

Deze map bevat een complete starterwebsite voor een lokaal zangkoor. De site gebruikt **Quarto** om `.qmd`-bestanden om te zetten naar HTML en **GitHub Pages** voor gratis hosting.

## 1. Wat moet je als eerste aanpassen?

### `_variables.yml`
Hier staan vrijwel alle praktische gegevens op één plek:

- koornaam
- plaats
- repetitiedag en -tijd
- repetitielocatie
- e-mail en telefoon
- dirigent
- repertoire
- contributie

### `_quarto.yml`
Vervang hier op drie plaatsen `KOORNAAM` en in de beschrijving `PLAATSNAAM`.

### De inhoudspagina's
Pas vervolgens deze bestanden aan:

- `index.qmd` — homepage
- `over-ons.qmd` — verhaal, repertoire, dirigent
- `meezingen.qmd` — informatie voor potentiële leden
- `optredens.qmd` — komende en eerdere optredens
- `contact.qmd` — contactinformatie en sociale media

### Foto's
Zet foto's in `images/`. Zie `images/README.txt` voor voorbeelden.

---

## 2. Lokaal bekijken

Installeer Quarto vanaf de officiële Quarto-website en open deze map in VS Code of een andere editor.

Open een terminal in de projectmap en voer uit:

```bash
quarto preview
```

Quarto opent dan een lokale versie van de website in je browser. Als je een `.qmd`-bestand opslaat, wordt de preview automatisch bijgewerkt.

Stop de preview met `Ctrl+C`.

---

## 3. Nieuwe GitHub-repository maken

Maak op GitHub een nieuwe **public repository**, bijvoorbeeld:

```text
koorwebsite
```

Je hoeft bij het aanmaken geen README, `.gitignore` of licentie toe te voegen, want deze template bevat die bestanden al.

Open daarna een terminal in deze projectmap:

```bash
git init
git add .
git commit -m "Initial choir website"
git branch -M main
git remote add origin https://github.com/JOUW-GEBRUIKERSNAAM/koorwebsite.git
git push -u origin main
```

---

## 4. GitHub Pages inschakelen

De template bevat al `.github/workflows/publish.yml`. Die workflow:

1. installeert Quarto op GitHub;
2. voert `quarto render` uit;
3. uploadt de map `_site`;
4. publiceert die via GitHub Pages.

Ga na je eerste push op GitHub naar:

**Repository → Settings → Pages**

Kies bij **Build and deployment / Source**:

```text
GitHub Actions
```

Ga daarna naar het tabblad **Actions**. De workflow **Publish Quarto website** hoort automatisch te draaien. Bij een groene check is de site gepubliceerd.

De tijdelijke URL is normaal gesproken:

```text
https://JOUW-GEBRUIKERSNAAM.github.io/koorwebsite/
```

Vanaf nu is de workflow simpel:

```bash
git add .
git commit -m "Update website"
git push
```

Iedere push naar `main` bouwt en publiceert de website opnieuw.

---

## 5. Eigen `.nl`-domein koppelen

Doe dit pas nadat de GitHub Pages-URL werkt.

Stel dat je domein is:

```text
www.koornaam.nl
```

### Stap A — GitHub

Ga naar:

**Repository → Settings → Pages → Custom domain**

Vul in:

```text
www.koornaam.nl
```

### Stap B — DNS bij je domeinprovider

Maak voor `www` een CNAME-record:

```text
Type:   CNAME
Naam:   www
Waarde: JOUW-GEBRUIKERSNAAM.github.io
```

Let op: achter `github.io` komt **niet** `/koorwebsite`.

Voor het kale domein `koornaam.nl` kun je de actuele GitHub Pages A-records gebruiken. Controleer hiervoor altijd de actuele GitHub-documentatie onder *Managing a custom domain for your GitHub Pages site*.

Op het moment waarop deze template is gemaakt gebruikt GitHub Pages voor het apex-domein deze IPv4-adressen:

```text
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

Voeg dus vier A-records toe met naam `@`, tenzij je DNS-provider een ALIAS/ANAME-record naar `JOUW-GEBRUIKERSNAAM.github.io` ondersteunt.

DNS-wijzigingen kunnen enige tijd nodig hebben om overal zichtbaar te worden.

### Stap C — HTTPS

Wanneer GitHub de DNS-configuratie herkent, ga je opnieuw naar:

**Settings → Pages**

Schakel **Enforce HTTPS** in.

### Stap D — Quarto-configuratie

Open `_quarto.yml` en haal het commentaarteken weg bij:

```yaml
site-url: "https://www.jouwdomein.nl"
```

Vervang het domein door jullie echte domein, commit en push opnieuw.

---

## 6. Website vindbaar maken in Google

Als het eigen domein werkt:

1. voeg het domein toe aan Google Search Console;
2. laat Google de homepage inspecteren en vraag indexering aan;
3. zorg dat de woorden `zangkoor`, jullie plaatsnaam en de koornaam natuurlijk in de teksten voorkomen;
4. vul echte informatie in op `meezingen.qmd`;
5. voeg regelmatig nieuwe optredens toe.

Een nuttige zoekopdracht om te controleren of Google de site heeft opgenomen is:

```text
site:koornaam.nl
```

---

## 7. Een echte foto toevoegen

Voorbeeld: zet `groepsfoto.jpg` in de map `images/`.

Vervang daarna een placeholder in een `.qmd`-bestand door:

```markdown
![KOORNAAM tijdens een optreden in PLAATSNAAM](images/groepsfoto.jpg)
```

Voor de grote foto op de homepage kun je de placeholder vervangen door bijvoorbeeld:

```html
<img src="images/groepsfoto.jpg"
     alt="KOORNAAM uit PLAATSNAAM"
     class="hero-image">
```

en eventueel de styling verder aanpassen in `styles.css`.

---

## 8. Bestandsoverzicht

```text
koorwebsite/
├── _quarto.yml
├── _variables.yml
├── index.qmd
├── over-ons.qmd
├── meezingen.qmd
├── optredens.qmd
├── contact.qmd
├── styles.css
├── robots.txt
├── images/
│   └── README.txt
├── .gitignore
└── .github/
    └── workflows/
        └── publish.yml
```

## Belangrijkste dagelijkse workflow

Als de site eenmaal staat, hoef je meestal alleen nog `.qmd`-bestanden en foto's te wijzigen:

```bash
quarto preview
# wijzigingen maken en controleren

git add .
git commit -m "Add new concert"
git push
```

GitHub doet de rest automatisch.
