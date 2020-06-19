---
title: Übersicht
---

Das [Projekt Alarmdisplay](https://alarmdisplay.org) bietet ein Informationssystem für Hilfsorganisationen.
Es ermöglicht ausrückenden Einsatzkräften einen Überblick über den aktuellen Einsatz und kann außerhalb von Einsätzen als Anzeige für alltägliche Informationen verwendet werden.

Die Kosten für Anschaffung und Betrieb sollen gering gehalten werden.
Dies wird durch die Verwendung von Open-Source-Software und offenen Standards erreicht.
Auch läuft die Software auf bereits bestehender oder günstiger Hardware (z. B. [Raspberry Pi](https://www.raspberrypi.org/)).

## Zentrale Eigenschaften des Projekts
- **Webbasiert:** Zur Anzeige sowie zur Verwaltung genügt ein Gerät mit einem Webbrowser
- **We <3 APIs:** Alles kann per REST-API gesteuert und konfiguriert werden
- **Offen:** Die Software wird auf [GitHub](https://github.com/alarmdisplay) entwickelt, alle können es sich ansehen und mitwirken
- **Selbst betreiben:** Vertrauen ist gut, selbst betreiben ist besser

Das Projekt leistet damit seinen Beitrag zur Digitalisierung des Feuerwehr- und Rettungswesens.
Der Quellcode ist unter den Bedingungen der [AGPL v3](https://opensource.org/licenses/AGPL-3.0) verfügbar.

## Struktur
Das Projekt gliedert sich in zwei Teilbereiche auf, die [Alarmanzeige](01_Display) und die [Alarmauswertung](02_Processor).

Die beiden Komponenten sind zwar aufeinander abgestimmt bzw. miteinander kompatibel, sie funktionieren aber auch eigenständig.
Der Austausch von Informationen findet ausschließlich über die REST-API statt, es gibt keine gemeinsame Datenbank.
Dadurch kann eine Komponente auch einzeln betrieben und mit eigener Software kombiniert werden.
