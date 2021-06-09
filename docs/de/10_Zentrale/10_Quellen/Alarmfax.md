---
title: Alarmfax
---

Das Alarmfax muss als PDF-Datei vorliegen, um verarbeitet werden zu können.
Das ist beispielsweise über die eingebaute Faxfunktion der FRITZ!Box möglich.

## Ordner überwachen
Klicke auf den Reiter _Eingang_ und wähle dann unter _Quelle hinzufügen_ den Punkt _Überwachter Ordner_ aus.

Du kannst einen absoluten **Pfad** (z. B. `/mnt/faxbox`) oder einen relativen Pfad (z. B. `inbox`) angeben.
Der relative Pfad bezieht sich dann auf das Verzeichnis, in dem der Server läuft.

Die Option **Polling** ist für lokale Ordner in der Regel nicht notwendig.
Ist der zu überwachende Ordner ein eingehängtes Netzlaufwerk, musst du Polling aktivieren, damit neue Dateien erkannt werden.

<p class="notice">
In der Beta 3 kann es vorkommen, dass neue Dateien in lokalen Ordnern nicht korrekt erkannt werden.
Aktiviere in diesem Fall die Option <i>Polling</i>.
Auch werden derzeit ausschließlich PDF-Dateien erkannt.
</p>

Nach dem Speichern kannst du noch ein **Layout** zur Textanalyse auswählen, mit dem die eingehenden Alarme zerlegt werden.
Wenn für deine Leitstelle noch kein Layout hinterlegt ist, findest du [weiter unten](#page_Weitere_Layout_Definition_hinzufugen) mehr Informationen.

## Fax ausdrucken

Über den Punkt _Datei weiterverarbeiten &hellip;_ kannst du einen oder mehrere Druckaufträge für die gefundene Datei einrichten.
Hierzu muss der Drucker bereits in [CUPS](https://www.cups.org/) eingerichtet sein, der Ausdruck funktioniert also erst mal nur unter Linux und macOS.

## Weitere Layout-Definition hinzufügen
Derzeit wird das Alarmfax der ILS Augsburg und der ILS Bamberg unterstützt.
Wenn das Layout für deine Leitstelle noch nicht eingebaut ist, kannst du das [im Forum](https://community.alarmdisplay.org/c/funktionalitaet/alarmzentrale/9) melden.
Falls du dich mit JSON und Regulären Ausdrücken auskennst, kannst du auch selbst eine Layout-Definition bauen und per Pull Request einreichen.
Die dafür notwendigen Schritte sind nachfolgend beschrieben.

Die bestehenden Definitionen sind unter [server/src/services/textanalysis/configs/](https://github.com/alarmdisplay/hub/tree/develop/server/src/services/textanalysis/configs) zu finden.
Erstelle eine neue Datei mit eindeutigem Namen (z.&nbsp;B. `ILS_Augsburg.ts`), möglicherweise kannst du die Datei einer benachbarten Leitstelle zu großen Teilen übernehmen.
Das Schema für `TextAnalysisConfig` ist in der Datei [server/src/services/textanalysis/textanalysis.service.ts](https://github.com/alarmdisplay/hub/blob/develop/server/src/services/textanalysis/textanalysis.service.ts) dokumentiert.

Damit die neue Definition verwendet werden kann, muss sie in die Datei [index.ts](https://github.com/alarmdisplay/hub/blob/develop/server/src/services/textanalysis/configs/index.ts) mit einem eindeutigen Bezeichner eingetragen werden.
Orientiere dich dabei an den bestehenden Einträgen.
Um die neue Definition in der Console auswählbar zu machen, trage den eindeutigen Bezeichner in die Methode `textAnalysisConfigs()` in der Datei [console/src/components/input/WatchedFolder.vue](https://github.com/alarmdisplay/hub/blob/develop/console/src/components/input/WatchedFolder.vue) ein.