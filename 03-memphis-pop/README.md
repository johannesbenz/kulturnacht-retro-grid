# Memphis Pop

Endlos wanderndes Muster im Memphis-Stil der 80er: Zickzack, Wellen, Kreise,
Dreiecke, Konfettipunkte und gestreifte Quadrate in Pink, Türkis, Gelb,
Violett und Orange. Das Muster zieht schräg durchs Bild, die Formen drehen
sich dabei langsam und atmen leicht.

Anders als die beiden anderen Animationen im Repo ist das hier rein grafisch —
keine Perspektive, kein Horizont, kein Fluchtpunkt.

Eine einzige Datei, kein Build, keine Abhängigkeiten, kein Internet nötig.

## Benutzen

`index.html` im Browser öffnen.

| Eingabe | Wirkung |
| --- | --- |
| Button unten rechts, `F` oder Doppelklick/Doppeltipp | Vollbild an/aus |
| `↑` / `↓` | schneller / langsamer |
| Leertaste | Pause / weiter |
| `D` | zwischen hellem und dunklem Untergrund wechseln |

Die helle Variante ist der klassische Memphis-Look. Für einen Beamer in einem
dunklen Raum ist die dunkle Variante meist angenehmer — deshalb die `D`-Taste.
Der Startzustand lässt sich am Ende des Skripts in `setTheme('light')` ändern.

## Anpassen

| Feld in `CFG` | Bedeutung |
| --- | --- |
| `cell` | Rastermaß, bestimmt wie groß und wie dicht die Formen stehen |
| `speed`, `angleDeg` | Tempo und Richtung der Wanderung |
| `jitter` | wie weit eine Form aus ihrer Rasterzelle wandern darf |
| `sizeMin`, `sizeMax` | Größenbereich der Formen |
| `spin`, `breathe` | Eigendrehung und Pulsieren |
| `margin` | zusätzlich gezeichnete Zellen ringsum (siehe unten) |

Die Farben stehen in `COLORS`, die beiden Untergründe in `THEMES`. Neue Formen
kommen als weiterer `case` in `shape()` dazu; danach `SHAPES` erhöhen.

## Technik

**Unendlich statt gekachelt.** Es gibt kein Muster, das sich wiederholt. Jede
Zelle eines gedachten unendlichen Rasters bekommt über einen Ganzzahl-Hash
ihrer Weltkoordinaten dauerhaft ihre Form, Farbe, Größe, Drehung und Lage.
Gezeichnet werden nur die Zellen im Bildausschnitt. Weil alles an der
Weltposition hängt und nicht am Bildausschnitt, wandert das Muster endlos
weiter — es springt nie und wiederholt sich nie.

**Rand.** Formen können über ihre Zelle hinausragen, am weitesten der
Viertelbogen. Würde man nur die sichtbaren Zellen zeichnen, würden solche
Formen am Bildrand aus dem Nichts auftauchen. `margin` zeichnet deshalb zwei
Zellreihen mehr, als zu sehen sind. Geprüft durch Vergleich mit einem
sechsfachen Rand: das Bild ist zu mehreren Zeitpunkten pixelgenau identisch,
es fehlt also nichts.
