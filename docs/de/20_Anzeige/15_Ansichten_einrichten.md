---
title: Ansichten einrichten
---

Die Ansichten für ein Display können in der [Console](05_Console.md) verwaltet werden.
Dazu in der Übersicht der Displays den Knopf 'Ansichten' des betreffenden Displays wählen.

![](console_display_listitem.png)

## Ruhemodus
Wenn das Display frisch eingerichtet wurde, ist noch keine Ansicht für den Ruhemodus vorhanden.
In diesem Fall zeigt das Display einfach das aktuelle Datum und die Uhrzeit mittig an.
Falls dies ausreicht, muss nichts weiter eingestellt werden.

Um den Ruhemodus informativer zu gestalten, stehen eine Reihe von Komponenten zur Verfügung.
Dazu zählen neben Datum/Uhrzeit noch _Ankündigungen_ zur Auflistung von Neuigkeiten und Unwetterkarten des DWD.
Weitere Komponenten sind in Planung, Ideen können gerne in der [Community](https://community.alarmdisplay.org/c/funktionalitaet/alarmanzeige/8) eingebracht werden.

Um die Komponenten zu verwenden, muss erst mit dem Knopf _Ansicht hinzufügen_ eine leere Ansicht angelegt werden.
Es können auch mehrere Ansichten angelegt werden, diese werden dann im Wechsel angezeigt.

Beim Bearbeiten einer Ansicht können die Komponenten auf einem Raster frei angeordnet werden.
Die Dimensionen des Rasters (Spalten und Zeilen) können für jede Ansicht separat eingestellt werden.

![](edit-view.gif)

Bei den Komponenten _Ankündigungen_ und _DWD-Unwetterkarte_ kann durch einen Klick auf den Namen der Komponente ein Fenster mit Optionen geöffnet werden.

*Hinweis:*
Aufgrund eines Fehlers werden bei Komponenten, die der Ansicht gerade neu hinzugefügt wurden, die Optionen nicht übernommen.
Deshalb sollten die Optionen erst bearbeitet werden, nachdem die Ansicht gespeichert wurde.

## Alarmbildschirm
Im Moment kann das Aussehen des Alarmbildschirms nicht individuell angepasst werden.
Der standardmäßige Alarmbildschirm versucht, die vorhandenen Informationen möglichst klar darzustellen.

Enthalten sind:
- Einsatzgrund
- Stichwort
- Verstrichene Zeit
- Adresse
- Freitext
- Aktuelle Uhrzeit

![](alert-screen.png)
