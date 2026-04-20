# Schnipseljagd

Interaktive Web-App für eine 5-Stationen-Schatzsuche · 02.05.2026

## Deployment (GitHub Pages)

1. Repository auf GitHub erstellen (z.B. `schnipseljagd`)
2. `index.html` hochladen (Upload-Button oder `git push`)
3. Repository → Settings → Pages → Source: **Deploy from branch** → Branch: `main` → `/root` → Save
4. Nach ~2 Minuten erreichbar unter: `https://[dein-username].github.io/schnipseljagd`

## Lokale Nutzung

Datei `index.html` direkt im Browser öffnen — kein Server nötig.

## Organisator-Zugang

PIN: Im Code in der Konstante `PIN` definiert (Standard: Geburtsjahr der Geburtstagskind).

## Auf GitHub Pages deployen

```bash
git remote add origin https://github.com/USERNAME/schnipseljagd.git
git push -u origin main
```

Dann in den Repository-Einstellungen: Settings → Pages → Branch: main → Save.
