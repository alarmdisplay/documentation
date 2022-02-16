---
title: API
---

Die API wird vom Server derzeit unter dem Pfad `/` bereitgestellt, soll aber noch unter `/api/v1/` verschoben werden.
Wenn der Server der Zentrale unter der IP-Adresse _192.168.1.5_ auf Port 4711 läuft, ist die API unter `http://192.168.1.5:4711/` erreichbar.
Eine Liste der Endpunkte folgt weiter unten.

## Authentifikation
Alle Endpunkte – mit ganz vereinzelten Ausnahmen – sind nur mit Authentifikation benutzbar.
Dies kann über zwei verschiedene Verfahren erfolgen:

### JWT
Mit einem `POST`-Request gegen den Endpunkt `/authentication` kann ein [JWT](https://jwt.io/) erworben werden.
Der Request muss folgendes Format haben:
```json
{
  "strategy": "local",
  "email": "test@example.org",
  "password": "super-secret"
}
```
Die Antwort enthält ein `accessToken`, das bei künftigen Requests im HTTP-Header `Authorization` als `Bearer`-Token verwendet werden kann.
Das Token ist ab Erhalt für 24 Stunden gültig.

### API-Key
Es kann auch ein statischer API-Key verwendet werden, z. B. zur Verwendung in Mikrocontrollern oder eigenen Skripten.
Der Key muss im HTTP-Header `x-api-key` übermittelt werden.

Erzeugt werden API-Keys in der Console unter Administration > API-Keys.
Ein API-Key wird nach dem Anlegen nur einmalig angezeigt und muss sofort notiert werden.
Diese Keys sind bis auf Widerruf gültig.

## Endpunkte
Es folgt eine Auflistung der verschiedenen Ressourcen, die über die API verwaltet werden können.
Mittelfristig soll diese Liste durch eine _Open API Specification_ abgelöst werden.

### `/authentication`
Abruf eines JWT

### `/api-keys`
Die API-Keys

### `/incidents`
Die Einsätze

### `/input/pager`
Endpunkt zum Zuliefern von ausgelösten Selektivrufen, siehe [Pager-API](10_Quellen/Pager-API.md).

### `/locations`
Die Örtlichkeiten von Einsätzen

### `/print-tasks`
Druckaufträge für erkannte Dateien

### `/resources`
Die Einsatzmittel

### `/resource-identifiers`
Die zusätzlichen Bezeichner von Einsatzmitteln wie Namen oder Selektivrufe

### `/serial-monitors`
Zu überwachende serielle Schnittstellen

### `/settings`
Allgemeine Einstellungen

### `/textanalysis`
Einstellungen, welche Textanalyse für welche Quelle verwendet wird

### `/users`
Die Benutzer

### `/watchedfolders`
Auf Dateiänderungen überwachte Ordner