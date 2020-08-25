---
title: Selektivrufe per API
---
Über die API können alarmierte Selektivrufe eingespeist werden.
Diese Schnittstelle ist für eigene Programme gedacht, die z. B. den potenzialfreien Kontakt von Funkmeldeempfängern abgreifen und das Ereignis weitermelden.

Der Endpunkt heißt `/input/pager` und erfordert Authentifizierung.
Es ist nur ein `POST`-Request möglich, der das folgende Format haben muss:
```json
{
  "selcall": "12345"
}
```

Dieser Request würde bewirken, dass alle Einsatzmittel gesucht werden, die mit dem Selektivruf 12345 verbunden sind.
Diese Einsatzmittel werden dann an den aktuellen – oder falls es keinen gibt, einen neuen – Einsatz angehängt.
Werden keine Einsatzmittel zu dem Selektivruf gefunden, wird kein Einsatz angelegt oder erweitert.