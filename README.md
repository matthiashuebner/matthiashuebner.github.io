# matthiashuebner.com

Nachbau der Visitenkarten-Seite `matthiashuebner.com` als reine statische
HTML/CSS-Seite – ohne Cloudflare-E-Mail-Obfuskierung, ohne Server-Logik,
direkt deploybar auf GitHub Pages.

## Struktur

```
.
├── index.html                              # Einstiegsseite
├── .nojekyll                               # GitHub Pages: Jekyll deaktivieren (Ordner mit "About..." bleiben sichtbar)
├── AboutPageAssets/
│   ├── styles/aboutPageStyle.css           # Original-Stylesheet, leicht aufgeräumt
│   └── images/
│       ├── teamslogo.png
│       ├── outlooklogo.png
│       └── In-White-34.png                 # LinkedIn-Icon
└── README.md
```

## Lokal ansehen

```bash
# Einfachster Weg
python3 -m http.server 8080
# dann http://localhost:8080 öffnen
```

## Veröffentlichen auf GitHub Pages

### Variante A — User-Site unter `https://<user>.github.io`

1. Auf GitHub ein Repository namens `<user>.github.io` anlegen
   (z. B. `matthiashuebner.github.io`).
2. In diesem Ordner:
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin git@github.com:<user>/<user>.github.io.git
   git push -u origin main
   ```
3. In den Repo-Settings → **Pages** → Source: `Deploy from a branch`,
   Branch: `main` / `/ (root)` auswählen.
4. Nach ~1 Minute ist die Seite unter `https://<user>.github.io` live.

### Variante B — Project-Site unter `https://<user>.github.io/<repo>`

Beliebigen Repo-Namen verwenden und unter Settings → Pages denselben
Branch/Ordner aktivieren. URL wird dann `https://<user>.github.io/<repo>/`.

### Eigene Domain (matthiashuebner.com)

1. Datei `CNAME` mit Inhalt `matthiashuebner.com` ins Repo-Root legen
   (oder in Pages-Settings → "Custom domain" eintragen, dann legt GitHub
   sie selbst an).
2. Beim DNS-Provider folgende Einträge setzen:
   - `A` `@` → `185.199.108.153`
   - `A` `@` → `185.199.109.153`
   - `A` `@` → `185.199.110.153`
   - `A` `@` → `185.199.111.153`
   - `CNAME` `www` → `<user>.github.io.`
3. In den Pages-Settings „Enforce HTTPS" aktivieren, sobald GitHub das Zertifikat ausgestellt hat.

## Was wurde gegenüber dem Original geändert?

- Cloudflare-`__cf_email__`-Verschleierung entfernt – E-Mail steht jetzt
  als normaler `mailto:`-Link (`info@matthiashuebner.com`).
- Eingebettete Cloudflare-Analytics-/Challenge-Scripts entfernt.
- Veralteter Adobe-Edge-Web-Fonts-Loader durch `<link>` auf Google Fonts
  ersetzt (Montserrat + Source Sans Pro), so wie das CSS sie ohnehin
  erwartet.
- Kleinere HTML-Aufräumarbeiten (`lang="de"`, valides Markup,
  Meta-Description, ARIA-Labels für die Icon-Links).
- Inhalte 1:1 übernommen.
