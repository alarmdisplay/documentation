---
title: Debian / Raspberry Pi OS
---
[TOC]

## Vorwort
**Aktuell ist die Software als Prototyp einzustufen und nicht für den Echtbetrieb vorgesehen.**
Im Rahmen des Beta-Tests sind Testinstallationen und die daraus gewonnenen Erfahrungen sehr willkommen.
Es müssen aktuell noch Abstriche bei der Stabilität oder der Sicherheit in Kauf genommen werden.
Deshalb wird dringend geraten, die Software nur in einem nicht öffentlich zugänglichen Netz zu betreiben.

Diese Anleitung gilt für Systeme auf Basis von [Debian GNU/Linux](https://www.debian.org/) und damit auch [Ubuntu](https://ubuntu.com/), [Linux Mint](https://linuxmint.com/) und [Raspberry Pi OS](https://www.raspberrypi.org/downloads/raspberry-pi-os/).

## Node.js
Wie bereits in den [Voraussetzungen](Voraussetzungen#page_Node.js) erwähnt, wird Node.js benötigt.
Ebenso brauchen wir [npm](https://www.npmjs.com/) (Node Package Manager), um die Abhängigkeiten zu installieren.
Beides kann aus den Paketquellen installiert werden.
````bash
sudo apt-get install nodejs npm
````

## Server vorbereiten
TODO: Release herunterladen

Anschließend wird die Datei entpackt, ein neuer Ordner `display` entsteht.

```bash
tar -xzf release.tar.gz
cd display
```

Mit `cd display` begeben wir uns in das Hauptverzeichnis des Servers für die Alarmanzeige.
Alle nachfolgenden Befehle werden in diesem Verzeichnis ausgeführt.

Als Nächstes installieren wir die Abhängigkeiten, dies kann ein wenig dauern.
```bash
npm install --only=production
```

Dann müssen noch ein paar Parameter konfiguriert werden, ohne die der Server nicht starten kann.
Diese werden in einer Datei namens `.env` gespeichert.
Die Datei `.env.example` enthält Beispielwerte und kann als Vorlage benutzt werden.
```bash
cp .env.example .env
edit .env
```

Mit den Werten aus der [Anleitung zum Anlegen der Datenbank](Voraussetzungen#page_Datenbank) könnte die Datei dann so aussehen:
```bash
DB_HOST=localhost
DB_USER=displayserver
DB_PASSWORD=ein-anderes-sicheres-Passwort
DB_NAME=ad_display
DB_PREFIX=disp_
```
`DB_PREFIX` definiert ein Präfix, das allen Namen für Tabellen vorangestellt wird.
Damit wird eine Unterscheidung möglich, falls noch andere Software mit derselben Datenbank arbeitet.

Soll der Server statt auf dem Port 3000 auf dem Port 4711 lauschen, kann eine Zeile mit `PORT=4711` angefügt werden.

## Der erste Start
Der Server kann jetzt zur Probe von der Kommandozeile aus gestartet werden.
```bash
node src/index.js
```
Der Server sollte starten, sich mit der Datenbank verbinden und die benötigten Datenbanktabellen anlegen.
Zum Schluss sollte `Server listens on port 3000` (oder ein anderer eingestellter Port) ausgegeben werden.
Wenn das nicht der Fall ist oder Fehler ausgegeben werden, bitte [im Forum](https://community.alarmdisplay.org/c/support/beta-test/6) einen Fehlerbericht verfassen.

## Als Service einrichten
Damit der Server dauerhaft läuft und bei einem Neustart automatisch startet, kann er als Service eingerichtet werden.
Dies geht beispielsweise mit [forever-service](https://github.com/zapty/forever-service).
```bash
npm install -g forever
npm install -g forever-service
sudo forever-service install -s src/index.js -r pi ad_display
```
Die Option `-r pi` gibt an, dass der Prozess unter dem Benutzer `pi` ausgeführt werden soll.
Hier kann ein beliebiger anderer Benutzer angegeben werden, aus Sicherheitsgründen sollte es aber nicht `root` sein.
Der Name des neuen Services ist hier `ad_display`, auch dieser kann nach eigenen Vorlieben verändert werden.

## Betrieb überwachen
Der Server protokolliert wichtige Ereignisse oder Fehler.
Wenn der Service im vorigen Schritt `ad_display` genannt wurde, heißt die Protokolldatei `/var/log/ad_display.log`.
Mit dem Befehl `tail /var/log/ad_display.log` können die neuesten Einträge angesehen werden.