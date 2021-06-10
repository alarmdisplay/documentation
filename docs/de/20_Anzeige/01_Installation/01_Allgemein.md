---
title: Allgemeine Vorbereitungen
---
[TOC]

## Datenbank
Zuerst muss eine Datenbank angelegt werden.
Die Namen für die Datenbank oder die Benutzer sind nur Vorschläge, die Verwendung anderer Namen muss in den späteren Schritten selbst bedacht werden.

Die Befehle können entweder über ein Kommandozeilenprogramm oder eine grafische Oberfläche wie [phpMyAdmin](https://www.phpmyadmin.net/) ausgeführt werden.

### Datenbank anlegen
Zuerst legen wir die Datenbank an sich an.

```sql
CREATE DATABASE `ad_display`
  DEFAULT CHARACTER SET utf8mb4
  COLLATE utf8mb4_general_ci;
```

### Benutzer anlegen
Als Nächstes wird der Benutzer angelegt, mit dem sich der Server der Anzeige am Datenbankserver anmelden kann.

Der unten gezeigte Befehl richtet einen Nutzer ein, der sich nur lokal anmelden darf.
Das heißt, der Server für die Anzeige müsste auf demselben System laufen wie die Datenbank.
Laufen die beiden Server auf unterschiedlichen Systemen, muss `localhost` mit der IP-Adresse des Servers für die Anzeige ersetzt werden.
Siehe hierzu auch die Dokumentation zu [Benutzernamen bei MariaDB](https://mariadb.com/kb/en/create-user/#account-names).

Der Teil nach `IDENTIFIED BY` stellt das Passwort dar, dieses sollte natürlich durch ein eigenes und sicheres Passwort ersetzt werden.

```sql
CREATE USER `displayserver`@`localhost`
  IDENTIFIED BY 'Bitte_ersetzen';
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