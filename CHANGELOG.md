# Änderungen

Das Format folgt *Keep a Changelog*. Bruchstellen sind ausdrücklich gekennzeichnet.

## [Nicht veröffentlicht]

### Hinzugefügt

- **Qualitätstor** `npm run check` (`.github/workflows/qualitaet.yml`).
  Geprüft werden: HTML-Grundgerüst · genau ein Skript- und Stilblock · **Syntax
  des Anwendungscodes** (echter Parser-Lauf, keine Klammerzählung) · Vertrag mit
  dem Backend (Adresse und vier Speicher-Namen) · Inhaltsbestand und
  Jahrgangs-Regel für alle sechs Formate · Secret-Muster · tote Verweise ·
  `vercel.json`.
- **`tools/pruefe-frontend.mjs`** — die Prüfungen als eigenständiges Skript,
  nur mit Node-Bordmitteln.
- **`package.json`** — es gab keine. Enthält nur die Prüfbefehle.
- **`.gitattributes`** — nagelt LF fest. `index.html` lag im Repository als LF,
  im Arbeitsverzeichnis aber als CRLF, weil `core.autocrlf=true` gesetzt ist.

### Geändert

- Die Signatur der Prüfung korrigiert: Die Einträge werden über die
  **Jahresmarke `j`** gezählt, nicht über öffnende Klammern. Eine Zählung der
  Klammern hätte verschachtelte Objekte mitgezählt und für `FEHLER` und `FAELLE`
  falsche Zahlen gemeldet (63 und 125 statt 5 und 5). Die Zahlen in der
  Dokumentation des Backends sind damit **belegt**, nicht behauptet.

### Nicht geändert

- `index.html` und `vercel.json` — dieser Vorgang war das Qualitätstor.
  Am Inhalt, an den Aufgaben und an der Darstellung wurde nichts angefasst.

## [1.0.0] — bis 2026-09-29

### Hinzugefügt

- Oberfläche mit sechs Formaten: Quiz (154), Karteikarten (133), Lückentexte (13),
  Fehlersuche (5), Fallstudien (5), Rechenaufgaben (15) — zusammen 325 Einträge.
- **Jahrgangs-System:** ein Feld `j` je Eintrag, kumulative Sicht (Jahr 1 → Jahr 2
  → Prüfung), Auswahl beim ersten Start, „Jahr wechseln" in der Seitenleiste.
- **Info-Button** an jeder Aufgabe — erklärt die Aufgabe, nicht die Lösung.
- **Profile und Fortschritt** über ein eigenes Backend auf dem Hetzner-Server.
  Der Fortschritt überlebt einen Rechnerwechsel.
- Rückfallweg: Antwortet der Server nicht, bleibt der Fortschritt im Browser
  liegen und wird später nachgereicht.
