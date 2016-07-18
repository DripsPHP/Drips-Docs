# Datenbank Grundlagen

Drips bietet 2 unterschiedliche Möglichkeiten auf eine Datenbank zuzugreifen. Einerseits kann über das [Medoo-Framework](http://medoo.in) auf die Datenbank zugegriffen werden und andererseits über das [Propel](http://propelorm.org) (das ORM-System).

In der Konfigurationsdatei können die Datenbank-Daten festgelegt werden:

```php
<?php

return array(
    // Datenbank-Typ: z.B.: sqlite, mysql, ...
    'database_type' => 'mysql',
    // Datenbank-Server (bei SQLite: der Dateipfad)
    'database_host' => 'localhost',
    // Name der Datenbank (bei SQLite nicht erforderlich)
    'database_name' => 'drips',
    // Datenbank-Benutzer (bei SQLite nicht erforderlich)
    'database_username' => 'root',
    // Datenbank-Passwort (bei SQLite nicht erforderlich)
    'database_password' => 'root',
    // Datenbank-Port (bei SQLite nicht erforderlich)
    'database_port' => 3306,
    // Datenbank Zeichensatz/-kodierung
    'database_charset' => 'utf8',
    // Legt fest ob Datenbankaktivitäten geloggt werden sollen oder nicht (Standard: true)
    'database_logging' => true
);
```

Die Datenbankverbindung wird (aus Performancegründen) nur dann aufgebaut, wenn auch eine Abfrage ausgeführt wird.

Das Datenbank-Objekt kann wie folgt abgerufen werden:

```php
<?php

use Drips\App;

$app = App::getInstance();
$database = $app->db;
```

> Selbstverständlich kann auch direkt über `$app->db` auf die Datenbank zugegriffen werden.

Ist eine weitere Datenbank-Verbindung erforderlich muss selbstständig ein jeweiliges Objekt angelegt werden. Wie dies funktioniert ist ebenso in der Medoo-Dokumentation zu finden, genauso wie das Ausführen von Abfragen.

Beachte allerdings, dass für die Herstellung einer Verbindung kein Medoo-Objekt sondern ein `Drips\Database\DB`-Objekt erzeugt werden muss.

Die Medoo-Dokumentation findest du [hier](http://medoo.in/doc).

> **Achtung:** die Datenbank-Komponente ist standardmäßig nicht in Drips enthalten und muss dementsprechend erst nachinstalliert werden. Hierfür muss lediglich folgendes Kommando auf der Konsole ausgeführt werden:

```
php composer require drips/database
```
