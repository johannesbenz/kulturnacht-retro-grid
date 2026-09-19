# Retro Grid

Endlos laufende Retro-/Synthwave-Animation im Browser: Neon-Grid, das auf den
Betrachter zuläuft, gestreifte Sonne über dem Horizont, Sternenhimmel,
Bergsilhouetten und ein CRT-Scanline-Look.

Eine einzige Datei, kein Build, keine Abhängigkeiten, kein Internet nötig.

## Benutzen

`index.html` auf einem beliebigen Gerät im Browser öffnen — per Doppelklick
aus dem Dateimanager, oder die Datei auf einen Webspace/USB-Stick legen.

| Eingabe | Wirkung |
| --- | --- |
| Button unten rechts, `F` oder Doppelklick/Doppeltipp | Vollbild an/aus |
| `↑` / `↓` | schneller / langsamer |
| Leertaste | Pause / weiter |

Bedienelemente und Mauszeiger blenden sich nach knapp drei Sekunden ohne
Eingabe aus — praktisch für Beamer oder Dauerbetrieb auf einem Display.

Die Animation läuft ohne Anfang und Ende durch: die Querlinien werden mit
gleichmäßigem Tiefenabstand erzeugt und zyklisch verschoben, deshalb gibt es
beim Umlauf keinen sichtbaren Sprung.

## Anpassen

Alle Stellschrauben stehen im Objekt `CFG` oben im `<script>`-Block:

| Feld | Bedeutung |
| --- | --- |
| `speed` | Grundtempo des Grids |
| `horizon` | Höhe der Horizontlinie (Anteil der Bildhöhe) |
| `rowStep` | Tiefenabstand der Querlinien |
| `colDensity` | angestrebte Spaltenzahl über die Bildbreite |
| `sunRadius`, `sunSink` | Größe der Sonne und wie tief sie hinterm Horizont steht |
| `starCount`, `twinkleFrac` | Anzahl Sterne, Anteil davon flackernd |

Die Farben des Grids liegen in den Konstanten `NEAR` (vorne, Cyan) und `FAR`
(am Horizont, Magenta), die Himmels- und Sonnenverläufe in `paintSky()` bzw.
`paintSun()`.

## Technik

Alles Unbewegte — Himmel, Sterne, Sonne, Berge, Horizontglühen und die
Längslinien des Grids — wird bei Programmstart und nach jedem Resize einmal in
Offscreen-Canvases gerendert. Pro Bild werden nur noch diese fertigen Ebenen
kopiert und die wandernden Querlinien neu gezeichnet. Das ist rund doppelt so
schnell wie eine vollständige Neuberechnung je Bild und hält auch ältere
Geräte und Beamer-Notebooks bei flüssiger Darstellung.

Horizont, Sonnengröße und Gitterdichte hängen am Seitenverhältnis, damit das
Bild quer wie hochkant stimmt.
