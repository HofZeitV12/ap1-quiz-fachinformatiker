# Änderungen

Das Format folgt *Keep a Changelog*. Bruchstellen sind ausdrücklich gekennzeichnet.

## [Nicht veröffentlicht]

### Geändert — Oberfläche, Umbau von Aufbau und Design (2026-09-30)

Rein darstellend. **Keine Aufgabendaten, keine Wege, keine Vertragswerte und
keine Regeln geändert** — der Inhalt und die sechs Formate sind unverändert.

- **Kopfzeile in drei Zonen getrennt.** Vorher lagen Titel, Wahl (Jahr, Profil)
  und Auskunft (Punkte, Quote, Serie) in einer undifferenzierten Reihe; das Auge
  musste über die Knöpfe steigen, um zum Stand zu kommen. Jetzt: links was das
  hier ist, rechts die Wahl, darunter der Stand. Der Speicher-Zustand ist von der
  Unterzeile in eine eigene kleine Zeile über der Wahl gewandert und damit auch
  auf dem Handy sichtbar. Das **Ausbildungsjahr hat einen eigenen Knopf in der
  Kopfzeile** bekommen; es ist die Wahl, die den sichtbaren Stoff bestimmt, und
  stand vorher nur im Menü „Mehr" (dort entfernt — ein Weg, nicht zwei).
