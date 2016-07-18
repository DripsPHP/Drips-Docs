# Templates

Drips verwendet [Smarty](http://smarty.net) als Template-Engine. Dementsprechend können sämtliche templatespezifischen Funktion in der [Dokumentation von Smarty](http://www.smarty.net/docs/en/) nachgelesen werden

## Widgets

Drips bietet zusätzlich zur Smarty-Funktionalität auch ein Widget-System. Ein Widget ist ähnlich einem Include, jedoch kann es einerseits durch Angabe von Parametern individuell angepasst werden und außerdem kann ein Widget auch Logik (wie ein Controller) enthalten.

```php
<?php

namespace widgets;

use Drips\MVC\IWidget;

class News implements IWidget
{
    public function exec($params, $view)
    {
        $view->assign('news', News::getAll());
        return $view->display(__DIR__.'/news.tpl');
    }
}
```

Das dazugehörige Template könnte wie folgt aussehen:

```smarty
<h3>News</h3>
{foreach $news as $new}
    <p>{$new}</p>
{foreachelse}
    <p>Es sind keine Newseinträge vorhanden</p>
{/foreach}
```

Das Widget kann anschließend wie folgt in einem anderen Template aufgerufen werden:

```smarty
{widget name="widgets\News"}
```
