---
title: Voraussetzungen
---
[TOC]

## Vorwort
**Aktuell ist die Software als Prototyp einzustufen und nicht für den Echtbetrieb vorgesehen.**
Im Rahmen des Beta-Tests sind Testinstallationen und die daraus gewonnenen Erfahrungen sehr willkommen.
Es müssen aktuell noch Abstriche bei der Stabilität oder der Sicherheit in Kauf genommen werden.
Deshalb wird dringend geraten, die Software nur in einem nicht öffentlich zugänglichen Netz zu betreiben.

## Hardware & Betriebssystem
Grundsätzlich sollte das Betriebssystem keine große Rolle spielen.
Da es ein Ziel des Projekts ist, den Einstieg ohne bestehende Hardware günstig zu halten, liegt der Fokus auf der Kompatibilität mit dem [Raspberry Pi](https://www.raspberrypi.org/) und _Raspberry Pi OS_.
Die Kompatibilität mit Windows sollte möglich sein, wurde aber noch nicht getestet.

## Node.js
Der Server läuft auf Basis von [Node.js](https://nodejs.org/).
Für den produktiven Betrieb sollte die _Active LTS_ Version von Node.js verwendet werden (LTS = Long Term Support).
Auch die _Maintenance LTS_ Version kann verwendet werden, sollte aber vor deren End-of-life durch eine aktuelle Version ersetzt werden.
Aktuelle Informationen dazu bietet die [Übersicht von Node.js-Releases](https://nodejs.org/en/about/releases/).

Die Installation von Node.js wird in der Anleitung für die jeweiligen Betriebssysteme behandelt. 

## Datenbank
Damit der Server Einstellungen und Daten speichern kann, wird eine Datenbank benötigt.
Empfohlen wird dafür der _MariaDB Community Server_, wobei ein kompatibles Datenbanksystem wie mySQL ebenfalls funktionieren sollte.
Für die gängigen Linux-Distributionen ist der Server über den Paketmanager installierbar, für andere Betriebssysteme kann er von der offiziellen [Downloadseite](https://mariadb.com/downloads/#mariadb_platform-mariadb_server) heruntergeladen werden.

Die Namen für die Datenbank oder die Benutzer sind nur Vorschläge.
Die Verwendung anderer Namen muss in den späteren Schritten selbst bedacht werden.

Die Befehle können entweder über ein Kommandozeilenprogramm oder eine grafische Oberfläche wie [phpMyAdmin](https://www.phpmyadmin.net/) ausgeführt werden.

### Datenbank anlegen
Zuerst legen wir die Datenbank an sich an.

```sql
CREATE DATABASE `ad_display`
  DEFAULT CHARACTER SET utf8mb4
  COLLATE utf8mb4_general_ci;
```

### Benutzer anlegen
Als Nächstes wird der Benutzer angelegt, mit dem sich der Server der Alarmanzeige am Datenbankserver anmelden kann.

Der unten gezeigte Befehl richtet einen Nutzer ein, der sich nur lokal anmelden darf.
Das heißt, der Server für die Alarmanzeige müsste auf demselben System laufen wie die Datenbank.
Laufen die beiden Server auf unterschiedlichen Systemen, muss `localhost` mit der IP-Adresse des Servers für die Alarmanzeige ersetzt werden.
Siehe hierzu auch die Dokumentation zu [Benutzernamen bei MariaDB](https://mariadb.com/kb/en/create-user/#account-names).

Der Teil nach `IDENTIFIED BY` stellt das Passwort dar, dieses sollte natürlich durch ein eigenes und sicheres Passwort ersetzt werden.

```sql
CREATE USER `displayserver`@`localhost`
  IDENTIFIED BY 'Bitte ersetzen';
```

### Benutzerrechte vergeben
Der neu angelegte Benutzer darf sich nun zwar anmelden, aber noch nicht auf die Datenbank zugreifen.
Der nachfolgende Befehl teilt die nötigsten Rechte zu und auch nur für diese eine Datenbank.
Falls im vorhergehenden Schritt der Host-Teil des Benutzers (`localhost`) abgeändert wurde, muss das auch hier gemacht werden.

```sql
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER
  ON `ad\_display`.*
  TO `displayserver`@`localhost`;
```