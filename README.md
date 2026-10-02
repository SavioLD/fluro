# Karriereseite HÖHN Präzisionsteile

Conversion-optimierte Karriere-Landingpage (Ad-Funnel) für zwei Stellen als
**CNC-Einrichter (m/w/d)** am Standort Rosenfeld. Aufbau und Sektionsstruktur
1:1 nach dem Vorbild der ALWA-Karriereseite, Texte und CI auf HÖHN angepasst.

Arbeitgeber ist die **FLURO-Gelenklager GmbH & Martin Höhn GmbH**; nach außen
führt die Marke **HÖHN Präzisionsteile** (geliefertes Logo). Der vollständige
Firmenname steht in Footer, Einwilligungstext, FAQ und den strukturierten Daten.

Die Seite ist eine einzige Datei: **`index.html`** (HTML, CSS und JS inline,
keine Build-Tools, keine Abhängigkeiten außer Google Fonts).

---

## 1. Veröffentlichen (GitHub Pages)

Repository → **Settings → Pages** → *Source: Deploy from a branch* →
Branch `main`, Ordner `/ (root)` → **Save**.

Die Seite liegt dann unter `https://saviold.github.io/fluro/`.

---

## 2. Die zwei Stellen

| Stelle | Deeplink für die Anzeige |
|---|---|
| CNC-Einrichter (m/w/d) **Serienfertigung** – Star-Langdreher, Fanuc | `?stelle=serienfertigung` (auch: `star`, `serie`, `langdreher`) |
| CNC-Einrichter (m/w/d) **Einzelteilfertigung** – Traub TNA400, TX8i | `?stelle=einzelteilfertigung` (auch: `traub`, `einzelteil`) |

Beispiel: `https://saviold.github.io/fluro/?stelle=star`

Mit Deeplink entfällt der Auswahlschritt komplett – der Bewerber startet
direkt bei Frage 1 (6 statt 7 Schritte) und der Hero ist auf die Stelle
getextet. Für Meta-Anzeigen dringend empfohlen.

Es sind **ausschließlich diese beiden Stellen** auf der Seite. Keine
Initiativbewerbung, keine Sammelbegriffe, keine Verlinkung auf andere Vakanzen.

---

## 3. Vorfilterung: 5 Fragen, eine pro Schritt

| # | Frage | Feld (Webhook) | Kategorie |
|---|---|---|---|
| 1 | Deine Ausbildung | `ausbildung` | **Pflicht** |
| 2 | Deine Berufserfahrung | `berufserfahrung` | **Pflicht** |
| 3 | Programmieren & Rüsten | `programmiererfahrung` | **Pflicht** |
| 4 | Zwei-Schicht-Betrieb | `schichtbereitschaft` | **Pflicht** |
| 5 | Dein Fertigungsumfeld | `fertigungsumfeld` | *optional* |

* **Pflichtfrage nicht erfüllt** → die Bewerbung endet sofort mit einem
  freundlichen Abschlusshinweis. Es werden keine weiteren Schritte gezeigt und
  **keine anderen Stellen angeboten**. Diese Abbrüche werden **nicht** an die
  Lead Table übertragen.
* **Optionale Frage nicht erfüllt** → der Bewerber kommt ganz normal weiter.
  Die Antwort wird übertragen und zusätzlich im Feld `nicht_erfuellt`
  als nicht erfüllt markiert.

### Stellenabhängige Kriterien

Die beiden Anzeigen verlangen unterschiedlich viel Berufserfahrung. Das bildet
die Seite ab: Eine Antwort gilt als erfüllt, wenn sie `data-ok="1"` trägt (gilt
für alle Stellen) **oder** wenn in `data-ok` die gewählte Stelle steht.

Beispiel aus Frage 2 – *3 bis unter 5 Jahre Erfahrung*:

```html
<input type="radio" name="berufserfahrung" value="…" data-ok="serienfertigung" />
```

→ Für die **Serienfertigung** reicht das aus, für die **Einzelteilfertigung**
(laut Anzeige mindestens fünf Jahre) ist es ein K.-o.-Kriterium.

### Kriterium ändern

Ein Kriterium strenger oder lockerer machen = genau ein Attribut ändern:

* `data-ok="1"` → gilt als erfüllt (für alle Stellen)
* `data-ok="serienfertigung"` → nur für diese Stelle erfüllt
* kein `data-ok` → nicht erfüllt (bei Pflichtfragen: K.-o.)

Pflicht/optional wird in der Liste `QUESTIONS` am Seitenende umgestellt
(`pflicht:true` / `pflicht:false`).

### Bewusst nicht enthalten

Kein Lebenslauf-Upload, keine Dateianhänge. Keine Fragen zu Alter, Herkunft,
Gesundheit, Religion oder Familienstand (AGG) – ausschließlich berufsbezogene
Kriterien.

---

## 4. Lead Table – Feldzuordnung

Webhook (generic) der Kachel steht im Script unter `WEBHOOK_URL`.
Gesendet wird **nur bei vollständiger, qualifizierter Bewerbung**.

