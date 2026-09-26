# tegel-grundwasser
**Was Regen und Grundwasser über die Zukunft von Berlin-Tegel erzählen.**

Eine interaktive Data-Storytelling-Seite über den ehemaligen Flughafen Berlin-Tegel: Wie hängen Niederschlag und Grundwasserstand auf dem Gelände zusammen, und was bedeutet das für das neue „Schwammstadt“-Stadtquartier, das dort gerade entsteht?

<img width="935" height="335" alt="image" src="https://github.com/user-attachments/assets/f015bea2-972f-4ccc-bffd-21d51b14249b" />

*Rehman Abubakr, 2019, [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Berlin_Tegel_Airport_(TXL)_-_April_2019_(2).jpg), [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.de), verkleinert und entsättigt.*

**🔗 Live ansehen:** *https://possidesiree.github.io/tegel-grundwasser/*

---

## Worum es geht

Über 70 Jahre lang war Tegel ein Flughafen mit großen versiegelten Flächen. Heute entsteht auf dem Gelände das Schumacher Quartier – ein neues Stadtviertel, das bewusst nach dem „Schwammstadt“-Prinzip gebaut wird: Regenwasser soll dort versickern, wo es fällt, statt abgeleitet zu werden.

Die Seite geht der Frage nach, ob und wie schnell sich Regen tatsächlich im Grundwasser unter Tegel bemerkbar macht – anhand von echten Messdaten aus 8 Grundwassermessstellen und täglichen Niederschlagswerten für den Zeitraum März 2025 bis September 2026.

## Wie diese Seite entstanden ist

Das Projekt ist in zwei Schritten entstanden: zuerst die Auswertung der Daten, dann die Umsetzung als interaktive Story.

