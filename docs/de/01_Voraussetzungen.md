---
title: Voraussetzungen
---

## Hardware & Betriebssystem
Grundsätzlich sollte das Betriebssystem keine große Rolle spielen.
Da es ein Ziel des Projekts ist, den Einstieg ohne bestehende Hardware günstig zu halten, liegt der Fokus auf der Kompatibilität mit dem [Raspberry Pi](https://www.raspberrypi.org/) und _Raspberry Pi OS_.
Die Kompatibilität mit Windows sollte möglich sein, wurde aber noch nicht getestet.

## Node.js
Die Software läuft auf Basis von [Node.js](https://nodejs.org/).
Für den produktiven Betrieb sollte die _Active LTS_ Version von Node.js verwendet werden (LTS = Long Term Support).
Auch die _Maintenance LTS_ Version kann verwendet werden, sollte aber vor deren End-of-life durch eine aktuelle Version ersetzt werden.
Aktuelle Informationen dazu bietet die [Übersicht von Node.js-Releases](https://nodejs.org/en/about/releases/).

Die Installation von Node.js wird in der Anleitung für die jeweilige Komponente behandelt. 

## Datenbank
Damit die Software Einstellungen und Daten speichern kann, wird eine Datenbank benötigt.
Empfohlen wird dafür der _MariaDB Community Server_, wobei ein kompatibles Datenbanksystem wie mySQL ebenfalls funktionieren sollte.
Für die gängigen Linux-Distributionen ist der Server über den Paketmanager installierbar, für andere Betriebssysteme kann er von der offiziellen [Downloadseite](https://mariadb.com/downloads/#mariadb_platform-mariadb_server) heruntergeladen werden.