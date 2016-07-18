# Routing

Das Routing ist für die Auflösung einer Url zu einer zugehörigen PHP-Funktion zuständig. Mithilfe des Routings kann also bestimmt werden, was beispielsweise beim Aufruf von `/user/add` passieren soll.

## Routen anlegen

Routen können wie folgt angelegt werden:

```php
<?php
$app->router->add('name_der_route', '/deine/url', function(){
    echo 'Hello World!';
});
```

Alternativ kann auch ein Controller übergeben werden (anstelle einer Funktion).

```php
<?php
$app->router->add('name_der_route', '/deine/url', MyController::class);
```

> Das Routing erzeugt lediglich ein Controller-Objekt. Welche Funktion des Controllers ausgeführt wird, ist auf Aufgabe des Controllers und hängt somit auch vom jeweiligen Controller ab.

Weitere Informationen zum Thema MVC (Controller) findest du [hier](mvc.md).

## Routen mit Platzhaltern

Innerhalb einer Url-Definition können auch Platzhalter verwendet werden, welche in folgendem Format angegeben werden: `{name_des_platzhalters}`.

z.B.:

```php
<?php
$app->router->add('name_der_route', '/deine/url/{param}', function($param){
    echo $param;
});
```

Der Wert des Platzhalters wird anschließend der Funktion als Parameter übergeben. (Reihenfolge beachten!)

Eine Route kann auch mithilfe eines regulären Ausdrucks definiert werden:

```php
<?php
$app->router->add("name_der_route", "/my/url/{param}", function($param){
    echo $param;
}, array(
    'pattern' => [
        'param' => '(startseite|kontakt|impressum)'
    ]
));
```

## Automatisches Routing

```php
<?php
$app->router->add('name_der_route', '/url/[auto]', function(){
    echo 'Hello World!';
});
```

Alle weiteren Urls die wie die gegebene Url beginnen werden an die Funktion gereicht, wobei jeder Teil (zwischen den Slashes) als Parameter an die jeweilige Funktion weitergegeben wird.

> Beim Automatischen Routing muss ein `Drips\MVC\RouteController` verwendet werden, anstelle des gewöhnlichen Controllers (siehe [MVC](mvc.md)).

## Routen einschränken

Die Routen können mehrfach eingeschränkt werden:

 - auf bestimmte Domains
 - nur für HTTPS-Verbindungen
 - auf bestimmte Verbs (Request-Methoden) ... `GET`, `POST`, `DELETE`, `PUT`, `PATCH`

Um eine Einschränkung festlegen zu können wird beim Hinzufügen einer Route ein weiterer Parameter angegeben. Dieser ist ein Array und beinhaltet alle gewünschten Einschränkungen.

```php
<?php
$app->router->add("name_der_route", "/my/url", function(){
    echo "Hello World!";
}, array(
    'https' => true,
    'verb' => ['POST', 'GET'],
    'domain' => ['example.com', 'example.at']
));
```

## Links generieren

Um die Verlinkungen auf die verschiedenen Seiten dynamisch zu generieren kann folgende Funktion verwendet werden.

```php
<?php
$url = route('name_der_route');
```

Es können auch Parameter übergeben werden:

```php
<?php
$url = route('name_der_route', [
    'param' => 'test'
]);
```

### Assets

Auch die Pfade zu Assets (JavaScripts, Stylesheets, Bildern, usw.) können dynamisch generiert werden (ausgehend vom public-Verzeichnis).

```php
<?php
$url = asset('css/style.css');
```

### Redirects / Umleitungen

Zusätzlich gibt es auch die Möglichkeit eine Umleitung auf eine andere Seite durchzuführen:

```php
<?php
redirect('name_der_route');
```
