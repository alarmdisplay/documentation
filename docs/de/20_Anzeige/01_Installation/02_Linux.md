---
title: Debian / Raspberry Pi OS
---
[TOC]

Diese Anleitung gilt für Systeme auf Basis von [Debian GNU/Linux](https://www.debian.org/) und damit auch [Ubuntu](https://ubuntu.com/), [Linux Mint](https://linuxmint.com/) und [Raspberry Pi OS](https://www.raspberrypi.org/downloads/raspberry-pi-os/).

Die gezeigten Befehle werden im Terminal ausgeführt.

## Node.js
Wie bereits in den [Voraussetzungen](Voraussetzungen#page_Node.js) erwähnt, wird Node.js benötigt.
Ebenso brauchen wir [npm](https://www.npmjs.com/) (Node Package Manager), um die Abhängigkeiten zu installieren.
Beides kann aus den Paketquellen installiert werden.
````bash
sudo apt-get install nodejs npm
````

## Server vorbereiten
Das Beta-Release kann [hier](https://github.com/alarmdisplay/display-backend/releases/download/v1.0.0-beta.1/display-1.0.0-beta.1.tar.gz) heruntergeladen werden.
Anschließend wird die Datei entpackt, ein neuer Ordner `display` entsteht.

```bash
tar -xzf display-1.0.0-beta.1.tar.gz
cd display
```

Mit `cd display` begeben wir uns in das Hauptverzeichnis des Servers für die Alarmanzeige.
Alle nachfolgenden Befehle werden in diesem Verzeichnis ausgeführt.

Als Nächstes installieren wir die Abhängigkeiten, dies kann ein wenig dauern.
```bash
npm install --only=production
```

Dann müssen noch ein paar Parameter konfiguriert werden, ohne die der Server nicht starten kann.
Bearbeite dazu die Datei `production.json` im Verzeichnis `config/`.
```bash
edit ./config/production.json
```

Diese Datei überschreibt Werte aus der Datei `default.json` aus dem gleichen Verzeichnis mit Werten für den Echtbetrieb ("production").
Essenziell ist dabei der Wert `mysql`, der die Datenbankverbindung definiert.
Mit den Werten aus der [Anleitung zum Anlegen der Datenbank](Voraussetzungen#page_Datenbank) könnte die Datei dann so aussehen:
```json
{
  "port": "4711",
  "mysql": "mysql://displayserver:Bitte_ersetzen@localhost:3306/ad_display"
}
```

Ebenso wurde der Port, auf dem der Server lauscht, auf 4711 geändert.
Wird die Zeile weggelassen, wird standardmäßig der Port 3031 verwendet.

## Der erste Start
Der Server kann jetzt zur Probe von der Kommandozeile aus gestartet werden.
```bash
NODE_ENV=production node index.js
```
Der Server sollte starten, sich mit der Datenbank verbinden und die benötigten Datenbanktabellen anlegen.
Zum Schluss sollte `Display Backend started on http://localhost:3031` (oder ein anderer eingestellter Port) ausgegeben werden.
Wenn das nicht der Fall ist oder Fehler ausgegeben werden, bitte [im Forum](https://community.alarmdisplay.org/c/support/beta-test/6) einen Fehlerbericht verfassen.

## Als Service einrichten
Damit der Server dauerhaft läuft und bei einem Neustart automatisch startet, kann er als Service eingerichtet werden.
Dies geht beispielsweise mit [forever-service](https://github.com/zapty/forever-service).
```bash
npm install -g forever
npm install -g forever-service
sudo forever-service install -s index.js -r pi -e "NODE_ENV=production" alarmdisplay_display
```
Die Option `-r pi` gibt an, dass der Prozess unter dem Benutzer `pi` ausgeführt werden soll.
Hier kann ein beliebiger anderer Benutzer angegeben werden, aus Sicherheitsgründen sollte es aber nicht `root` sein.
Der Name des neuen Services ist hier `alarmdisplay_display`, auch dieser kann nach eigenen Vorlieben verändert werden.

## Betrieb überwachen
Der Server protokolliert wichtige Ereignisse oder Fehler.
Wenn der Service im vorigen Schritt `alarmdisplay_display` genannt wurde, heißt die Protokolldatei `/var/log/alarmdisplay_display.log`.
Mit dem Befehl `tail /var/log/alarmdisplay_display.log` können die neuesten Einträge angesehen werden.