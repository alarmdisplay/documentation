---
title: Alarmfax
---

Das Alarmfax muss als PDF-Datei vorliegen, um verarbeitet werden zu können.
Das ist beispielsweise über die eingebaute Faxfunktion der FRITZ!Box möglich.

## Ordner überwachen
In der Console kannst du unter _Eingang > Überwachte Ordner_ festlegen, welche Ordner auf neue PDF-Dateien überwacht werden sollen.
Du kannst einen absoluten Pfad (z. B. `/mnt/faxbox`) oder einen relativen Pfad (z. B. `inbox`) angeben.
Der relative Pfad bezieht sich dann auf das Verzeichnis, in dem der Server läuft.

Die Option _Polling_ ist für normale Verzeichnisse nicht notwendig.
Ist das zu überwachende Verzeichnis ein eingehängtes Netzlaufwerk, wirst du Polling aktivieren müssen, damit neue Dateien erkannt werden.

## Texterkennung und -analyse
Sobald eine neue PDF-Datei erkannt wurde, wird sie in ein Arbeitsverzeichnis kopiert und der Texterkennung zugeführt.
Der ausgelesene Text wird dann analysiert.
Wird der Text als Alarmfax identifiziert, werden die erkannten Daten als Alarm weiterverarbeitet.

Derzeit wird nur das Alarmfax der ILS Augsburg unterstützt, weitere benötigte Formate bitte [im Forum](https://community.alarmdisplay.org/c/funktionalitaet/alarmzentrale/9) melden.
