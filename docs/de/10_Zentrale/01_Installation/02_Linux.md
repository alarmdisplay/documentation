---
title: Debian / Raspberry Pi OS
---
[TOC]

Diese Anleitung gilt für Systeme auf Basis von [Debian GNU/Linux](https://www.debian.org/) und damit auch [Ubuntu](https://ubuntu.com/), [Linux Mint](https://linuxmint.com/) und [Raspberry Pi OS](https://www.raspberrypi.org/downloads/raspberry-pi-os/).

Die gezeigten Befehle werden im Terminal ausgeführt.

Bei Fragen und Problemen kannst du dich [im Forum](https://community.alarmdisplay.org/c/support/5) melden.

## Node.js
Wie bereits in den [Voraussetzungen](../../01_Voraussetzungen#page_Node.js) erwähnt, wird Node.js benötigt.
Ebenso brauchen wir [npm](https://www.npmjs.com/) (Node Package Manager), um die Abhängigkeiten zu installieren.
Beides kann aus den Paketquellen installiert werden.
```bash
sudo apt-get install nodejs npm
```

<p class="notice">
Es ist mindestens Node.js in Version 16 erforderlich, empfohlen wird jedoch Version 20.
Da in den Paketquellen meist ältere Versionen zu finden sind, empfiehlt es sich, vor der Installation die <a href="https://github.com/nodesource/distributions/blob/master/README.md#debinstall" target="_blank">Paketquellen von NodeSource</a> einzubinden. 
</p>

## Zusätzliche Software
Für die Verarbeitung von Alarmfaxen wird weitere Software benötigt, die mit den folgenden Befehlen installiert und konfiguriert werden kann:
```bash
sudo apt-get install imagemagick tesseract-ocr-deu
sudo sed -i.bak '$i\ \ <policy domain="coder" rights="read" pattern="PDF" />' /etc/ImageMagick-6/policy.xml
```

## Server vorbereiten
Lade das aktuelle Beta-Release herunter und entpacke es.
Beim Entpacken entsteht ein neuer Ordner `hub`.

```bash
wget https://github.com/alarmdisplay/hub/releases/download/v1.0.0-beta.5/hub-1.0.0-beta.5.tar.gz
tar -xzf hub-1.0.0-beta.5.tar.gz
cd hub
```

Mit `cd hub` begibst du dich in das Hauptverzeichnis des Servers für die Zentrale.
Alle nachfolgenden Befehle werden in diesem Verzeichnis ausgeführt.

Installiere nun die Abhängigkeiten.
```bash
npm install --only=production
```

Dann muss noch die Datenbankverbindung konfiguriert werden, ohne die der Server nicht starten kann.
Lege dazu eine Datei `local-production.json` im Verzeichnis `config/` an.
```bash
edit ./config/local-production.json
```

Mit den Werten aus der [Anleitung zum Anlegen der Datenbank](01_Allgemein#page_Datenbank) würde die Datei folgendermaßen aussehen:
```json
{
  "mysql": "mysql://hubserver:Bitte_ersetzen@localhost:3306/ad_hub"
}
```

Hier trägst du natürlich deine richtigen Daten ein.

## Der erste Start
Der Server kann jetzt zur Probe von der Kommandozeile aus gestartet werden.
```bash
NODE_ENV=production node index.js
```
Der Server sollte starten, sich mit der Datenbank verbinden und die benötigten Datenbanktabellen anlegen.
Zum Schluss sollte `Hub Backend started on http://localhost:3030` ausgegeben werden.

## Als Service einrichten
Damit der Server dauerhaft läuft und bei einem Neustart automatisch startet, kann er als Service eingerichtet werden.
Dies geht beispielsweise mit [forever-service](https://github.com/zapty/forever-service).
```bash
npm install -g forever
npm install -g forever-service
sudo forever-service install -s index.js -r pi -e "NODE_ENV=production" alarmdisplay_hub
```
Die Option `-r pi` gibt an, dass der Prozess unter dem Benutzer `pi` ausgeführt werden soll.
Hier kann ein beliebiger anderer Benutzer angegeben werden, aus Sicherheitsgründen sollte es aber nicht `root` sein.
Jetzt kannst du den Dienst mit dem `service`-Kommando steuern, z. B. `sudo service alarmdisplay_hub restart`.

## Betrieb überwachen
Der Server protokolliert wichtige Ereignisse oder Fehler in der Datei `/var/log/alarmdisplay_hub.log`.
Mit dem Befehl `tail -f /var/log/alarmdisplay_hub.log` wird das Ende der Datei angezeigt und neue Einträge tauchen automatisch auf.

## Updates
Wenn eine neue Version erscheint, läuft das Update sehr ähnlich zur Installation.
Also Release herunterladen, entpacken und mit `npm` die Abhängigkeiten installieren.
Die Datei `config/local-production.json` kann aus der bestehenden Installation übernommen werden.

Wenn alles bereit ist, stoppe den Dienst mit `sudo service alarmdisplay_hub stop`.
Ersetze die bestehende Installation mit dem eben vorbereiteten Ordner.
Dabei kann es ratsam sein, den alten Ordner zuvor umzubenennen (z.B. von `hub` zu `hub_old`), um bei Fehlern auf diese funktionierende Variante zurückgreifen zu können.
Starte dann den Dienst mit `sudo service alarmdisplay_hub start` und prüfe die Logdatei auf eventuelle Warnungen oder Fehlermeldungen.