**Design:** Als Ausgangspunkt für die Optik diente [Figma Make](https://www.figma.com/make/) – dort wurden mit einem kurzen Prompt verschiedene Design-Richtungen für eine Data-Storytelling-Seite durchgespielt (Bildsprache, Typografie, Aufbau der Kennzahlen-Karten). Die überzeugendste Richtung – ein ruhiger, editorialer Look mit klarer Typo-Hierarchie, großzügigen Fotostrecken und hervorgehobenen Kennzahlen-Karten – wurde als Vorlage für die tatsächliche Umsetzung übernommen. Im Zuge der Implementierung hat sich daraus die heutige, kapitelspezifische Farbwelt entwickelt (Asphaltgrau, Wasserblau, Trocken-Orange, Grün – siehe [Theming](#theming)), die im Figma-Entwurf so noch nicht angelegt war, aber demselben gestalterischen Grundgedanken folgt.

**Umsetzung:** Der Code (HTML, CSS, JavaScript sowie die Diagramme als handgeschriebenes SVG) wurde iterativ mit KI-Unterstützung (Claude) entwickelt – ausgehend vom Figma-Entwurf über den Aufbau der Kapitelstruktur bis zu Detailarbeit wie den „Woher kommt diese Zahl?“-Popovers, der Karte und dem Quellenverzeichnis. Die eigentliche Datenanalyse (Python/pandas) und die Rohdaten stammen aus der Projektarbeit des Teams, nicht von der KI.

> Mehr zur technischen Umsetzung im Detail: Abschnitt [Technische Dokumentation](#technische-dokumentation) weiter unten.

## Aufbau der Seite

Die Story ist in elf kurze Kapitel gegliedert, die als scrollbare Einzelseite funktionieren:

| # | Kapitel | Thema |
|---|---------|-------|
| 1 | Asphalt | Warum Wasser auf einem ehemaligen Flughafen wichtig ist |
| 2 | Früher und heute | Dieselbe Fläche, eine neue Aufgabe (Vorher/Nachher-Vergleich) |
| 3 | Die Idee | Kann eine Stadt wie ein Schwamm funktionieren? |
| 4 | Das neue Tegel | Warum diese Idee für Tegel interessant ist |
| 5 | Unter der Erde | Wo wird gemessen? (interaktive Karte) |
| 6 | Frühjahr 2025 | Es regnet kaum |
| 7 | Sommer 2025 | Plötzlich wird es nass |
| 8 | Die Reaktion | Der Regen kommt zuerst, das Grundwasser folgt später |
| 9 | Frühjahr 2026 | Ein außergewöhnlicher Regentag |
| 10 | Die Bilanz | Regen hilft – aber er setzt die Uhr nicht einfach zurück |
| 11 | Zurück nach Tegel | Was bedeutet das für das neue Tegel? |

Danach folgen zwei Transparenz-Kapitel: **Methodik** (wie gerechnet wurde) und das vollständige **Quellenverzeichnis**.

*Hinweis: In internen Projektunterlagen ist gelegentlich von „22 Kapiteln“ die Rede – das bezog sich auf einen früheren Zwischenstand mit anderer Gliederung. Maßgeblich ist die obenstehende, aktuelle Elf-Kapitel-Struktur der veröffentlichten Seite.*

## Funktionen

- **Vorher/Nachher-Regler:** Zwei Fotos derselben Landebahn lassen sich per Schieberegler vergleichen.
- **Interaktive Karte:** Alle acht Grundwassermessstellen auf einer Leaflet-Karte, mit einem Tages-Regler, der die Messwerte zu jedem beliebigen Tag im Zeitraum anzeigt.
- **„Woher kommt diese Zahl?“:** Jede hervorgehobene Kennzahl lässt sich antippen (ⓘ) und zeigt in einem Popover, wie sie berechnet wurde und aus welcher Quelle sie stammt.
- **Quellenverweise im Text:** Jede Aussage mit Zahl ist mit `[n]` verlinkt und springt zum passenden Eintrag im Quellenverzeichnis.
- **Kennzeichnung der Angabenart:** ● Messwert, ∑ Berechnung, ≈ Statistik, ◇ Interpretation, ↗ Extern, ▢ Planung – auf einen Blick erkennbar, was direkt gemessen und was interpretiert ist.
- Läuft komplett im Browser, ohne Server oder Build-Schritt – eine einzige `index.html`.

![Vorher/Nachher-Vergleichsregler einer Landebahn in Tegel](readme-images/compare.png)

![Interaktive Karte mit den acht Grundwassermessstellen](readme-images/map.png)

## Daten & Methodik

### Datenherkunft

Die zwei Kern-Datensätze – die Zeitreihe der Grundwasserstände und die Standorte der acht Messstellen – wurden vom Projektpartner **FUTR HUB – Innovating Urban Data, Urban Tech Republic** ([futr-hub.urbantechrepublic.de](https://futr-hub.urbantechrepublic.de)) bereitgestellt.

Beim Niederschlag gab es einen Umweg: Ursprünglich war die offizielle DWD-Wetterstation Tegel als Quelle vorgesehen. Sie wurde verworfen, weil ihre Messreihe bereits 2021 endet und den Untersuchungszeitraum 2025–2026 damit nicht abdeckt. Als Ersatz dient der Rasterdatensatz **HYRAS-DE-PR** des Deutschen Wetterdienstes (ein Gitterpunkt bei 52,5615° N, 13,2822° O), der durchgehend bis zum aktuellen Datenrand reicht.

### Methodik

- **Analysezeitraum:** 1. März 2025 bis 22. September 2026.
- **Grundwasser:** Tageswerte von acht Grundwassermessstellen rund um Berlin-Tegel.
- **Niederschlag:** Tageswerte aus dem HYRAS-Datensatz, Version v6-1 (siehe oben).
- **Veränderungen** werden als letzter minus erster verfügbarer Messwert im jeweiligen Zeitraum berechnet (in Metern).
- Für Vergleiche über alle Messstellen wird meist der **Median** statt des Mittelwerts verwendet, damit einzelne stark schwankende Messstellen (insbesondere `gwm32-22-op`) das Ergebnis nicht verzerren.
- Der Zusammenhang zwischen Regen und Grundwasser wird über eine **Pearson-Korrelation** zwischen 30-Tage-Regensummen und 30-Tage-Grundwasseränderungen geprüft, zeitversetzt um 0–42 Tage, auf drei Arten berechnet (Mittelwert der Messstellen, Median der Messstellen, je Messstelle einzeln). *Eine Korrelation beweist keine Ursache-Wirkungs-Beziehung – das macht die Seite an den entsprechenden Stellen explizit deutlich.*
- **Karte:** Leaflet 1.9.4, gerendert als Vektor-Illustration aus OpenStreetMap-Geometrie (Overpass-API) – kein klassischer Kachel-Hintergrund (siehe [Technische Dokumentation](#technische-dokumentation)).
- **Werkzeuge:** Python (pandas) für die Auswertung, Diagramme als eigenes SVG – keine externen Chart-Bibliotheken.

Die vollständige, unverkürzte Methodik-Beschreibung steht direkt auf der Seite im Abschnitt „Methodik“.

## Quellen

### Datengrundlage (eigene Auswertung)

| # | Datei | Verwendung |
|---|-------|------------|
| 1 | `Niederschlag_Flughafen_Tegel_2025_2026_v6-1_taeglich.csv` | Tägliche Niederschlagswerte für Berlin-Tegel |
| 2 | `Grundwasser je messstation im zeitverlauf.csv` | Tageswerte der Grundwasserstände (m) an acht Messstellen |
| 3 | `Karte mit Grundwasserpegel.csv` | Standorte (Breiten-/Längengrad) der acht Messstellen |

### Externe Quellen

| # | Herausgeber | Titel |
|---|-------------|-------|
| 4 | Deutscher Wetterdienst (DWD) | [Hydrometeorologischer Rasterdatensatz Niederschlag (HYRAS-DE-PR)](https://www.dwd.de/DE/leistungen/hyras_de_pr/hyras_de_pr.html) |
| 5 | Senatsverwaltung für Stadtentwicklung, Bauen und Wohnen Berlin | [Startschuss für Wohnungsbau im Schumacher Quartier](https://www.berlin.de/sen/stadt/presse/pressemeldungen/pressemitteilung.1526943.php) |
| 6 | Berlin TXL Management GmbH | [Über uns](https://tegelprojekt.de/ueber-uns/) |
| 7 | Berlin TXL Management GmbH (Schumacher Quartier) | [Startschuss für die ersten Wohnungen](https://schumacher-quartier.de/startschuss-fuer-die-ersten-wohnungen-im-schumacher-quartier/) |
| 8 | Berlin TXL Management GmbH (Schumacher Quartier) | [Wassernutzung](https://schumacher-quartier.de/wassernutzung/) |
| 9 | Berlin TXL Management GmbH | [Verdunstungsbeet-Anlage eröffnet](https://tegelprojekt.de/gemeinsam-gegen-hitze-in-der-stadt-forschung-und-wasserwirtschaft-eroeffnen-verdunstungsbeet-anlage-in-berlin-txl/) |
| 10 | Berlin TXL Management GmbH (Urban Tech Republic) | [Digitaler Zwilling für Regenwasser](https://urbantechrepublic.de/digitaler-zwilling-regenwasser-einbau-sensoren/) |
| 11 | Berliner Regenwasseragentur | [Urban Tech Republic – Projektdatenbank](https://regenwasseragentur.berlin/inspirieren-lassen/projektdatenbank/urban-tech-republic/) |
| 12 | Bundeswehr (Luftwaffe) | [Flughafen Tegel schließt endgültig](https://www.bundeswehr.de/de/organisation/luftwaffe/aktuelles/flughafen-tegel-schliesst-endgueltig-5070678) |
| 13 | Deutscher Wetterdienst (DWD) | [Glossar: Niederschlagshöhe](https://www.dwd.de/DE/service/lexikon/begriffe/N/Niederschlagshoehe.html) |
| 14 | Senatsverwaltung für Stadtentwicklung Berlin | [Umweltatlas 02.07 – Flurabstand des Grundwassers](https://www.berlin.de/umweltatlas/_assets/wasser/flurabstand/de-texte/kc207.pdf) |
| 15 | Senatsverwaltung für Stadtentwicklung und Umwelt Berlin | [Umweltatlas 02.17 – Grundwasserneubildung](https://www.berlin.de/umweltatlas/_assets/wasser/grundwasserneubildung/de-texte/kb217.pdf) |
| 16 | OpenStreetMap contributors | [OpenStreetMap-Kartendaten](https://www.openstreetmap.org/copyright) (ODbL) |

*Alle Links wurden zuletzt am 23.09.2026 aufgerufen. Das vollständige, mit Zitatzweck versehene Quellenverzeichnis steht direkt auf der Seite.*

### Bildnachweis

Alle Fotos stammen von Wikimedia Commons und sind entsprechend lizenziert. Alle übrigen Grafiken (Karte, Diagramme, Illustrationen) sind eigene Darstellungen – **keine KI-generierten Bilder.**

| Bild | Titel | Fotograf:in | Jahr | Lizenz |
|------|-------|-------------|------|--------|
| Titelbild | [Berlin Tegel Airport (TXL) – April 2019 (2)](https://commons.wikimedia.org/wiki/File:Berlin_Tegel_Airport_(TXL)_-_April_2019_(2).jpg) | Rehman Abubakr | 2019 | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.de) |
| Kapitel 1 / Vergleichsregler | [Berlin Tegel runway 2015](https://commons.wikimedia.org/wiki/File:Berlin_Tegel_runway_2015.jpg) | Orderinchaos | 2015 | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.de) |
| Vergleichsregler | [Flughafen TXL Landebahn Süd](https://commons.wikimedia.org/wiki/File:Flughafen_TXL_Landebahn_S%C3%BCd.jpg) | Dirk1981 | 2022 | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.de) |
| Kapitel 2 | [Flughafen TXL Terminal A](https://commons.wikimedia.org/wiki/File:Flughafen_TXL_Terminal_A.jpg) | Dirk1981 | 2022 | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.de) |
| Kapitel 4 | [Berlin-Tegel from the air](https://commons.wikimedia.org/wiki/File:Berlin-Tegel_from_the_air.jpg) | Tim Pritlove | 2005 | [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/deed.de) |
| Schlussbild | [Berliner Flughafen Tegel von oben 02](https://commons.wikimedia.org/wiki/File:Berliner_Flughafen_Tegel_von_oben_02.jpg) | Berlinschneid | 2019 | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.de) |

## Technische Dokumentation

Dieser Abschnitt richtet sich an alle, die den Code pflegen, Daten aktualisieren oder die Seite weiterentwickeln wollen.

### Architektur

Die Seite ist eine **Single-File-Webanwendung**: der komplette Code (HTML, CSS, JavaScript) liegt in einer einzigen `index.html`. Es gibt keinen Build-Prozess, keinen Paketmanager und keine zu installierenden Abhängigkeiten. Auch alle Analysedaten (Niederschlag, Grundwasserstände, Kartengeometrie, Quellenverzeichnis, Bildnachweise) sind direkt im Code als JavaScript-Konstanten eingebettet, nicht in separaten CSV-/JSON-Dateien. Das macht das Hosting einfach, bedeutet aber auch: Jede Datenaktualisierung erfordert eine Änderung an dieser einen Datei.

**Externe Abhängigkeiten (per CDN geladen):**

| Zweck | Quelle |
|---|---|
| Kartenbibliothek | Leaflet 1.9.4, von `cdnjs.cloudflare.com` |
| Leaflet-CSS | direkt in die Seite eingebettet (kein eigener CDN-Request) |
| Schriften | Archivo, Atkinson Hyperlegible, IBM Plex Mono – über Google Fonts |

Ohne Internetverbindung lädt die Seite zwar, zeigt aber Systemschriften statt der gewählten Web-Fonts, und die Karte funktioniert nicht (Leaflet kann nicht geladen werden).

### Datenstrukturen im Code

Die wichtigsten JavaScript-Konstanten im `<script>`-Block:

| Konstante | Inhalt |
|---|---|
| `D` | Tageswerte: `D.rain` (Niederschlag ab `D.start`), `D.stations` (Stammdaten je Messstelle inkl. Koordinaten und Zeitreihe) |
| `GEO` | GeoJSON-`FeatureCollection` mit der Geometrie des ehemaligen Flughafens (Start-/Landebahnen, Rollwege, Vorfeld, Terminal, Gewässer, Straßen) |
| `SOURCES` | Quellenverzeichnis, 16 Einträge: `1`–`3` interne Datendateien, `4`–`16` externe Quellen |
| `IMAGES` | 6 Wikimedia-Commons-Fotos mit Fotograf:in, Jahr, Lizenz und Verwendungsort |
| `INFO` | Erklärtexte je Kennzahl für die „Woher kommt diese Zahl?“-Popovers, inkl. Berechnungsweg und Quellenverweis |
| `KIND` | Legende für die Angabearten: `●` Messwert, `∑` Berechnung, `≈` Statistik |
| `STEPS` | Datumsspannen, die das scrollgesteuerte Diagramm beim Durchscrollen der entsprechenden Kapitel hervorhebt |

Eine Datenaktualisierung bedeutet konkret: die Arrays in `D` erweitern bzw. ersetzen, betroffene Werte in `INFO` neu berechnen und anpassen, sowie das `ABRUF`-Datum und ggf. den Analysezeitraum in den Fließtexten aktualisieren. Es gibt keine automatisierte Neuberechnung – alle Kennzahlen sind als fertige Strings im Code hinterlegt.

### Interaktive Komponenten – Implementierung

- **Quellen-/Erklär-Popovers:** Kennzahlen sind als `<span class="info" data-info="...">` ausgezeichnet, Quellenangaben als `<a class="ref" data-ref="...">`. Ein zentraler `click`-Handler (`openPop`/`closePop`) fängt Klicks ab und zeigt die Details (`infoCard()` bzw. `srcCard()`). Das Quellenverzeichnis am Seitenende wird beim Laden per `initRefs()` aus `SOURCES`/`IMAGES` generiert.
- **Karte:** Keine klassische Kachel-Karte (kein `L.tileLayer`), sondern eine mit Leaflet gerenderte **Vektor-Illustration**: `GEO` enthält statisch eingebettete OpenStreetMap-Geometrie (Overpass-API, Datenstand 1. Juni 2026), die nach Kategorie sortiert und mit den CSS-Farbvariablen der Seite eingefärbt wird – dadurch passt sich die Karte automatisch dem Hell-/Dunkelmodus an. Die acht Messstellen kommen als Marker aus `D.stations` hinzu. Bei künftigen Änderungen am Kartenausschnitt ist eine neue Overpass-Abfrage nötig, da zur Laufzeit keine Geodaten nachgeladen werden.
- **Scrollgesteuertes Diagramm:** In den Kapiteln zu Frühjahr/Sommer 2025 wechselt ein Diagramm synchron zum Scrollen den hervorgehobenen Datumsbereich (`STEPS`, `drawScrolly()`). Die Kurven werden live aus `D` als SVG gezeichnet, nicht als Bild eingebunden.
- **Vorher/Nachher-Regler:** `#compare`/`#compare-range` blenden zwei Fotos übereinander; die Reglerposition steuert eine CSS-Custom-Property (`--pos`), die den sichtbaren Ausschnitt begrenzt.

### Theming

Farben sind als CSS Custom Properties auf `:root` definiert und für den Dunkelmodus über `@media (prefers-color-scheme: dark)` überschrieben – die Seite folgt damit automatisch der Systemeinstellung der Besucher:innen. Zusätzliche „Stimmungs“-Klassen je Kapitel (`mood-asphalt`, `mood-water`, `mood-dry`, `mood-green`) färben Hintergründe passend zum jeweiligen Thema (Asphalt/Beton, Wasser, Trockenheit, Grünfläche) – diese kapitelspezifische Farblogik ist im Zuge der Umsetzung aus der ursprünglichen Figma-Design-Idee heraus entstanden (siehe [Wie diese Seite entstanden ist](#wie-diese-seite-entstanden-ist)).

### Bekannte Einschränkungen

- **Keine Offline-Nutzung:** Ohne Internetzugriff fehlen Web-Fonts und die Leaflet-Bibliothek.
- **Kein automatisierter Daten-Import:** Alle Zahlen sind statisch im Code hinterlegt; eine Aktualisierung erfordert manuelle Änderungen an `D`, `INFO`, `SOURCES` und den zugehörigen Texten – es gibt keine Konsistenzprüfung zwischen Rohwerten und gerundeten Textangaben.
- **Kartengeometrie ist ein Schnappschuss:** `GEO` spiegelt den Stand der Overpass-Abfrage vom 1. Juni 2026 wider und aktualisiert sich nicht automatisch.
- **Keine Tests/kein Linting:** Als Single-File-Projekt ohne Build-Pipeline gibt es keine automatisierten Prüfungen; Änderungen sollten vor dem Veröffentlichen lokal im Browser kontrolliert werden.

## Lokal ausführen

Die Seite ist eine einzige, in sich geschlossene `index.html` – HTML, CSS und JavaScript in einer Datei. Bilder werden direkt von Wikimedia Commons geladen, die Karte über die Leaflet-Bibliothek von einem CDN.

```bash
git clone <Repository-URL>
cd <Repository-Ordner>
open index.html   # oder: Doppelklick im Datei-Explorer
```

Eine Internetverbindung wird benötigt, damit Fotos, Kartendaten und Schriftarten laden.

## Hosting

Die Seite ist für **GitHub Pages** vorbereitet: `index.html` liegt im Repository-Root, GitHub Pages baut daraus automatisch die Live-Version unter `https://possidesiree.github.io/tegel-grundwasser/`.

## Kontext

Ein Projekt im Rahmen der CityLAB Berlin Summer School 2026, Datenjournalismus rund um das Grundwassermonitoring am ehemaligen Flughafen Tegel.
