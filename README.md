# ADS Infrastructure Repository

Dieses Repository enthält die Infrastruktur für die ADS-Übungen. Diese kann mithilfe von Docker
gestartet und benutzt werden. Die Infrastruktur besteht aus folgenden Komponenten:

- Jupyter Notebook Server
- PostgreSQL Datenbank
- Adminer Datenbank-Admin-Tool

## Voraussetzungen

Da für die Infrastruktur lediglich Docker und Git benötigt werden, sind die Voraussetzungen relativ gering.
Ein einigermaßen aktueller Rechner mit Linux, Windows oder macOS sollte ausreichen. Sollte ein
Firmenrechner verwendet werden, muss aller Wahrscheinlichkeit nach im Vorhinein mit der IT-Abteilung des Unternehmens 
gesprochen werden, denn beide Tools müssen installiert werden, ggf. sind Berechtigungen und Firewall-Regeln
anzupassen.

Zudem wird für das Starten der Infrastruktur ein Terminal benötigt. Auf Linux und macOS lässt sich
das Terminal mit dem Befehl "terminal" öffnen. Auf Windows kann das Terminal mit dem Befehl "cmd"
gestartet werden.

### Alternatives Terminal für Windows
Das Standard-Terminal von Windows ist nicht besonders komfortabel und verwendet andere Befehle als
Linux und macOS. Daher empfiehlt es sich, ein alternatives Terminal zu verwenden. Ein gutes Terminal
ist das Git Bash Terminal, welches mit Git mitinstalliert wird. Es kann mit dem Befehl "git bash"
gestartet werden. 

## Installation

### Docker
Docker lässt sich mit Docker Desktop recht einfach installieren. 
Auf der [Docker-Website](https://docs.docker.com/desktop/) befinden sich die wesentlichen Informationen
zur Installation.

### Git
Git ist ein Tool zu Versionsverwaltung. Das bedeutet, dass mit ihm Änderungen an Dateien nachvollzogen
werden können. Außerdem können Änderungen an Dateien zwischen verschiedenen Rechnern synchronisiert werden.
Auf Linux und macOS ist Git in der Regel bereits vorinstalliert. Für Windows kann Git [hier](https://git-scm.com/download/win) 
heruntergeladen werden.

## Vorbereitung

### Option A: Repository klonen
Um das Repository zu klonen, muss einer der folgenden Befehle ausgeführt werden:

Clonen über HTTPS:

```shell
git clone https://github.com/dbuas/ads-docker-infrastructure.git <PROJECT_FOLDER_NAME>
```

Clonen über SSH:

```shell
git clone git@github.com:mhebing/ads-docker-infrastructure.git <PROJECT_FOLDER_NAME>
```

PROJECT_FOLDER_NAME sollte dabei durch den erwünschten Namen des Projektes ersetzt werden.

### Option B: Repository herunterladen
Alternativ kann das Repository auch als ZIP-Datei heruntergeladen werden. Dazu können
die Dateien auf der [Repository-Website](https://github.com/dbuas/ads-docker-infrastructure)
unter Releases heruntergeladen werden.

### Setzen der Umgebungsvariablen
Um die Infrastruktur starten zu können, müssen noch einige Umgebungsvariablen gesetzt werden.
Dazu wird das Konzept der .env-Datei verwendet. Diese Datei enthält die Umgebungsvariablen, die
von Docker automatisch erkannt werden. Ein wichtiger Aspekt dabei ist, dass .env-Dateien **NIEMALS**
in ein Repository eingecheckt werden sollten. Daher wurde die .env-Datei in die .gitignore-Datei eingetragen.
Dadurch wird sie nicht im Repository angezeigt und kann nicht aus Versehen eingecheckt werden.
Es befindet sich eine Beispiel-Datei im Repository, die kopiert werden kann:

```shell
cp .env.example .env
```

Die Datei sollte mit einem beliebigen Texteditor geöffnet und die Variablen entsprechend
angepasst werden.

#### Jupyter Token

Um Zugriff auf Jupyter zu erhalten, muss ein Token gesetzt werden. Dieses Token wird in der 
.env-Datei mit JUPYTER_TOKEN gesetzt. Wenn über den Browser auf Jupyter zugegriffen wird, wird statt
der Notebook-Übersicht ein Fenster angezeigt, in dem das Token eingegeben werden muss. Dieser Token kann
dann aus der .env-Datei kopiert werden.

## Starten der Infrastruktur

Um die Infrastruktur zu starten, muss in das Projektverzeichnis gewechselt werden. Dort kann dann
mit folgendem Befehl die Infrastruktur gestartet werden:

```shell
docker-compose up -d
```

Nachdem die Infrastruktur gestartet wurde, sieht man im Docker Desktop die gestarteten Container.
Wenn alles geklappt hat, sollten dort drei Container zu sehen sein. Zudem sollten die Icons auf der 
linken Seite neben dem Namen der Container grün sein.

Im Docker Desktop sind zudem die Links hinterlegt, um auf die verschiedenen Komponenten zuzugreifen.
Wichtig sind die beiden Links zu Jupyter und Adminer. Diese können im Browser geöffnet werden in dem
auf die Zahlen 8888:8888 oder 8080:8080 geklickt wird. Der Standartbrowser sollte sich dann öffnen.

### Installation zusätzlicher Pakete
Um zusätzliche Pakete in Jupyter zu installieren, müssen diese in der requirements.txt-Datei eingetragen werden.
Diese befindet sich im Ordner jupyter-server. Nachdem die Pakete eingetragen wurden, muss die
Infrastruktur neu gestartet werden. Dazu kann folgender Befehl ausgeführt werden:

```shell
docker-compose down
docker-compose up -d --build
```

Das build flag sorgt dafür, dass der Jupyter Container neu gebaut wird und die neuen Pakete installiert werden.


## Stoppen der Infrastruktur
Nach dem Beenden der Übungen sollte die Infrastruktur wieder gestoppt werden. Dazu kann folgender Befehl

```shell
docker-compose down
```


## TODO
- [ ] Fehlende Pakete in Jupyter installieren