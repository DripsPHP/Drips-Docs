# Aufbau und Struktur

Eine übersichtliche und einheitliche Struktur ist bei Entwicklung von Software-Projekten äußerst wichtig. Aus diesem Grund wird von Drips bereits eine Ordnerstruktur- und ein Ablaufschema vorgegeben.

## Ordnerstruktur

```
├── config
├── logs
├── public
│   ├── assets
├── src
│   ├── bootstrap.php
│   ├── controllers
│   ├── models
│   └── views
├── tmp
└── vendor
```

- `config` ... beinhaltet sämtliche Konfigurationsdateien
- `logs` ... beinhaltet alle Logdateien
- `public/assets` ... beinhaltet alle JavaScripts, Stylesheets, Bilder, etc.
- `src/bootstrap.php` ... die Hauptdatei deiner Webanwendung
- `src/controllers` ... beinhaltet alle Controller
- `src/models` ... beinhaltet alle Models
- `src/views` ... beinhaltet alle Views bzw. Templates
- `tmp` ... temporäres Verzeichnis von Drips, wird beispielsweise für Caching usw. verwendet
- `vendor` ... beinhaltet alle Abhängigkeiten von Drips (Dateien in diesem Verzeichnis dürfen auf keinen Fall verändert werden!!)

## Grundlegender Ablauf

Was passiert, wenn man eine Drips-Webseite aufruft?

1. Eingehender Request wird analyisiert (`Drips\HTTP\Request`)
2. Request wird an den Router weitergereicht (`Drips\Routing\Router`)
3. Der Router findet eine zutreffende Route und führt die Callback-Funktion bzw. den zugehörigen Controller aus - wird keine entsprechende Route gefunden - kommt es zu einem  `Error 404`
4. Mithilfe von Ausgaben (`echo`) oder Anzeigen von Views wird ein Response (`Drips\HTTP\Response`) erzeugt, welcher zum anfragenden Benutzer zurückgesendet wird.
