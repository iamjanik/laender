# 🌍 Länder

Interaktive deutschsprachige Übersicht aller Staaten der Erde mit Lernkarten-Funktion.

## Dateien

| Datei | Inhalt |
|---|---|
| `index.html` | HTML-Struktur, alle Styles (`<style>`), Anti-FOUC-Snippet, gesamte App-Logik (`<script>`) |
| `laender.json` | Länderdaten (Land, Hauptstadt, Kontinent, Fläche, Bevölkerung, UN-Status, Fakt) |

## Starten

Lokaler Server erforderlich (wegen `fetch()` für `laender.json`):

```bash
npx serve .
```

Dann im Browser: `http://localhost:3000`

> **Hinweis:** Die App funktioniert nicht über `file://` – nur über einen lokalen HTTP-Server.

---

## Wo was ändern

**Farben, Dark Mode, Layout** → `index.html`, `<style>`-Block  
CSS-Variablen stehen ganz oben in `:root { }` (Light) und `:root[data-theme="dark"] { }` (Dark).

**Länderdaten** → `laender.json`  
Jeder Eintrag kann folgende Felder haben:

| Feld | Pflicht | Beschreibung |
|---|---|---|
| `Land` | ✅ | Ländername (deutsch) |
| `Hauptstadt` | ✅ | Hauptstadt(städte), mehrere mit `\n` getrennt |
| `Kontinent` | ✅ | `Afrika`, `Amerika`, `Asien`, `Europa`, `Ozeanien` |
| `Fläche` | ✅ | Fläche als formatierter String, z. B. `„357.114 km²"` |
| `Bevölkerung` | ✅ | Bevölkerung als formatierter String, z. B. `„ca. 84 Mio."` |
| `UNStatus` | optional | `nicht_anerkannt` / `beobachter` / `teilweise_anerkannt` |
| `UNStatusText` | optional | Erklärungstext zum UN-Status (erscheint in der Karte) |
| `UNHinweis` | optional | `true`, wenn ein zusätzlicher Hinweis angezeigt werden soll |
| `UNHinweisText` | optional | Text für den Hinweisblock |
| `Fakt` | optional | „Wusstest du?"-Fakt (erscheint grün hinterlegt in der Karte) |

**Logik, Flashcards, Rendering** → `index.html`, `<script>`-Block  
- `FLAGS` – Emoji-Flags-Map (Ländername → Emoji)
- `UN_CFG` – Konfiguration der drei UN-Status-Typen (CSS-Klassen, Icons, Labels)
- `renderList()` – Hauptliste neu aufbauen (mit Alphabettrennern)
- `buildCard()` – einzelne Länderkarte erzeugen
- `renderStart()` / `renderCard()` / `renderReveal()` / `renderType()` / `renderResult()` – Flashcard-Zustände

---

## Features

### Übersicht
- **Filtert nach Kontinent** (Afrika, Amerika, Asien, Europa, Ozeanien)
- **Filtert nach UN-Status** (Mitglied, Beobachter, teilweise anerkannt, nicht anerkannt)
- **Suche** nach Land oder Hauptstadt (Desktop: Inline im Header; Mobil: aufklappbares Suchfeld)
- **Alphabetische Trenner** mit Anzahl der Staaten pro Buchstabe
- **Ergebnis-Pill** zeigt gefilterte Anzahl / Gesamtzahl
- **Alle Karten auf-/zuklappen** (Button reagiert auf individuellen Kartenzustand)
- **Dark Mode** – automatisch per `prefers-color-scheme`, manuell umschaltbar, persistiert in `localStorage`

### Länderkarte
- Emoji-Flagge, Ländername, Kontinent-Tag
- Farbiger Rahmen und Dot bei besonderem UN-Status
- Felder: Hauptstadt, Bevölkerung, Fläche
- UN-Status-Block mit Erklärungstext (wenn vorhanden)
- Optionaler Hinweis-Block
- „💡 Wusstest du?"-Fakt (grün hinterlegt, wenn vorhanden)

### Lernkarten (Flashcard-Modus)
- **Aufdecken-Modus**: Hauptstadt anzeigen, dann „Gewusst" / „Nicht gewusst"
- **Eingabe-Modus**: Hauptstadt eintippen, Tipp-Toleranz bei Schreibvarianten
- Filterbar nach **Anfangsbuchstabe** (A–Z, mit Bereichsauswahl per Range-Button)
- Filterbar nach **Kontinent**
- Zufällige Reihenfolge (Shuffle)
- Ergebnisscreen mit Fehler-Liste am Ende

---

## UN-Status-System

Staaten ohne `UNStatus`-Feld gelten als vollständige UN-Mitglieder (keine besondere Markierung).

| Wert | Bedeutung | Farbe |
|---|---|---|
| `nicht_anerkannt` | Nicht oder kaum international anerkannt | Orange |
| `beobachter` | UN-Beobachterstaat (z. B. Vatikanstadt) | Blau |
| `teilweise_anerkannt` | Von einem Teil der UN-Staaten anerkannt | Gelb |

---

## Datengrundlage

Alle Daten basieren auf der [Liste der Staaten der Erde](https://de.wikipedia.org/wiki/Liste_der_Staaten_der_Erde) (Wikipedia, deutsch).  
Politische Statusangaben können sich ändern. Die App dient ausschließlich privaten Lern- und Informationszwecken.

---

## Tech-Stack

- **Vanilla HTML / CSS / JavaScript** – alles in einer Datei, kein Framework, kein Build-Tool
- Daten via `fetch()` aus `laender.json`
- Fonts: [DM Serif Display](https://fonts.google.com/specimen/DM+Serif+Display) + [DM Sans](https://fonts.google.com/specimen/DM+Sans) (Google Fonts)
- Versionskontrolle: GitHub
