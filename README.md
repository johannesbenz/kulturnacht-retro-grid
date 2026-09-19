# Kulturnacht — Retro-Animationen

Zwei endlos laufende 80er-Animationen für den Browser. Beide sind je eine
einzelne HTML-Datei: kein Build, keine Abhängigkeiten, kein Internet nötig.
Datei öffnen, Vollbild, läuft.

| Ordner | Was es ist |
| --- | --- |
| [`01-retro-grid`](01-retro-grid/) | Synthwave-Sonnenuntergang: Neon-Grid bis zum Horizont, gestreifte Sonne, Sternenhimmel, Berge |
| [`02-neon-tunnel`](02-neon-tunnel/) | Flug durch einen gewundenen Vektortunnel: verdrehte Neonringe, durchlaufende Farbbänder, Leuchtkern |

Die beiden sind bewusst unterschiedlich aufgebaut — das eine eine Landschaft
mit Horizont, das andere eine radiale Komposition ohne festen Bezugspunkt —
teilen sich aber Neonoptik, CRT-Scanlines und die Bedienung.

## Bedienung (in beiden gleich)

| Eingabe | Wirkung |
| --- | --- |
| Button unten rechts, `F` oder Doppelklick/Doppeltipp | Vollbild an/aus |
| `↑` / `↓` | schneller / langsamer |
| Leertaste | Pause / weiter |

Zeiger und Bedienelemente blenden sich nach knapp drei Sekunden ohne Eingabe
aus — gedacht für Beamer oder ein Display im Dauerbetrieb.

Beide laufen ohne Anfang und Ende durch, und zwar nachweislich sprungfrei:
alles Sichtbare hängt nur von der Position im Raum ab, nicht davon, das
wievielte Element gerade dort steht. Details dazu stehen in den READMEs der
jeweiligen Ordner.

## Anpassen

In beiden Dateien stehen alle Stellschrauben gesammelt im Objekt `CFG` oben im
`<script>`-Block, die Farben direkt darunter. Der jeweilige Ordner-README
erklärt die einzelnen Felder.
