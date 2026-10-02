# Creatives & Social-Assets

Alle Dateien sind ausschließlich aus dem gelieferten Bildmaterial gebaut
(`../bilder/zerspaner-mit-teil.png`, `../bilder/zerspaner-produktionsleiter.png`)
und tragen das Original-Logo unverändert – nicht nachgebaut, nicht eingefärbt,
Seitenverhältnis nicht verzerrt.

CI durchgängig: Navy `#07416b` und Grau `#717777` (aus dem Logo gemessen),
Akzent-Hellblau `#9ecbe8`, Schriften Barlow (Headlines) und Inter (Fließtext) –
dieselben wie auf der Karriereseite.

## Aufbau: ein Satz je Stelle

| Ordner | Stelle | Anzeigen-Link |
|---|---|---|
| `serienfertigung/` | CNC-Einrichter (m/w/d) Serienfertigung · Star-Langdreher | `…/fluro/?stelle=star` |
| `einzelteilfertigung/` | CNC-Einrichter (m/w/d) Einzelteilfertigung · Traub | `…/fluro/?stelle=traub` |
| `beide-stellen/` | beide Stellen gemeinsam | `…/fluro/` (ohne Parameter) |

Je Ordner 15 Creatives: 3 Konzepte × 5 Platzierungsformate.
**45 Creatives gesamt.**

## Welche Datei für welche Platzierung

| Dateiendung | Pixel | Platzierung |
|---|---|---|
| `-4x5` | 1080 × 1350 | Facebook- und Instagram-Feed (Hochformat) |
| `-1x1` | 1080 × 1080 | quadratische Platzierungen, Marketplace, Explore |
| `-9x16` | 1080 × 1920 | Stories und Reels |
| `-191x1` | 1200 × 628 | rechte Spalte, Suchergebnisse, Audience Network – die Platzierungen, die zwingend Querformat sind |
| `-3x4` | 1080 × 1440 | organische Beiträge, andere Kanäle (keine eigene Meta-Platzierung) |

## Wichtig: im Ads Manager je Platzierung ersetzen

Wird **eine** Datei hochgeladen, schneidet Meta sie im Schritt *Zuschneiden*
selbst auf die übrigen Seitenverhältnisse zu – dabei fliegen Button und
Textzeilen aus dem Bild.

Deshalb im Schritt **Zuschneiden** pro Platzierungskachel auf **„Ersetzen"**
gehen und die Datei mit dem passenden Seitenverhältnis hochladen:

* 1:1 → `…-1x1.jpg`
* 9:16 → `…-9x16.jpg`
* 1,91:1 → `…-191x1.jpg`
* Feed → `…-4x5.jpg`

Dann wird nichts automatisch beschnitten. Alternativ bei jeder Kachel
**„Original"** wählen – dann bleibt das Bild unbeschnitten, läuft aber in
manchen Platzierungen mit Balken.

Geprüft beim Rendern: In allen 45 Creatives liegen Logo, Eyebrow, Headline,
Subline und Button vollständig innerhalb der Fläche, und kein Text läuft über
seine Box hinaus. Die Headline wird automatisch verkleinert, falls eine Zeile
zu breit würde. Zusätzlich wird geprüft, dass das Logo in keinem Layout
verzerrt dargestellt wird.

## Die drei Konzepte

| Datei | Konzept | Layout |
|---|---|---|
| `creative-01-benefit-*` | Benefit voran – 13. Gehalt, 30 Tage Urlaub, unbefristet | Foto mit Verlauf |
| `creative-02-berufsbild-*` | Berufsbild direkt – Stelle und Maschinen konkret | Foto oben, Navy-Block unten |
| `creative-03-huerde-*` | Problem/Lösung – kein Anschreiben, kein Lebenslauf | Foto mit Navy-Karte |

Die drei Konzepte nutzen bewusst **unterschiedliche Layouts und Motive**, damit
die drei Creatives einer Anzeigengruppe nicht wie Dubletten wirken und Meta
echte Varianten zum Ausspielen hat.

Die 9:16-Varianten halten oben 250 px und unten 336 px frei – dort liegt in
Stories und Reels die Meta-Oberfläche (Profilzeile bzw. CTA-Leiste).

Das Querformat 1,91:1 nutzt ein eigenes Layout: Text links, Foto rechts. Es ist
nur dabei, damit die zwingend queren Platzierungen eine eigene Datei bekommen
und Meta das Hochformat nicht selbst beschneidet.

Die Headline skaliert beim Rendern automatisch herunter, falls eine Zeile zu
breit wird (geprüft: „Einzelteilfertigung." passt bei 94 px, ab 112 px greift
die Verkleinerung).

## Werbetexte

Pro Stelle gibt es 3 Textvarianten. Sie nehmen **keinen Bezug auf Bildinhalte**,
jede Variante lässt sich mit jedem Creative derselben Stelle kombinieren.
Die Texte stehen im Chatverlauf zum Kopieren bereit.

## Facebook-Seite

| Datei | Format | Hinweis |
|---|---|---|
| `fb-profilbild.jpg` | 1080 × 1080 | Logo mittig. Nachgemessen: kein Logo-Pixel außerhalb des runden Beschnitts, 168 px Luft zum Rand. |
| `fb-titelbild.jpg` | 1640 × 856 | Logo und Claim vollständig in der Sicherheitszone 1092 × 616. Unten rechts bleibt frei für den Facebook-Button. |
