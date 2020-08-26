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

## Erkennung im Alarmfax
Im Alarmfax werden Einsatzmittel oft mit Abkürzungen bezeichnet (z. B. `FL Ottmarsh 47/1` statt 'Ottmarshausen 47/1').
Damit diese Einsatzmittel erfolgreich erkannt und zugeordnet werden können, kann bei jedem Einsatzmittel eine Liste von alternativen Namen angegeben werden.

Leider fehlt in der aktuellen Beta-Version noch die grafische Oberfläche zum Anlegen in der Console.
Über die [API](../50_API.md#page_section_10) können die alternativen Namen bereits gesetzt werden.

## Zuordnung von Selektivrufen
Einem Einsatzmittel können ebenso Selektivrufe zugeordnet werden.
Selektivrufe, die [per API](../10_Quellen/Pager-API.md) zugeliefert werden, aber keinem Einsatzmittel zugeordnet sind, werden ignoriert.

Leider fehlt in der aktuellen Beta-Version noch die grafische Oberfläche zum Anlegen in der Console.
Über die [API](../50_API.md#page_section_10) können die Selektivrufe bereits gesetzt werden.