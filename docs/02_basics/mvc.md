# MVC (Model-View-Controller)

Drips setzt auf die MVC-Architektur. Hierbei wird die eigentliche Ausgabe (View) von der Steuerung/Logik (Controller) und den Daten (Model) vollkommen getrennt.

## Model

Das Model repräsentiert die Datensicht der Webanwendung. Über das Model gelangen die eigentlichen Daten in die Anwendung. Ein Beispiel für ein Model könnte wie folgt aussehen:

```php
<?php

use Drips\MVC\Model;

class News extends Model {  

    protected static $news = array(  
        "news1" => array("title" => "Eintrag 1", "content" => "Ich bin der erste Eintrag."),  
        "news2" => array("title" => "Eintrag 2", "content" => "Ich bin der ewige Zweite!"),  
        "news3" => array("title" => "Eintrag 3", "content" => "Na dann bin ich die Nummer drei.")  
    );  

    public static function getAll(){  
        return static::$news;  
    }  

    public static function getOne($id){  
        if (array_key_exists($id, static::$news)) {  
            return static::$news[$id];  
        }
    }  
}  
```

Ein News-Model können alle Newseinträge oder ein spezieller Eintrag abgefragt werden.
Ein News-Model-Objekt sollte/kann genau einem Eintrag entsprechen mit zugehörigen Gettern und Settern.

> Für eine Datenbank-Kopplung zwischen Model und Datenbank siehe [ORM/Entities](../03_database/orm.md)).

## View

Die View ist für die jeweilige Darstellung zuständig. Grundsätzlich finden Ausgaben ausschließich in der View statt, um die eigentliche Ausgabe von der Logik und der Steuerung vollständig zu trennen.

```php
<?php

use Drips\MVC\View;

$view = new View;
$view->display(DRIPS_SRC.'/views/test.tpl');
```

> Üblicherweise befindet sich bereits innerhalb eines Controllers bereits ein `View`-Objekt auf welches mittels `$this->view` zugegriffen werden kann.

Das zugehörige Template (in diesem Fall `test.tpl`) ist grundsätzlich normaler HTML-Code in welchem Platzhalter, aber auch Schleifen- und Kontrollflüsse eingesetzt werden können (siehe [Templates](templates.md)).

## Controller

Der Controller ist die Steuerung der Webanwendung zuständig und regelt somit den Ablauf und beinhaltet die Logik.

```php
<?php

use models\News;
use Drips\MVC\Controller;

class NewsController extends Controller
{
    public function getAction()
    {
        $this->view->assign('news', News::getAll());
        $this->view->display(DRIPS_SRC.'/views/news.tpl');
    }
}
```

Abhängig von der Request-Methode (von HTTP), sprich `GET`, `POST`, usw. wird die zugehörige Controller-Action ausgeführt. Beispielsweise wird bei einem `GET`-Request die `getAction()` ausgeführt während bei einem  `POST`-Request die `postAction()` ausgeführt wird.

Die Platzhalter beim Routing werden als Parameter an die jeweilige Action (Methode) übergeben.

Neben dem gewöhnlichen Controller gibt es auch spezielle vorgefertige Controller.

### RouteController

Der `RouteController` funktioniert ähnlich wie der bestehende Controller, jedoch in Kombination mit dem automatischen Routing. (siehe [Routing](routing.md))
Hierbei wird die jeweilige Action anhand der aufgerufenen Url abgeleitet.

Zunächst wird eine Route angelegt, z.B.: `/test/[auto]`

```php
<?php

use Drips\MVC\RouteController;

class TestController extends RouteController
{
    public function updateAction()
    {
        // ...
    }
}
```

Beim Aufruf von `/test/update` wird automatisch die `updateAction()` ausgeführt. Standardmäßig wird die `indexAction()` ausgeführt.

Wie beim gewöhnlichen Controller kann auch hierbei von verschiedenen Request-Methoden unterschieden werden, wie z.B.: `getUpdateAction()` und `postUpdateAction()`.

### StaticPageController

Der `StaticPageController` ist für die Auslieferung statischer Inhalte zuständig. Er kann beispielsweise für die Auslieferung von Impressum, Startseite, Über uns, usw. verwendet werden.

```php
<?php

use Drips\MVC\StaticPageController;

class MyStaticPageController extends StaticPageController
{
    // Legt das Verzeichnis fest, indem sich die Dateien befinden
    protected $source_directory;
    // Legt die Dateiendung der Dateien fest
    protected $file_extension = "tpl";
    // Legt den (HTTP-)Response-Type (MIME) fest
    protected $response_type = "text/html";
}
```

Hierbei muss eine zugehörige Route angelegt werden, die einen Platzhalter definiert, sodass der Controller richtig arbeiten kann, wie z.B.: `/static/{page}`.

### CompileController

Der `CompileController` ist für die Auslieferung von zu kompilierenden Inhalten zuständig. Er wird beispielsweise für die Übersetzung von LESS- in CSS-Dateien verwendet.

```php
<?php

use Drips\MVC\CompileController;

class MyCompileController extends CompileController
{
    // Legt das Verzeichnis fest, indem sich die Quelldateien befinden
    protected $source_directory;
    // Legt das Verzeichnis fest, wo die übersetzten Dateien abgelegt werden sollen (Cache-Verzeichnis!)
    protected $target_directory = "tmp/compile";
    // Legt die Dateiendung der Dateien im $source_directory fest
    protected $file_extension;
    // Legt den (HTTP-)Response-Type (MIME) fest
    protected $response_type;
    // Legt fest ob Caching aktiviert werden soll, oder nicht
    protected $caching = false;
}
```

Auch hierbei muss eine zugehörige Route definiert werden, z.B.: `/css/{file}.css`.
