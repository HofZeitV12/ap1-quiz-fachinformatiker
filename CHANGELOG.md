# Änderungen

Das Format folgt *Keep a Changelog*. Bruchstellen sind ausdrücklich gekennzeichnet.

## [Nicht veröffentlicht]

### Hinzugefügt

- **Inhaltsanalyse** `npm run analyse` (`tools/analysiere-inhalte.mjs`).
  Misst Verteilung über Bereiche und Jahre, findet Lücken, ähnliche Paare,
  verdächtig kurze Einträge und wortgleiche Titel. **Lexikalisch, ohne Modell** —
  Begründung in Entscheidung 0011. Läuft ohne Netzwerk, ohne Abhängigkeiten,
  ändert nichts.
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
- **Das Tor prüft jetzt die Werkzeuge selbst** (Syntax aller `.mjs` in `tools/`).
  Ein Werkzeug mit Syntaxfehler meldet keinen Fehler — es stürzt ab, und niemand
  merkt es. 34 Prüfungen.

### Befunde der Inhaltsanalyse (Lauf vom 2026-09-29)

- **Keine Lücke:** jeder der 12 Bereiche hat in jedem der 3 Jahre Einträge.
- **Keine Dubletten:** über alle 325 Einträge, 6 Formate, 3 Jahre und 12 Bereiche
  gibt es **keine zwei Einträge im selben Format**, die sich ähnlich sind. Die 12
  gefundenen Paare sind **alle** `QUIZ ↔ KARTEN` — gewollt (derselbe Stoff in zwei
  Abfrageformen).
- **Ein Verdacht:** „Kaufvertrag" erscheint als Quiz in **Jahr 2** und als
  Karteikarte in **Jahr 1** (Ähnlichkeit 71 %, Überdeckung 89 %). Eine der beiden
  Jahresmarken ist wahrscheinlich falsch. Aufgenommen als offene Aufgabe im
  Backend-Repository.
- **Beobachtung:** der Bereich `recht` liegt mit **allen 41** Einträgen in Jahr 1,
  obwohl Datenschutz und IT-Sicherheit laut Rahmenlehrplan erst ab Monat 19 dran
  sind (Jahr 2). Ebenfalls als offene Aufgabe aufgenommen.

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
