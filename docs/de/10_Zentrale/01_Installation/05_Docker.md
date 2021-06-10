---
title: Docker
---
[TOC]

Wenn du möchtest, kannst du die Zentrale mit Docker betreiben.
Dann brauchst du auf deinem lokalen System kein Node.js oder ähnliches installieren, das Docker-Image bringt alles nötige mit.
Die [Datenbank](01_Allgemein#page_Datenbank) brauchst du trotzdem noch, aber auch die kannst du natürlich mit Docker laufen lassen.

Die Images findest du auf [Docker Hub](https://hub.docker.com/repository/docker/alarmdisplay/hub).

Bei Fragen und Problemen kann dir bestimmt auch die [Dokumentation von Docker](https://docs.docker.com/) weiterhelfen.

## Umgebungsvariablen
Über Umgebungsvariablen kannst du ein paar grundlegende Einstellungen vornehmen, die für den Betrieb wichtig sind.

Lege dir eine Datei an, in der du die Umgebungsvariablen speicherst.
Du kannst dir zum Beispiel in deinem Home-Verzeichnis einen Ordner _env_ anlegen, in dem solche Dateien abgelegt werden.
Im folgenden wird angenommen, dass die Datei _~/env/hub.env_ heißt.

<p class="notice">
Du solltest die Schreib- und Leserechte für die Datei mit den Umgebungsvariablen beschränken.
Das geht beispielsweise mit dem Befehl <code>chmod 640 ~/env/hub.env</code>.
</p>

### Datenbankverbindung
Setze in der Datei nun den Wert für die Datenbankverbindung.
Mit den Werten aus der [Anleitung zum Anlegen der Datenbank](01_Allgemein#page_Datenbank) würde die Datei folgendermaßen aussehen:

```ini
MYSQL_URI=mysql://hubserver:Bitte_ersetzen@db:3306/ad_hub
```

Hier wird angenommen, dass die Datenbank in einem Docker-Container namens _db_ betrieben wird.

## Container starten
Starte den Container mit dem folgenden Befehl:

```shell
docker run -d --env-file /home/pi/env/hub.env -p 3030:3030 --name hub --restart always alarmdisplay/hub:1.0.0-beta.3
```

Damit läuft der Container im Hintergrund und startet auch automatisch beim Hochfahren deines Rechners.

Falls du einen Ordner überwachen möchtest, musst du ihn in den Container einbinden.
Mit dem Parameter `-v /mnt/faxbox:/faxbox` machst du den lokalen Ordner /mnt/faxbox als /faxbox innerhalb des Containers verfügbar.

Wenn du eine serielle Schnittstelle überwachen möchtest, musst du sie ebenso in den Container einbinden.
Mit dem Parameter `--device /dev/ttyACM0:/dev/ttyACM0` machst du das lokale Gerät /dev/ttyACM0 unter gleichem Namen im Container verfügbar. 

Beim Einrichten der Überwachung in der Console musst du dann den Pfad angeben, wie er innerhalb des Containers lautet.

## Betrieb überwachen
Der Server protokolliert wichtige Ereignisse oder Fehler.
Die Logs kannst du dir mit `docker logs -f hub` ansehen.

## Einschränkungen
+ Aktuell kann aus dem Docker-Container heraus nicht gedruckt werden ([Issue auf GitHub](https://github.com/alarmdisplay/hub/issues/11)).
