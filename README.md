# FMechanik Website

Landingpage fuer **FMechanik Meisterwerkstatt** (`www.fmechanik.de`) mit:

- Deutscher Startseite
- Kombinierter Seite fuer `Impressum & Datenschutz`
- Cloudflare Pages kompatibler Struktur
- Einfach austauschbaren Platzhaltern fuer Logo/Favicon

## Struktur

- `index.html` Hauptseite
- `rechtliches/index.html` Impressum + Datenschutz
- `styles.css` Design und responsive Layout
- `assets/logo.svg` Logo-Platzhalter (einfach ersetzen)
- `assets/favicon.svg` Favicon-Platzhalter (einfach ersetzen)
- `assets/werkstatt-aussen.png` Werkstattfoto
- `assets/reifen-service.png` Reifenservicefoto
- `assets/bremsen-service.png` Bremsenservicefoto
- `_headers` Security Header fuer Cloudflare Pages
- `_redirects` Weiterleitungen `/impressum` und `/datenschutz`

## Logo/Favicon ersetzen

Nur diese Dateien austauschen:

- `assets/logo.svg`
- `assets/favicon.svg`

Dateinamen gleich lassen, dann sind keine Codeaenderungen noetig.

## Lokale Vorschau

```powershell
python -m http.server 8080
```

Dann `http://localhost:8080` oeffnen.

## Git-basiertes Auto-Deploy (GitHub Actions -> Cloudflare Pages)

Die Datei `.github/workflows/cloudflare-pages.yml` deployt automatisch:

- `push` auf `main` -> Production Deploy
- `pull_request` -> Preview Deploy

Noetige GitHub Repository Secrets:

- `CLOUDFLARE_ACCOUNT_ID`
- `CLOUDFLARE_API_TOKEN`

Cloudflare API Token (minimal):

- Account permission: `Pages Write`
- Account scope: dein Cloudflare Account

Danach in GitHub:

1. `Settings` -> `Secrets and variables` -> `Actions`
2. Beide Secrets anlegen
3. Commit nach `main` pushen
4. Unter `Actions` den Workflow `Deploy to Cloudflare Pages` pruefen

Damit ist ein voll git-getriebener Deploy-Flow aktiv, auch wenn die native Cloudflare-Git-Integration aktuell Fehler wirft.

## DNS Setup (ohne Nameserver-Wechsel)

1. In Cloudflare Pages nur `www.fmechanik.de` als Custom Domain verbinden.
2. Beim aktuellen DNS-Provider:
   - `CNAME` `www` -> `fmechanik-website.pages.dev`
   - Domain-Weiterleitung (301) `fmechanik.de` -> `https://www.fmechanik.de`
3. Bestehende Mail-Records (MX, SPF, DKIM, DMARC) unveraendert lassen.
