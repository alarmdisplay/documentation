---
title: API
---

Die API wird vom Server unter dem Pfad `/api/v1/` bereitgestellt.
Wenn der Server der Alarmanzeige unter der IP-Adresse _192.168.1.5_ auf Port 3000 läuft, ist die API unter `http://192.168.1.5:3000/api/v1/` erreichbar.

Zur Erkundung der bestehenden Endpunkte, liefert der Server unter `/api-docs.json` eine Spezifikation gemäß [OpenAPI Specification](https://swagger.io/specification/v2/) aus.
Diese kann mit Tools wie [Swagger UI](https://swagger.io/tools/swagger-ui/) betrachtet werden.

## Authentifikation
Aktuell ist noch keine Authentifikation notwendig, wird aber nachgerüstet.