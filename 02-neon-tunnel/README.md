# Neon Tunnel

Endloser Flug durch einen gewundenen Vektortunnel: achteckige Neonringe, die
sich zu einer Wendel verdrehen, durchlaufende Farbbänder, mitfliegende
Lichtpunkte und ein Leuchtkern am fernen Ende.

Eine einzige Datei, kein Build, keine Abhängigkeiten, kein Internet nötig.

## Benutzen

`index.html` im Browser öffnen. Bedienung wie bei `01-retro-grid`:

| Eingabe | Wirkung |
| --- | --- |
| Button unten rechts, `F` oder Doppelklick/Doppeltipp | Vollbild an/aus |
| `↑` / `↓` | schneller / langsamer |
| Leertaste | Pause / weiter |

## Anpassen

Alle Stellschrauben stehen im Objekt `CFG` oben im `<script>`-Block:

| Feld | Bedeutung |
| --- | --- |
| `sides` | Ecken je Ring — kleiner wirkt kantiger, mehr Vektor-Optik |
| `speed` | Fluggeschwindigkeit |
| `ringStep`, `ringCount` | Abstand und Anzahl der Ringe, zusammen die Tunnellänge |
| `twistZ`, `spin` | Verdrehung pro Tiefeneinheit und Eigendrehung |
| `driftAmp*`, `driftFreq*`, `driftSpd*` | wie stark, wie eng und wie schnell sich der Tunnel windet |
| `colorCycle` | nach wie vielen Ringen sich die Farbe wiederholt |
| `starCount` | Anzahl der mitfliegenden Lichtpunkte |

Die Farbfolge steht in `PAL` — die Liste wird zyklisch durchlaufen und weich
interpoliert, Einträge lassen sich beliebig ergänzen oder ersetzen.

## Technik

**Sprungfreier Umlauf.** Ringe liegen bei `z = i · ringStep − offset`, wobei
`offset` zyklisch umläuft. Farbe, Verdrehung und Krümmung hängen deshalb
ausschließlich von der Tiefe `z` und von umlaufend gehaltenen Phasen ab, nie
vom Ringindex `i`. Ein Ring an einer bestimmten Tiefe sieht damit immer gleich
aus, egal welcher Ring gerade dort steht — beim Umlauf entsteht kein Sprung.

Dazu gehört, dass ein Ring bereits unsichtbar ist, bevor er auftauchen oder
verschwinden kann: je nach Phase reicht der hinterste Ring bis
`ringCount · ringStep` oder nur einen Schritt davor, deshalb blendet
`zFadeEnd` schon bei `(ringCount − 1) · ringStep` auf null aus. Nachgewiesen
mit einer virtuellen Uhr: schiebt man `dist` um genau einen Ringabstand
weiter, ist das Bild pixelgenau identisch.

**Leuchten.** Statt jede Linie mehrfach zu zeichnen, wird das fertige Bild
zweimal verkleinert abgelegt und additiv zurückgeblendet. Die Interpolation
beim Hochskalieren wirkt wie eine Weichzeichnung — das ergibt den Neon-Schein
für wenige Millisekunden pro Bild.
