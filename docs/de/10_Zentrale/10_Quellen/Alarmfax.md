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

## Weitere Layout-Definition hinzufügen
Derzeit wird nur das Alarmfax der ILS Augsburg unterstützt.
Wenn das Layout für deine Leitstelle noch nicht eingebaut ist, kannst du das [im Forum](https://community.alarmdisplay.org/c/funktionalitaet/alarmzentrale/9) melden.
Falls du dich mit JSON und Regulären Ausdrücken auskennst, kannst du auch selbst eine Layout-Definition bauen und per Pull Request einreichen.
Die dafür notwendigen Schritte sind nachfolgend beschrieben.

Die bestehenden Definitionen sind unter [server/src/services/textanalysis/configs/](https://github.com/alarmdisplay/hub/tree/develop/server/src/services/textanalysis/configs) zu finden.
Erstelle eine neue Datei mit eindeutigem Namen (z.&nbsp;B. `ILS_Augsburg.ts`), möglicherweise kannst du die Datei einer benachbarten Leitstelle zu großen Teilen übernehmen.
Das Schema für `TextAnalysisConfig` ist in der Datei [server/src/services/textanalysis/textanalysis.service.ts](https://github.com/alarmdisplay/hub/blob/develop/server/src/services/textanalysis/textanalysis.service.ts) dokumentiert.

Damit die neue Definition verwendet werden kann, muss sie in die Datei [index.ts](https://github.com/alarmdisplay/hub/blob/develop/server/src/services/textanalysis/configs/index.ts) mit einem eindeutigen Bezeichner eingetragen werden.
Orientiere dich dabei an den bestehenden Einträgen.
Um die neue Definition in der Console auswählbar zu machen, trage den eindeutigen Bezeichner in die Methode `textAnalysisConfigs()` in der Datei [console/src/components/input/WatchedFolder.vue](https://github.com/alarmdisplay/hub/blob/develop/console/src/components/input/WatchedFolder.vue) ein.