---
title: Konfiguration
---
[TOC]

## Dateien zur Konfiguration

Während viele Dinge über die [Console](05_Console.md) eingestellt werden können, findet die grundlegende Konfiguration über Textdateien statt.
Diese befinden sich im Ordner _config_.

Die Grundlage bildet dabei die Datei _default.json_, in der sämtliche Standardwerte definiert sind.
Für die meisten Fälle reichen diese Standardwerte auch aus, und manche davon sollten erst gar nicht verändert werden.
Der einzige Wert, der dort nicht gesetzt ist, ist die Datenbankverbindung.
Deshalb muss diese Einstellung bei der ersten Installation berücksichtigt werden.

Die Standardwerte der _default.json_ können durch weitere Dateien überschrieben und erweitert werden.
Dabei legt die Datei _development.json_ Einstellungen für die Entwicklung fest, und _production.json_ die Einstellungen für den Echtbetrieb.

Diese drei Dateien werden mit jedem Release ausgeliefert.
Damit bei einem Update eigene Einstellungen nicht verloren gehen, sollten diese Dateien nicht verändert werden.
Schreibe deine Anpassungen stattdessen in eine Datei namens _local-development.json_ bzw. _local-production.json_.

Weitere technische Details gibt es in der [Dokumentation zu node-config](https://github.com/lorenwest/node-config/wiki/Configuration-Files).

## Einstellungen

### Port anpassen
Um die Software abweichend auf Port 4711 zu betreiben, musst du die Einstellung _port_ anpassen.
```json
{
  "port": 4711
}
```

### Sitzungsdauer der Console anpassen
Normal läuft die Sitzung in der Console (und von JWTs allgemein) nach 24 Stunden ab.
Um die Dauer auf beispielsweise 8 Stunden zu reduzieren, trage Folgendes ein:
```json
{
  "authentication": {
    "jwtOptions": {
      "expiresIn": "8h"
    }
  }
}
```

API-Keys sind davon nicht betroffen, diese laufen nie ab.

### Timeout für neuen Einsatz
Wenn Alarme eintreffen, die keinem konkreten Einsatz zugeordnet werden können (z. B. ausgelöste Selektivrufe), wird zuerst ein neuer Einsatz erstellt.
In den ersten 15 Minuten des Einsatzes werden weitere uneindeutige Alarmierungen dem laufenden Einsatz zugeordnet.
Danach wird wieder ein neuer Einsatz angelegt.
Die Anzahl der Minuten hierfür kann mit der folgenden Einstellung gesteuert werden:
```json
{
  "incidents": {
    "minutesBeforeNewIncident": 15
  }
}
```

### Logging
Im Echtbetrieb schreibt die Software nur allgemeine Informationen und Fehler in das Logfile.
Um einem möglichen Fehler auf die Schliche zu kommen, kannst du hiermit mehr Logausgaben bewirken:
```json
{
  "logging": {
    "level": "debug"
  }
}
```

## Anpassungen mit Docker
Bei der Verwendung von Docker läuft es ein bisschen anders.
Hier können nur ausgewählte Einstellungen per Umgebungsvariable in den Container gegeben werden.

Bei der Alarmzentrale sind das:
* MYSQL_URI: Die Datenbankverbindung im `mysql://`-Schema

Um Anpassungen vorzunehmen, die nicht als Umgebungsvariable ausgeführt sind, kannst du ebenfalls eine local-Datei erstellen.
Allerdings heißt diese nicht _local-production.json_, sondern _local-docker.json_.

Du kannst sie entweder [direkt einbinden](https://docs.docker.com/engine/reference/commandline/run/#mount-volume--v---read-only)
```shell
... -v custom.json:/home/node/app/config/local-docker.json ...
```
oder du baust dir ein Image mit dieser zusätzlichen Datei:
```dockerfile
FROM alarmdisplay/hub
COPY ./custom.json /home/node/app/config/local-docker.json
```
