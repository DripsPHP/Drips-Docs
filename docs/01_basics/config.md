# Konfiguration

Sobald du Drips installiert hast, erhältst du ein `config`-Verzeichnis. In diesem befinden sich jeweils eine Konfigurationsdatei für die *Development*- und die *Production*-Umgebung.

Standardmäßig übernimmt die *Production*-Umgebung die Werte der *Development*-Umgebung, aber du kannst dies nach deinen Bedürfnissen anpassen.

Innerhalb der Konfigurationsdatei kannst du Drips konfigurieren.

## Umgebung wechseln

Du kannst die Umgebung (Development / Production) jederzeit wechseln. Führe hierzu einfach folgende Kommandos aus:

**Development-Umgebung aktivieren**
```
php drips env dev
```

**Production-Umgebung aktivieren**
```
php drips env prod
```
