# Erstelle deine eigene ScaleIT APP:

Es gibt einige Abhängigkeiten, Strukturen oder Voraussetzungen, die beim Erstellen einer eigenen ScaleIT App bezüglich der ScaleIT  [Architektur][13] bedacht werden sollten. Glücklicherweise hat das ScaleIT Team bereits viele Arbeiten erledigt und stellt Beispiele, Vorlagen, [Sidecars](#furtherReading) und Anleitungen zu dieser Prozedur bereit. In diesem Artikel wollen wir dir zeigen, wie einfach du deine eigene ScaleIT-App aus bereits existierenden Strukturen erstellen kannst.

Falls die ScaleIT Welt neu für dich ist, empfehlen wir zuerst die grundlegende [Dokumentation][1] der Plattform zu lesen. Damit bekommst du einen Überblick über die wichtigsten Funktionen und Gründe, warum du oder dein Unternehmen die Plattform nutzen solltet.


Die folgende Abbildung zeigt den Erstellungsprozess einer App:

![App Creation Circle](
https://raw.githubusercontent.com/ScaleIT-Org/media-ressources/master/miscellaneous/app_creation_circle.png "App Creation Circle")*Figure 1: App Creation Circle*

### 1) Technology Stack

#### Installations-Voraussetzungen

- [ ] [Docker][4]
- [ ] [Docker Compose][8]
- [ ] [NodeJS / npm][6]  
- [ ] [.Net Core][5]
- [ ] [AngularJs][11]
- [ ] [Ionic][18]

Versichere dich zuerst, dass [Docker][4] und [Docker Compose][8] installiert sind. Um dein Programmierumfeld fertig zu stellen, solltest du außerdem [.Net Core][5] oder [NodeJS][6] (Abhängig von deiner Backend Entscheidung) und den [npm][7] Paketmanager installieren. Bei Problemen oder für neue Versionen kannst du auf die jeweiligen Quellen zurückgreifen. [AngularJs][11] und [Ionic][18] werden automatisch mit [npm][7] installiert. Dieses Verhalten ist in der package.json Datei im Stammverzeichnis deines Projekts definiert.

### 2) Meta Skeleton

#### Erste Schritte

- [ ] [Meta Skeleton][17]

Wie zuvor erwähnt, gibt es bereits Vorlagen und [Sidecars](#furtherReading), die du nutzen solltest, um mit deiner ScaleIT-App zu beginnen. Es empfiehlt sich die spezifizierte Projektstruktur kennenzulernen, der alle Applikationen der Einheitlichkeit und Übersichtlichkeit wegen folgen sollten. Nutze [dieses][17] Repo als Anfangsvorlage. Du siehst die gewünschte Ordnerstruktur, und Vorlagen für die Dokumentation (z.B. Readme).

    <app_name>
    ├── docker-compose.yml
    ├── dc.build.yml [optional]
    ├── .env.default
    ├── .env.test.default [optional]
    ├── .env.staging.default [optional]
    ├── .env.production.default [optional]
    ├── README
    ├── Resources/
    | ├── Documentation/
    | ├── Rancher/
    | | ├── catalogIcon-&lt;app1&gt;.svg //jpg,png or other format ok
    | | ├── appHubIcon-&lt;app1&gt;.svg //jpg,png or other format ok
    | | ├── config.yml // meta-data about the app
    | | └── Screenshots/ // App Screenshots
    | | | └── 1.jpg
    | | └── Versions/
    | | .   └── 0/
    | | .   . └── docker-compose.yml // compose version 2 due to compatibility reasons
    | | .   . └── rancher-compose.yml
    | └── Documentation/
    | └── README
    ├── Domain Software/
    | ├── DomainContainer1/
    | | ├── Dockerfile
    | | └── &lt;some other files&gt;
    | └── DomainContainer2/
    | └── Dockerfile
    └── Platform Sidecars/ [optional]
    . ├── SidecarContainer1/
    . | ├── Dockerfile
    . | └── &lt;some other files&gt;
    . └── SidecarContainer2/
    . . └── Dockerfile
Weitere Informationen dafür findest du [hier][9].

### 3) Skeletons

- [ ] [.NetCore Backend][2]
- [ ] [NodeJS Backend][3]
- [ ] [Ionic frontend][18]

Das "Domain Software" Verzeichnis enthällt die komplette Logik deiner App. Wir bieten ein simples [Ionic frontend][18] mit wahlweise einem [.NetCore][2] oder [NodeJS][3] Backend, an denen du deine Programmierfähigkeiten auslassen kannst. Ein guter Weg diese Module zu nutzen ist "git submodule composition". Füge z.B. das [dotnet api backend][2] zu deiner Domain Software mit folgendem Code hinzu:

    git submodule add https://github.com/ScaleIT-Org/dotnet-api-backend-skeleton.git "Domain Software/dotnet-api-backend-skeleton"

Ergänze zusätzlich das [Ionic frontend][18]:

    git submodule add https://github.com/ScaleIT-Org/ionic-app-skeleton.git "Domain Software/ionic-app-skeleton"

Gehe für den Aufbauprozess sicher, dass sich ein dockerfile im "Domain Software" Ordner befindet und passe das main docker-compose.yml an.
Zum Beispiel:

    version: '2'

    services:
      my-app:
          build: Domain Software/
          ports:
              - "HOSTPORT:CONTAINERPORT"

Ein Beispiel dazu findest du in [diesem][19] Repo mit [dotnet api backend][2] und [Ionic frontend][18].

Anmerkungen zu den Eigenschaften des App Gerüsts:

* Das Logo unter /src/assets/logo.png wird automatisch komplett weiß konvertiert - Denke daran auch eine Version mit transparentem Hintergrund zu erstellen.

#### Standalones
Wenn du alles Lokal, ohne die Docker Virtualisierung betreiben möchtest, lese den folgenden Abschnitt.

Der nächste Schritt ist aufgeteilt in zwei unabhängige Teile für die zwei Backend Versionen:

____
###### - NodeJS
Dupliziere die NodeJS-Backend Vorlage:
```
#NodeJS
git clone git@github.com:ScaleIT-Org/nodejs-backend-skeleton.git
```

Gehe nun zum Ursprung des neu erstellten Ordners und löse die Abhängigkeiten mit [NPM][7] auf.
```
cd nodejs-backend-skeleton
npm install
```
Im nächsten Schritt musst du das Frontend erstellen. Das funktioniert auch mit [NPM][7]. Hierbei wird mit den ionic scripts durchgeführt das gesamte Frontend gebaut, typescripts umgewandelt und diverse Abhängigkeiten aufgelöst. Alles mit folgendem Befehl:
```
npm run build
```
Das war einfach, nicht wahr?
Jetzt kannst du alles starten mit:
```
node server.js
```
Gehe in deinen Internet-Browser und prüfe ```localhost:3000```
____
###### - ASP.NET
Dupliziere die ASP.NET-Backend Vorlage:
```
#ASP.NET
git clone git@github.com:ScaleIT-Org/dotnet-api-backend-skeleton.git
```
Gehe zum Ursprung des neu erstellten Ordners und löse die asp.net Projektabhängigkeiten auf.
```
dotnet restore
```
Der nächste Schritt ist identisch zu der NodeJS Version. Führe folgenden Befehl aus, um die Abhängigkeiten für dein Frontend aufzulösen:
```
npm install
```
Nun musst du das Frontend aufbauen. Die ionic scripts, welche die typescripts kompilieren, werden während dem dotnet build Prozess automatisch ausgeführt. Führe einfach folgenden Befehl aus:
```
dotnet build
```

Gehe in deinen Internet-Browser und prüfe ```localhost:5000```
____

Wenn alles geklappt hat solltest du jetzt folgenden Bildschirm in deinem Browser sehen:

| Mobile        | Desktop       |
| ------------- | ------------- |
| <img src="https://raw.githubusercontent.com/ScaleIT-Org/ionic-app-skeleton/master/Resources/Store/Screenshots/Mobile%20Main%20Page.png?raw=true"/> | <img src="https://raw.githubusercontent.com/ScaleIT-Org/ionic-app-skeleton/master/Resources/Store/Screenshots/Desktop%20Main%20Page.png?raw=true"/> |

|Administration view with configurable endpoints| Tech Stack |
| ------------- | ------------- |
| <img width="100%" src="https://github.com/ScaleIT-Org/ionic-app-skeleton/blob/master/Resources/Store/Screenshots/Administration.png?raw=true"/> | <p align="center"><img width="40%" src="https://raw.githubusercontent.com/ScaleIT-Org/ionic-app-skeleton/master/Resources/Documentation/tech-stack.png?raw=true"/> <p align="center">Webpack->(Typescript->Angular->Ionic)->Compiled HTML, JS, CSS</p></p>|
Figure 2: Ionic Sample Frontend

### 4) Sidecars

- [ ] [App Registration Sidecar][21]
- [ ] [OAuth Sidecar][20]

Unsere gewählte App-Architektur (Siehe Fig. 1) beinhaltet auch die Möglichkeit mehrere [Sidecars](#furtherReading) zu nutzen. Diese sind zusätzliche, unabhängige Softwareteile, die du zu deiner App hinzufügen kannst. Sie laufen neben der Domain Software und können für weitere gewünschte Funktionen genutzt werden. Zum Beispiel einen Registrierungsservice zu unserem zentralen App-Register, wie in Fig. 2.

![alt text](https://github.com/ScaleIT-ORG/spsc-app-registration/raw/master/Resources/Documentation/architecture.png "App Architecture")*Figure 2: App Architecture*

Der einfachste Weg alles zu bauen und zu betreiben ist, sich in den Haupt-Projektordner zu bewegen und ```docker-compose up``` auszuführen.
Das erstellt und startet deine Docker Images. Die [NodeJS][3] Version sollte dann unter ```localhost:3000``` und die [.NetCore][2] Version unter ```localhost:5002``` erreichbar sein.
#### Beispiel

Unser Musterbeispiel findest du [hier][22].

### 5) Rancher Catalog

In Arbeit.

### 6) Readiness Checklists

- [ ] [App Readiness Checklist][9]
- [ ] [Eco System Readiness Checklist][9]

Nachdem du deine App angepasst hast, gibt es noch einen weiteren Schritt zu erledigen. Wir haben eine sogenannte [App Readiness Checklist][9] erstellt, in der wir einige Regeln und Bedingungen definiert haben. Diese sind nötig, um eine einheitliche Struktur und Verhalten aller ScaleIT-Apps gewährleisten zu können. Überprüfe anhand unserer [Checkliste][9] die Konformität deiner App mit den geltenden Standards.

### 7) Erstelle deine eigenen Inhalte

Jetzt, da alles erstellt und bereit ist, liegt es an dir, deine Ideen für eine geeignete ScaleIT-App einzubringen. Für einen einfachen Start haben wir die Links zu den genutzten Technologien gesammelt:

- [ ] [ScaleIT Repo][23] (Skeletons/Examples/Documentation)
- [ ] [Ionic Framework][10] (Frontend)
- [ ] [Ionic Icons][16] (Frontend)
- [ ] [AngularJs][11] (Frontend)
- [ ] [Typescript][12] (Frontend)
- [ ] [NodeJs][6] (Backend)
- [ ] [.NetCore][5] (Backend)
- [ ] [Docker][4] (Virtualization)
- [ ] [Docker Compose][8] (Virtulization)

<a name="furtherReading">
Hier findest du weiterführende Erläuterungen zu genutzten Konzepten:

- Sidecar Pattern
  - [Sidecar Article][14]
  - [Sidecar Pattern][15]
</a>

[1]: http://scaleit-platform-documentation.readthedocs.io/en/latest/index.html
[2]: https://github.com/ScaleIT-Org/dotnet-api-backend-skeleton
[3]: https://github.com/ScaleIT-Org/nodejs-backend-skeleton
[4]: https://www.docker.com/
[5]: https://www.microsoft.com/net/download/linux
[6]: https://nodejs.org/en/
[7]: https://www.npmjs.com/
[8]: https://docs.docker.com/compose/
[9]: http://scaleit-platform-documentation.readthedocs.io/en/latest/app_readiness.html
[10]: https://ionicframework.com/docs/components/
[11]: https://docs.angularjs.org/api
[12]: https://www.typescriptlang.org/docs/home.html
[13]: http://scaleit-platform-documentation.readthedocs.io/en/latest/architecture.html
[14]: https://www.voxxed.com/2015/01/use-container-sidecar-microservices/
[15]: https://docs.microsoft.com/en-us/azure/architecture/patterns/sidecar
[16]: https://ionicframework.com/docs/ionicons/
[17]: https://github.com/ScaleIT-Org/sapp-i40-app-skeleton
[18]: https://github.com/ScaleIT-Org/ionic-app-skeleton
[19]: https://github.com/ScaleIT-Org/sapp-ionic-dotnetcore-example
[20]: https://github.com/ScaleIT-Org/kong-sidecar
[21]: https://github.com/ScaleIT-Org/spsc-app-registration-sidecar
[22]: https://github.com/ScaleIT-Org/sapp-sidecar-app-registration-example
[23]: https://github.com/ScaleIT-Org/
