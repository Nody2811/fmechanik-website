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

## DNS Setup (ohne Nameserver-Wechsel)

1. In Cloudflare Pages nur `www.fmechanik.de` als Custom Domain verbinden.
2. Beim aktuellen DNS-Provider:
   - `CNAME` `www` -> `fmechanik-website.pages.dev`
   - Domain-Weiterleitung (301) `fmechanik.de` -> `https://www.fmechanik.de`
3. Bestehende Mail-Records (MX, SPF, DKIM, DMARC) unveraendert lassen.
