# Projekt: Schnipseljagd

## Was ist das?

Interaktive Web-App für eine 5-Stationen-Schatzsuche zum Geburtstag (02.05.2026, Dachau/München). Zwei Modi: Spieler (Rätsel lösen, Münze aufbauen) und Organisator (PIN-geschützt, zeigt Lösungen + Checkliste). Alles in einer einzigen `index.html`.

## Ordnerstruktur

```
Schnipseljagt/
├── CLAUDE.md                    ← diese Datei
├── README.md                    ← Deployment-Anleitung
├── index.html                   ← die komplette App (HTML + CSS + JS)
├── Kurfürst_Maximilian_Münze.png ← Münzbild (RGBA, 2380×1290px)
├── _preview_coin.html           ← Standalone-Vorschau für Coin-Design-Iteration
└── docs/
    └── superpowers/
        ├── plans/               ← Implementierungsplan
        └── specs/               ← Design-Dokument
```

## Technische Architektur

- **Format:** Einzelne `index.html`, kein Framework, kein Build-Schritt
- **State:** `localStorage` mit Key `schnipseljagd_v1`
- **Deployment:** GitHub Pages (1 Datei hochladen, URL teilen)
- **Kompatibilität:** Mobile-first, Safari iOS + Chrome Android

## Design

- **Stil:** Arcane (Netflix) – dunkelblau/lila, Bronze/Gold-Akzente, Cinzel-Schrift
- **Münze:** Echtes PNG-Foto (Kurfürst Maximilian I.), in 5 Scherben gebrochen, Arcane-Bronze-Filter, zackige Risslinien
- **SVG-Technik:** Einzelnes SVG mit verschachtelten clipPaths; PNG-Transparenz für Freistellung; kein CSS `filter:drop-shadow` (verursacht goldenen Halo)

## Spielmechanik

- 5 Stationen, sequenziell freigeschaltet
- Jede gelöste Station enthüllt eine Münzscherbe (in zufälliger Reihenfolge: `SHARD_MAP = {1:3, 2:1, 3:5, 4:2, 5:4}`)
- `PIN = '1985'` (Geburtsjahr) für Organisator-Modus

## Die 5 Rätsel

| # | Ort | Mechanismus | Lösung | Scherbe |
|---|-----|-------------|--------|---------|
| 1 | Zuhause | Caesar-Chiffre (Shift 23) | DACHAU | 3 |
| 2 | Dachauer Altstadt, Untermarkt | Telefon-Tastatur T9 | ZAUNKOENIG | 1 |
| 3 | Café Zaunkönig | Anfangsbuchstaben-Steganographie | AMPERBRUECKE | 5 |
| 4 | Amperbrücke Mitterndorf | Mathe → Alphabet (A=1) | GELATO | 2 |
| 5 | La Veneziana Eisdiele | Vigenère (Schlüssel DZAG) | KURFUERSTMAXIMILIAN | 4 |

Vigenère-Schlüssel DZAG = Anfangsbuchstaben der 4 Vorgänger-Lösungen.

## Wie gearbeitet werden soll

- Coin-Design-Änderungen immer zuerst in `_preview_coin.html` testen, dann in `index.html` übertragen
- PNG-Messung: Münzzentrum (1189.5, 644.5), Radius 644px; SVG-Mapping: scale=97/644≈0.1506, image x=-79 y=3 width=358 height=194
- Bei Änderungen an der Münze: CSS `filter:drop-shadow` auf `.coin-stage` vermeiden → `box-shadow` verwenden

## Wichtige JS-Konstanten

```js
const PIN = '1985';
const SHARD_MAP = {1:3, 2:1, 3:5, 4:2, 5:4};
const VIG_KEY = 'DZAG';
const VIG_CIPHER = 'NTRLXDRYWLADLLIRLZN';
const STATE_KEY = 'schnipseljagd_v1';
```
