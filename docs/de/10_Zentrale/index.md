---
title: Zentrale
---
Die Zentrale ist eine reine Serverkomponente zur Datenverarbeitung.
Für eine benutzerfreundliche Einrichtung und Verwaltung stellt der Server die [Console](05_Console.md) zur Verfügung.

## Features

- Überwachung von Ordnern auf neue (Alarmfax-) PDF-Dateien
- Auslesen dieser PDF-Dateien *
- Ausdruck der erkannten PDF-Dateien
- Überwachen von seriellen Schnittstellen (z. B. zur DME-Auswertung)
- Optionale Validierung von Adressen mittels OpenStreetMap
- Kombination von Alarmeingängen zu Einsätzen
- Weiterleitung der Einsätze an die [Anzeige](../20_Anzeige)
- Web-App zur Verwaltung aller Einstellungen im Browser
    - Nutzeraccounts (derzeit alle mit der gleichen Berechtigung)
- REST-API und WebSocket-Verbindung für eigene Software
    - Authentifizierung mit JWT und statischen API-Keys
    - API-Endpunkt zum Zuliefern von ausgelösten Selektivrufen

*: Derzeit wird nur das Alarmfax der ILS Augsburg und der ILS Bamberg unterstützt, weitere benötigte Formate bitte [im Forum](https://community.alarmdisplay.org/c/funktionalitaet/alarmquellen/9) melden