- **Ein Fortschrittsmaß statt nur Zahlen.** Neben Punkten, Quote und Serie steht
  jetzt ein Balken mit Viertelmarken („x % bearbeitet") — der Weg ist eine
  Strecke, keine Zahl. Er zählt ausschließlich die Rechenaufgaben des gewählten
  Ausbildungsjahrs; mehr gibt der Vertrag mit zwei Tabellen nicht her.
- **Die Seitenleiste hat vier erkennbare Ebenen.** Vorher waren 43 Einträge
  13,5 px auf 38 px und unterschieden sich nur durch das Zeichen „↳". Jetzt:
  Formate als gerahmter, nummerierter Block · Bereich als Titelzeile (nicht
  anklickbar) · Aufgabe eingerückt mit Fortschrittsmarke · Quiz/Karten zum
  Bereich kleiner und weiter eingerückt, ohne Fortschrittszahl.
- **Drei Flächengewichte statt eines.** Neun Stellen trugen dieselbe Kante
  `border-top:3px solid tinte` — eine Quellenliste wog damit so schwer wie eine
  laufende Rechenaufgabe. Jetzt: ruhige Fläche (Startseite, Quellen), Blatt mit
  Gewichtskante (Kalkulation, Quiz, Karte, Fallstudie, Dialog), streng (rot).
- **Ein wiederkehrendes Zeichen.** Der kurze Querstrich vor einer Abschnitts-
  und Bereichsüberschrift bindet Kopfzeile, Liste und Blatt aneinander.
- **Startseite beginnt mit „Heute lernen"** statt zum dritten Mal den Namen des
  Programms zu wiederholen. Die sechs Formate sind als Wahl gesetzt (Nummer,
  Umfang, Name), nicht als Kartenreihe; das Raster bleibt auch auf dem Handy
  zweispaltig und fällt erst unter 380 px auf eine Spalte.
- **Tippziele mindestens 44 px**, `overscroll-behavior` gegen ungewollte
  Seitwärtsgesten, `theme-color` ergänzt.

### Behoben — Tastaturbedienung

- **Die Seitenleiste hatte keinen sichtbaren Fokusring.** Rund 50 Knöpfe, durch
  die man nur mit Tab kommt, ohne je zu sehen, wo man steht. `.rail-item` und
  `button.akt` haben jetzt `:focus-visible` (nachgeprüft: alle zwölf
  interaktiven Muster der Oberfläche tragen einen Fokusring).
- Die Kopfzeile wuchs mobil auf 234 px, weil der Speicher-Zustand die Knöpfe in
  zwei Reihen drängte. Jetzt stehen die vier Schalter in einer Reihe bei 208 px.

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

### Hinzugefügt — Oberfläche (UX/UI-Überarbeitung 2026-09-30)

- **Rückweg zur Übersicht** (`Übersicht` in der Kopfzeile, `btn-uebersicht`).
  Erscheint nur beim Lernen und behält den Fortschritt – im Unterschied zum
  Zurücksetzen. Vorher gab es aus dem Lernfluss nur den Browser-Zurück-Knopf
  oder den prominenten „Fortschritt zurücksetzen".
- **Profil-Knopf in der Kopfzeile** (`btn-profil`). Name und Ausbildungsjahr
  waren auf dem Handy nur über die eingeklappte Seitenleiste erreichbar; jetzt
  steht „Profil: <Name>" immer sichtbar oben, mit `aria-label`.
- **Fortschrittsbalken im Quiz** (`.fortschrittsbalken`) unter dem Quizkopf –
  zeigt die Position in der Runde („Frage 3 von 12"). Der Zähler allein stand
  zu weit weg vom Geschehen.
- **Marken an der Quiz-Auflösung** (`.urteil-marke`): ✓ an der richtigen,
  ✗ an der falsch gewählten Antwort. Die Farbe allein war beim schnellen
  Durchklicken zu schwach.
- **Farbige Erklärungsbox**: grün bei richtiger, rot bei falscher Antwort
  (`#quiz-erklaerung.gut` / `.schlecht`) – vorher immer neutral.
- **Lesehilfe in der Seitenleiste** (`.rail-legende`): erklärt, dass der
  Prozentwert an einem Bereich die AP1-Häufigkeit ist und die Zahl rechts an
  einer Aufgabe der eigene Fortschritt. Beides war leicht zu verwechseln.
- **Aktiv-Markierung** für „↳ Quiz/Karteikarten zu diesem Bereich" in der
  Seitenleiste, wenn genau dieser Bereich läuft.
- **Sichere Ränder auf Geräten mit Notch** über `env(safe-area-inset-*)`
  (`.kopf`, `.blatt`, `.rail`) und `viewport-fit=cover`.

### Geändert — Oberfläche (UX/UI-Überarbeitung 2026-09-30)

- **„Formate 6"** wird jetzt als getrennte Flex-Zeile ausgegeben. Vorher
  entstand im Screenreader und in der Semantik die zusammengeklebte Zeichen-
  kette „Formate6" (die Zahl klebte am Text).
- **Quiz-Knöpfe umbenannt:** „Nächste Frage" → **„Weiter"**, „Neue Fragen" →
  **„Neues Set"**. Die alten Beschriftungen klangen fast gleich.
- **Zurücksetzen-Warnung** nennt jetzt die Folge: „…betrifft alle Aufgaben,
  Quizfragen und Karten dieses Profils und lässt sich nicht rückgängig machen."

### Geändert — Barrierefreiheit und Verweise (2026-09-30, Nachmittag)

- **Seitenleiste ist keine Dokumentgliederung mehr.** Die Bereichsnamen standen
  als `<h2>` in der Navigation. Ein Screenreader las damit zwölf
  Navigationsgruppen als Inhaltsüberschriften vor. Sie sind jetzt `<div
  class="rail-kopf">` mit unveränderter Darstellung; im Navigationsbaum sind
  **0 Überschriften**, vorher 12.
- **Fortschritt wird angesagt, nicht nur gezeigt.** Eine Zahl wie „84“ klang für
  Vorleser wie eine bloße Ziffer. Jeder Eintrag trägt jetzt
  `aria-label="…, 84 Prozent Fortschritt"`, ohne Versuch „…, noch kein Versuch".
- **Position im Baum.** Die Navigation hat
  `aria-label="Aufgabenbereiche – Position 3 von 51"` – ein Anker in einer
  51 Punkte langen Liste.
- **Quiz-Fortschritt live** (`.quiz-fortschritt`): Der Zähler „Frage 3 von 12 ·
  1 richtig“ steht in einer `role="status"`-Fläche und wird nach jeder Antwort
  neu gesetzt. Der Balken allein war für Vorleser unsichtbar.
- **Eigene Bestätigungsfläche statt `confirm()`** (`.bestaetig`, `<dialog>`).
  Betrifft „Fortschritt zurücksetzen“ und „Kartenfortschritt zurücksetzen“.
  Eigener Dialog bringt Fokusfang, Escape und `::backdrop` mit; `confirm()`
  blockiert den Hauptfaden und ist nicht gestaltbar. „Abbrechen“ ist
  vorfokussiert, der Fokus kehrt zum Auslöser zurück.
- **Tippziele auf Fingerbedienung.** `.rail-toggle` und `.heim` waren 33 px hoch
  und lagen unter dem Richtwert von 44 px; sie sind jetzt mindestens 44 px
  (`@media (pointer:coarse)`), Navigationseinträge 38 px, auf Touch 44 px.
- **Reihenfolge auf dem Handy.** Die Lesehilfe schob sich zwischen Kopfzeile und
  ersten Lernschritt; sie steht jetzt am Ende der Leiste (`.rail-legende`,
  `order:9`). Dabei einen Spezifitätsfehler behoben: `body.rail-offen .rail`
  überschrieb das nötige `display:flex`.

### Hinzugefügt — Verweise auf einen Bereich (2026-09-30, Nachmittag)

- **`?bereich=<id>` in der Adresse.** Ein Link zeigt direkt in einen Bereich:
  `…/?bereich=netzwerk` öffnet das Quiz zur Netzwerktechnik. Der Parameter wird
  über `history.replaceState` gepflegt — kein Neuladen, der Zurück-Knopf bleibt
  innerhalb des Trainers nutzbar, und ein Lesezeichen landet wieder im richtigen
  Bereich (`adresseSetzen`, `starteBereich`).
- **Gemerkter Wunsch über die Anmeldung hinweg** (`wunschBereich`). Wer einen
  Bereichslink öffnet und noch kein Profil hat, sieht erst die Anmeldung und
  landet danach trotzdem im gewünschten Bereich. Ohne dieses Merken liefe ein
  geteilter Link ins Leere.
- Einstieg wählt automatisch die passende Form: Quiz, wenn es Fragen zum Bereich
  gibt, sonst die erste Rechenaufgabe des Bereichs.

**Bewusst nicht** in die Adresse aufgenommen: die einzelnen Aufgaben. Sie werden
bei jedem Aufruf neu erzeugt und sind damit nicht verlinkbar — ein Nachbau der
Oberfläche in der Adresse wäre irreführend.

### Geprüft (2026-09-30)

- Qualitätstor `npm run check`: **alle 34 Prüfungen bestanden.** Der Vertrag
  (`API`, `STORE`, `JAHR_STORE`, `PROFIL_STORE`, `KARTEN_STORE`) blieb unverändert.
- **Alle sechs Formate am Handy (390 × 844) durchgeklickt** — kein waagerechter
  Überlauf (`scrollWidth` bleibt 390 px):
  Rechnen · Quiz · Karteikarten · Lückentexte · Fehlersuche · Fallstudien.
- Interaktionen geprüft: Quiz antworten und weiterblättern (Zähler zählt mit),
  Karte umdrehen, Lückentext prüfen, Fehlersuche markieren, Rechnung prüfen und
  Lösungsweg anzeigen, Fallstudie auswählen.

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
