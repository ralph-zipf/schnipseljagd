# Schnipseljagd-App – Design-Dokument
*2026-04-19*

## Überblick

Interaktive Web-App für eine 5-Stationen-Schatzsuche (02.05.2026, Dachau/München) zum Geburtstag. Zwei Modi: Spieler (Rätsel lösen, Münze aufbauen) und Organisator (Lösungen, Checkliste, Druck).

## Technische Architektur

- **Format:** Einzelne `index.html` (HTML + CSS + JS eingebettet), kein Build-Schritt
- **State:** `localStorage` – Fortschritt bleibt bei Seitenreload erhalten
- **Deployment:** GitHub Pages (1 Datei hochladen → URL teilen)
- **Kompatibilität:** Mobile-first, Safari iOS + Chrome Android

## Design

- **Stil:** Arcane (Netflix) – dunkelblau/lila Hintergrund, gold/bronze Akzente, Hextech-Leuchten, Cinzel-Schrift
- **Layout:** Hero (Münz-Puzzle) + scrollbare Stations-Liste → Detail-Ansicht
- **Münze:** SVG-Reiterstandbild Kurfürst Maximilian I, in 5 unregelmäßige Scherben gebrochen, Arcane-Stil

## Spieler-Modus (Standard)

- Münz-Puzzle oben: 5 Scherben, erscheinen in zufälliger Reihenfolge beim Lösen
- 5 Stations-Karten mit Status (gesperrt / aktiv / gelöst)
- Station-Detail: Rätseltext (wie auf Karte), Eingabefeld, "Lösung prüfen"-Button
- Richtig → Scherbe leuchtet auf, nächste Station wird freigeschaltet
- Falsch → Hinweis-Feedback, optional ein Tipp

## Organisator-Modus (PIN-geschützt)

- Zugang: Lock-Icon unten rechts → 4-stelliger PIN (festgelegt in der Datei)
- Zeigt: alle Stationen inkl. gesperrte, Mechanismus-Erklärung, Lösung im Klartext
- Vigenère-Geheimtext: wird automatisch berechnet (Schlüssel DZAG, Klartext KURFUERSTMAXIMILIAN)
- Checkliste Vorbereitung (5–8 Punkte, abhakbar, persistent in localStorage)
- Druck-Ansicht: jede Rätselkarte als sauber formatierter Ausdruck (print-CSS)

## Die 5 Rätsel

| # | Ort | Mechanismus | Lösung | Scherbe |
|---|-----|-------------|--------|---------|
| 1 | Zuhause | Caesar-Chiffre (Shift 23, Quersumme 1985) | DACHAU | Shard 3 |
| 2 | Dachauer Altstadt, Untermarkt | Telefon-Tastatur-Chiffre (T9 +4) | ZAUNKOENIG | Shard 1 |
| 3 | Café Zaunkönig | Steganographie (Anfangsbuchstaben) | AMPERBRUECKE | Shard 5 |
| 4 | Amperbrücke Mitterndorf | Mathe → Alphabet (A=1) | GELATO | Shard 2 |
| 5 | La Veneziana Eisdiele | Vigenère (Schlüssel DZAG) | KURFUERSTMAXIMILIAN | Shard 4 |

Shard-Reihenfolge bewusst zufällig (nicht 1→2→3→4→5), damit die Münze sich nicht offensichtlich aufbaut.

## Vigenère-Berechnung (Station 5)

- Schlüssel: DZAG (Anfangsbuchstaben der 4 Vorgänger-Lösungen: **D**achau, **Z**aunkoenig, **A**mperbruecke, **G**elato)
- Klartext: KURFUERSTMAXIMILIAN (18 Zeichen, Schlüssel rotierend)
- Geheimtext: wird in der App automatisch berechnet und angezeigt

## Daten-Struktur (JavaScript)

```js
const STATIONS = [
  { id: 1, ort: "Zuhause", titel: "Der Geburts-Code", mechanismus: "Caesar-Chiffre",
    rätseltext: "...", lösung: "DACHAU", hinweis: "...", shard: 3 },
  // ...
];
const PIN = "1985"; // Geburtsjahr als PIN
```

## Checkliste Vorbereitung

1. Rätselkarten drucken (5 Stück)
2. Rätselkarten laminieren oder in Hülle
3. Station 1 vorbereiten (Zuhause)
4. Schnipsel an Station 2–5 deponieren
5. App-URL an eigenes Handy schicken
6. PIN merken
7. Backup: Lösungen als Screenshot
8. Reservierung La Trattoria by Giovanni bestätigen

## GitHub Pages Deployment

1. Repository erstellen (z.B. `schnipseljagd`)
2. `index.html` hochladen
3. Settings → Pages → Branch: main → Speichern
4. URL: `https://[username].github.io/schnipseljagd`
