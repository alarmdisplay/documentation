---
title: Docker
---
[TOC]

Wenn du möchtest, kannst du die Anzeige mit Docker betreiben.
Dann brauchst du auf deinem lokalen System kein Node.js oder ähnliches installieren, das Docker-Image bringt alles nötige mit.
Die [Datenbank](01_Allgemein#page_Datenbank) brauchst du trotzdem noch, aber auch die kannst du natürlich mit Docker laufen lassen.

Die Images findest du auf [Docker Hub](https://hub.docker.com/repository/docker/alarmdisplay/display).

Bei Fragen und Problemen kann dir bestimmt auch die [Dokumentation von Docker](https://docs.docker.com/) weiterhelfen.

## Umgebungsvariablen
Über Umgebungsvariablen kannst du ein paar grundlegende Einstellungen vornehmen, die für den Betrieb wichtig sind.

Lege dir eine Datei an, in der du die Umgebungsvariablen speicherst.
Du kannst dir zum Beispiel in deinem Home-Verzeichnis einen Ordner _env_ anlegen, in dem solche Dateien abgelegt werden.
Im folgenden wird angenommen, dass die Datei _~/env/display.env_ heißt.

<p class="notice">
Du solltest die Schreib- und Leserechte für die Datei mit den Umgebungsvariablen beschränken.
Das geht beispielsweise mit dem Befehl <code>chmod 640 ~/env/display.env</code>.
</p>

### Datenbankverbindung
Setze in der Datei nun den Wert für die Datenbankverbindung.
Mit den Werten aus der [Anleitung zum Anlegen der Datenbank](01_Allgemein#page_Datenbank) würde die Datei folgendermaßen aussehen:

```ini
MYSQL_URI=mysql://displayserver:Bitte_ersetzen@db:3306/ad_display
```

Hier wird angenommen, dass die Datenbank in einem Docker-Container namens _db_ betrieben wird.

### Anbindung an die Zentrale
Wenn du die Anzeige an die [Zentrale](../../10_Zentrale) koppeln möchtest, füge noch folgende Umgebungsvariablen hinzu.

```ini
HUB_HOST=http://hub:3030
HUB_API_KEY=5:852896607ab905...
```

Hier wird angenommen, dass die Zentrale in einem Container namens _hub_ läuft.
Den API-Key bekommst du in der Console der Zentrale.

### Logging
Die Schwelle für die Logausgaben ist im Standard auf _INFO_ eingestellt, was für den normalen Betrieb ausreicht.
Zur Fehlersuche kannst du detaillierteres Logging mit der folgenden Umgebungsvariable aktivieren:

```ini
LOG_LEVEL=debug
```

## Container starten
Starte den Container mit dem folgenden Befehl:

```shell
docker run -d --env-file /home/pi/env/display.env -p 3031:3031 --name display --restart always alarmdisplay/display:1.0.0-beta.5
```

Damit läuft der Container im Hintergrund und startet auch automatisch beim Hochfahren deines Rechners.

## Betrieb überwachen
Der Server protokolliert wichtige Ereignisse oder Fehler.
Die Logs kannst du dir mit `docker logs -f display` ansehen.
