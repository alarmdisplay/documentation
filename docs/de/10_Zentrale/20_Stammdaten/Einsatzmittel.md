---
title: Einsatzmittel
---

Unter _Verarbeitung > Einsatzmittel_ können die eigenen Einsatzmittel eingetragen werden.
Dabei können verschiedene Typen von Einsatzmitteln unterschieden werden:
- Organisationen
- Fahrzeuge
- Führungsdienstgrade
- Gruppen
- Sonstige

Diese Unterscheidung kommt aktuell noch nicht zum Tragen und ist nur eine Vorbereitung für die Zukunft.

![](resources.png)

## Erkennung in Texten
Im Alarmfax werden Einsatzmittel oft mit Abkürzungen bezeichnet (z. B. _FL Ottmarsh 47/1_).
Damit diese Einsatzmittel erfolgreich erkannt und zugeordnet werden können, kann bei jedem Einsatzmittel eine Liste von alternativen Namen angegeben werden.
Bei der Textanalyse werden ausschließlich diese Bezeichner herangezogen.

![](resource-editor.png)

## Zuordnung von Selektivrufen
Einem Einsatzmittel können ebenso Selektivrufe zugeordnet werden.
Dies ist Voraussetzung, um ausgelöste Selektivrufe [per API](../10_Quellen/Pager-API.md) zuliefern zu können.
