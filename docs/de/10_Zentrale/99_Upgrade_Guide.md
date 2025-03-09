---
title: Upgrade Guide
---

Bei einem Update können Änderungen enthalten sein, die für den Weiterbetrieb eine manuelle Anpassung erfordern.
Da Alarmdisplay auf [Semantic Versioning](https://semver.org/) setzt, passiert das nur bei Versionssprüngen der Hauptversion (z.B. von 1.x.x auf 2.x.x).
Während der Beta-Phase können solche sog. _breaking changes_ bei jedem Release auftreten.

## Von 1.0.0-beta.4 zu 1.0.0-beta.5

### Datenmodell der Adressen
Das Feld `locality` wurde in `municipality` umbenannt und ein zusätzliches Feld `district` eingeführt.
Diese Änderung spiegelt sich auch in der API wider.