```json
{
  "vorname":              "Max",
  "nachname":             "Mustermann",
  "telefon":              "0151 23456789",
  "email":                "max@beispiel.de",
  "stelle":               "CNC-Einrichter (m/w/d) Serienfertigung",
  "ausbildung":           "…",
  "berufserfahrung":      "…",
  "programmiererfahrung": "…",
  "schichtbereitschaft":  "…",
  "fertigungsumfeld":     "…",
  "nicht_erfuellt":       "–",
  "datum":                "02.10.2026",
  "datenschutz":          "Ja (Einwilligung mit Absenden, Art. 6 Abs. 1 lit. a DSGVO)",
  "quelle":               "Karriere-Landingpage FLURO",
  "seite":                "https://saviold.github.io/fluro/"
}
```

**Vorname und Nachname sind zwei getrennte Felder.** Es wird bewusst **kein**
kombiniertes Feld (`name`, `fullname`, `vollstaendiger_name`) mitgesendet –
sonst stünde der Name in der Lead Table doppelt. Jedes Feld wird genau einmal
übergeben, es gibt keine Sammelfelder.

Das Honeypot-Feld (`firma_website`, Spam-Schutz) wird nie mitgesendet.

---

## 5. CI anpassen

Alle Farben und Schriften stecken ausschließlich im `:root`-Block ganz oben in
`index.html`. Wer dort etwas ändert, ändert die ganze Seite.

Die Farben sind **direkt aus dem Original-Logo gemessen** (`bilder/logo.png`):
Navy `#07416b` (70 % der deckenden Logo-Pixel) und Grau `#717777` (30 %).

```css
--brand:#07416b;        /* HÖHN-Navy: Buttons, Akzente, Fortschritt */
--brand-dark:#052f4e;   /* Hover-Zustand */
--brand-700:#06395e;    /* Navy als Textfarbe auf Hell */
--brand-900:#10212e;    /* Dunkles Navy: Überschriften, Hero, Footer */
--brand-soft:#e8f0f6;   /* Zarte Flächen hinter Icons */
--on-brand:#ffffff;     /* Textfarbe auf Navy */
--ink-mute:#717777;     /* Grau aus dem Logo */
```

Schriften: **Barlow** (Überschriften) und **Inter** (Fließtext), eingebunden
über Google Fonts im `<head>`.

## 6. Bildmaterial

Alle Dateien liegen in `bilder/`. Die Seite erkennt sie automatisch, es muss
kein Code angefasst werden.

| Datei | Verwendung |
|---|---|
| `logo.png` | Original-Logo (Navy/Grau), Kopfzeile |
| `logo-weiss.png` | Original-Logo (weiß), Hero und Footer |
| `hero.jpg` | Hintergrundbild im Hero (1800 × 1032, 166 KB) |
| `og-bild.jpg` | Vorschaubild beim Teilen (1200 × 630) |
| `zerspaner-mit-teil.png` | Quellfoto (2000 × 1334) |
| `zerspaner-produktionsleiter.png` | Quellfoto (2000 × 1202) |

Die beiden Quellfotos sind bewusst unangetastet im Repo. `hero.jpg` und
`og-bild.jpg` sind daraus erzeugte, fürs Web komprimierte Zuschnitte – die
Original-PNGs mit 3,5 bzw. 3,9 MB würden die Ladezeit auf dem Handy und damit
die Abschlussquote ruinieren.

Die Logos werden **unverändert** eingebunden: nicht nachgebaut, nicht
eingefärbt, Seitenverhältnis nicht verzerrt.

## 7. Mobile Laufruhe

Beim Schrittwechsel gibt es **kein** `window.scrollTo`, **kein**
`scrollIntoView`, **kein** automatisches `focus()`, keinen Reload und keinen
Anker-/Hash-Sprung. `render()` ändert ausschließlich Klassen, Breite und Text.

Die Höhe des Formularcontainers ist über alle Schritte fest
(`--form-min` / `--form-min-mobile`), damit beim Wechsel nichts springt oder
umbricht. Fortschrittsanzeige und Weiter-Button bleiben an fester Position.

Im Browser (Chromium, iPhone-Viewport) geprüft: über alle sieben Schritte
bleiben Scrollposition, Dokumenthöhe und die Position der Formularkarte auf
dem Bildschirm **exakt identisch** – auch bei 320 px Displaybreite.

---

## 8. Offene Punkte

* **Impressum / Datenschutz** verlinken aktuell auf `https://fluro.de/de`.
  Sobald die genauen URLs bekannt sind, im Footer (2 ×) und im
  Einwilligungstext (1 ×) eintragen. Ich wollte keine Pfade raten und 404er
  auf Pflichtlinks riskieren.
* **Kontaktdaten**: Es wurden bewusst keine Telefonnummer und keine
  E-Mail-Adresse erfunden. Sobald eine Recruiting-Adresse vorliegt, kann sie
  im Footer und unter dem Formular ergänzt werden.
* **Postleitzahl** im strukturierten Datensatz: 72348 Rosenfeld – bitte kurz
  bestätigen.
* **Lead-Table-Testeintrag**: Das Payload wurde im Browser abgefangen und
  geprüft (siehe Abschnitt 4). Ein echter Testlauf gegen
  `api-v2.lead-table.com` war aus der Build-Umgebung nicht möglich, weil die
  Netzwerk-Policy den Host blockiert. Einmal über die Live-Seite bewerben
  und in der Kachel nachsehen.
