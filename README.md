# Karriereseite FLURO-Gelenklager GmbH & Martin Höhn GmbH

Conversion-optimierte Karriere-Landingpage (Ad-Funnel) für zwei Stellen als
**CNC-Einrichter (m/w/d)** am Standort Rosenfeld. Aufbau und Sektionsstruktur
1:1 nach dem Vorbild der ALWA-Karriereseite, Texte und CI auf FLURO angepasst.

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

```css
--brand:#e2001a;        /* FLURO-Rot: Buttons, Akzente, Fortschritt */
--brand-dark:#b80015;   /* Hover-Zustand */
--brand-700:#9e0012;    /* Rot als Textfarbe auf Hell */
--brand-900:#14181d;    /* Anthrazit: Überschriften, Hero, Footer */
--brand-soft:#fff0f1;   /* Zarte Flächen hinter Icons */
--on-brand:#ffffff;     /* Textfarbe auf Rot */
```

Schriften: **Barlow** (Überschriften) und **Inter** (Fließtext), eingebunden
über Google Fonts im `<head>`.

---

## 6. Bildmaterial

Dateien in den Ordner `bilder/` legen – die Seite erkennt sie automatisch,
es muss kein Code angefasst werden. Details siehe
`bilder/HIER-BILDER-ABLEGEN.txt`.

| Datei | Wirkung |
|---|---|
| `bilder/fluro-logo.svg` (oder `.png`) | Logo in der Kopfzeile |
| `bilder/fluro-logo-weiss.svg` (oder `.png`) | Logo in Hero und Footer |
| `bilder/hero.jpg` | Hintergrundbild im Hero |

Fehlt eine Datei, bleibt der Fallback stehen (Schriftzug bzw. Farbverlauf) –
es gibt nie ein kaputtes Bild.

---

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

* **CI-Farben**: Die Unternehmenswebsite war aus der Build-Umgebung nicht
  erreichbar (Netzwerk-Policy). Die Werte oben sind eine Annahme
  (Industrierot + Anthrazit) – bitte mit den echten Hausfarben abgleichen.
  Anpassung = der `:root`-Block, sonst nichts.
* **Logo**: wird automatisch übernommen, sobald es in `bilder/` liegt. Bis
  dahin steht der Schriftzug „FLURO“ als Fallback.
* **Impressum / Datenschutz**: verlinken aktuell auf `https://fluro.de/de`.
  Sobald die genauen URLs bekannt sind, im Footer und im Einwilligungstext
  eintragen (3 Stellen).
* **Kontaktdaten**: Es wurden bewusst keine Telefonnummer und keine
  E-Mail-Adresse erfunden. Sobald eine Recruiting-Adresse vorliegt, kann sie
  im Footer und unter dem Formular ergänzt werden.
* **Postleitzahl** im strukturierten Datensatz: 72348 Rosenfeld – bitte kurz
  bestätigen.
