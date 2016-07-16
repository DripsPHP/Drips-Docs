# Installation

Als erstes musst du
[Drips herunterladen](https://github.com/Prowect/Drips-Installer/archive/master.zip).
Nachdem du es heruntergeladen hast musst du das ZIP-Archiv entpacken und die Dateien auf deinen Webspace oder deinen Webserver hochladen.
Wenn du einen lokalen Webserver verwendest, kannst du es natürlich auch dort in dein `htdocs` oder `www` Verzeichnis kopieren.

Beachte vor der Installation bitte folgendes:

  - du benötigst einen Apache-<small>*)</small> oder NGINX-Webserver <small>*)</small>
  - du benötigst PHP 5.5 oder höher
  - der Webserver/Drips benötigt Vollzugriff auf das Drips-Verzeichnis (z.B.: Berechtigungen auf `0777` setzen)

> **Achtung:** nach der Installation von Drips solltest du (aus Sicherheitsgründen) deinen Document-Root auf das `public`-Verzeichnis legen.

<small>
*) wenn du einen NGINX-Server verwendest benötigst du folgende Konfiguration:

```nginx
location / {
    if (!-e $request_filename) {
        rewrite ^(.*)$ /index.php;
    }
}
```

*) wenn du einen Apache-Server verwendest musst du `AllowOverride All` in deiner Konfiguration festlegen.
</small>

## Einfache Installation

Nachdem du deine Dateien entsprechend kopiert oder hochgeladen hast, rufst du es über deinen Webbrowser auf.

Es öffnet sich eine Willkommensseite mithilfe der du Drips installieren kannst.

> **Achtung:** wenn du Drips unter Windows installieren möchtest, musst du zuerst eine Umgebungsvariable für PHP setzen!


Als erstes wählst du eine Umgebung (entweder *Development* oder *Production*) aus.

 - Bei *Development* wird Drips im Debug-Modus installiert und bietet zusätzliche Möglichkeiten zum Debuggen deiner Drips-Anwendung.
 - Bei *Production* wird Drips für den Produktivbetrieb konfiguriert, somit werden Fehlermeldungen deaktiviert und die Sicherheit verstärkt.

Danach drückst du auf den Button, um den Installationsvorgang zu starten. Nachdem die Installation erfolgreich abgeschlossen wurde, kannst du mit der Entwicklung deiner Drips-Anwendung loslegen.

## Manuelle Installation

Wenn der Installationsvorgang fehlschlägt oder du die Installation lieber manuell vornimmst, kannst du dies wie folgt machen.

1. öffne dein *Terminal* oder deine *CMD*
2. Navigiere mittels `cd` in dein Drips-Verzeichnis
3. Führe folgendes Kommando aus:

```
php drips install
```

> **Achtung:** bei der manuellen Installation wird Drips immer im Development-Modus installiert. Um auf Production umschalten zu können ist folgendes Kommando notwendig:
```
php drips env prod
```
