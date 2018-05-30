<img src="https://raw.githubusercontent.com/ScaleIT-Org/media-ressources/master/logo/scaleit-logo.png" alt="ScaleIT Node.js App Skeleton" width="40%">

# Create your own ScaleIT APP:

To create your own ScaleIT application for the ScaleIT [architecture][13], there are many dependencies, structures or requirements you should take care of. Fortunately, we already did lot of the work for you and created many examples, templates and documentation about this procedure. In this article, I will show you how to use these already existing structures to create your own ScaleIT application with ease.

If you are new to the whole ScaleIT world I would suggest you to first read our basic [documentation][1] about the platform to get a quick overview about the main aspects why you or your company should use it.

### Install Dependencies

First of all, make sure [Docker][4] and [Docker Compose][8] is installed on your machine.
To set up your programming environment you should also install [ASP.Net][5] or [NodeJS][6] (regarding to your backend decision) and the [NPM][7] package manager. For problems or new versions please refer to the respective sources.

### Getting Started

As I mentioned before there are already some templates and [sidecars](#furtherReading) you should use to get started with your ScaleIT app. Before you start you should know the specified project's structure which all applications should follow to keep consistency and to orientate yourself faster through a project, developed by someone else. Use [this][17] repo as your starting point. You can see the desired folder structure and templates for the documentation (e.g. Readme) ...

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
    | | ├── catalogIcon-<app1>.svg //jpg,png or other format ok
    | | ├── appHubIcon-<app1>.svg //jpg,png or other format ok
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
    | | └── <some other files>
    | └── DomainContainer2/
    | └── Dockerfile
    └── Platform Sidecars/ [optional]
    . ├── SidecarContainer1/
    . | ├── Dockerfile
    . | └── <some other files>
    . └── SidecarContainer2/
    . . └── Dockerfile
For further documentation check [this][9] out.

The 'Domain Software' directory has to contain all logic your app supports.
We provide a simple [Ionic frontend][18] with either [ASP.Net][2] or [NodeJS][3] backend where you can romp around with your programming skills.
A good way to utilize these modules is to use git submodule composition.
E.g. add the [dotnet api backend][2] to your domain software with the following line of code:

    git submodule add https://github.com/ScaleIT-Org/dotnet-api-backend-skeleton.git "Domain Software/dotnet-api-backend-skeleton"

additionaly add the [Ionic frontend][18]:

    git submodule add https://github.com/ScaleIT-Org/ionic-app-skeleton.git "Domain Software/ionic-app-skeleton"

For the build process you need to provide a dockerfile in the 'Domain Software' folder and adjust the main docker-compose.yml
e.g.

    version: '2'

    services:
      my-app:
          build: Domain Software/
          ports:
              - "HOSTPORT:CONTAINERPORT"

You can see a working example in [this][19] repo with [dotnet api backend][2] and [Ionic frontend][18].

Our chosen app architecture (seen in fig. 1) also includes the opportunity to use several [sidecars](#furtherReading). These are additional independent software parts you can add to your dockerized application to run next to your domain software, which can be used to add desired specific functionality. For example an registration service to our central app-registry as seen in fig. 1

![alt text](https://github.com/ScaleIT-ORG/spsc-app-registration/raw/master/Resources/Documentation/architecture.png "App Architecture")*Figure 1: App Architecture*

The easiest way to build and run everything is to move to your main project folder and execute  ```docker-compose up```
This builds your docker images and starts them.
The [NodeJS][3] version should then be accessible under ```localhost:3000``` and asp.net version under  ```localhost:5002```.

### Standalones
If you want to run everything local without the docker virtualization read the following section.

The following step is separated into two independent sections for the two backend versions:
____
###### - NodeJS
Clone the NodeJS-Backend template:
```
#NodeJS
git clone git@github.com:ScaleIT-Org/nodejs-backend-skeleton.git
```

then go into the root of the newly created folder and resolve the dependencies with [NPM][7].
```
cd nodejs-backend-skeleton+ohzeq  .git
npm install
```
as next step you need to build the frontend. This is also done with NPM where some ionic scripts are executed. In this step the whole frontend will be build, typescripts transformed and dependencies resolved. Everything with the following simple command:
```
npm run build
```
isn't it easy?
Now you can start everything with:
```
node server.js
```
Go to your internet browser and check ```localhost:3000```
____
###### - ASP.NET
Clone the ASP.NET-Backend template:
```
#ASP.NET
git clone git@github.com:ScaleIT-Org/dotnet-api-backend-skeleton.git
```
go into the root of the newly created folder and resolve the asp.net project dependencies:
```
dotnet restore
```
the next step is similar to with the nodejs version. To resolve the dependencies for your frontend execute:
```
npm install
```
as next step you need to build the frontend. The ionic scripts to transform the typescripts are executed during the dotnet build process. Just run the following simple command:
```
dotnet build
```

Go to your internet browser and check ```localhost:5000```
____

If everything went well you should see the following screen in your browser:

| Mobile        | Desktop       |
| ------------- | ------------- |
| <img src="https://raw.githubusercontent.com/ScaleIT-Org/ionic-app-skeleton/master/Resources/Store/Screenshots/Mobile%20Main%20Page.png?raw=true"/> | <img src="https://raw.githubusercontent.com/ScaleIT-Org/ionic-app-skeleton/master/Resources/Store/Screenshots/Desktop%20Main%20Page.png?raw=true"/> |

|Administration view with configurable endpoints| Tech Stack |
| ------------- | ------------- |
| <img width="100%" src="https://github.com/ScaleIT-Org/ionic-app-skeleton/blob/master/Resources/Store/Screenshots/Administration.png?raw=true"/> | <p align="center"><img width="40%" src="https://raw.githubusercontent.com/ScaleIT-Org/ionic-app-skeleton/master/Resources/Documentation/tech-stack.png?raw=true"/> <p align="center">Webpack->(Typescript->Angular->Ionic)->Compiled HTML, JS, CSS</p></p>|
Figure 2: Ionic Sample Frontend

#### Create Your Own Content

Now that everything is up and running it is on you to implement your ideas for a convenient ScaleIT application.
To easily get started we collected the links to the used technologies:

- [Ionic Framework][10] (Frontend)
- [Ionic Icons][16] (Frontend)
- [AngularJs][11] (Frontend)
- [Typescript][12] (Frontend)
- [NodeJs][6] (Backend)
- [ASP.NET][5] (Backend)
- [Docker][4] (Virtualization)
- [Docker Compose][8] (Virtulization)

Notes on the features of the App Skeleton:

* The logo located at /src/assets/logo.png will be automatically converted to all white - keep in mind to create a version with transparent background.

<a name="furtherReading">
If you want further reading material about used concepts check this out:

- Sidecar Pattern
  - [Sidecar Article][14]
  - [Sidecar Pattern][15]
</a>


#### Check App Readiness

After you modified your app there is one more step to do.
We constructed a so called [App Readiness Checklist][9] where we defined some rules and constraints to maintain a consistent structure and behaviour under all existing ScaleIT applications. So checkout our [checklist][9] and verify that your app is compliant with applicable standards.

[1]: http://scaleit-platform-documentation.readthedocs.io/en/latest/index.html
[2]: https://github.com/ScaleIT-Org/dotnet-api-backend-skeleton
[3]: https://github.com/ScaleIT-Org/nodejs-backend-skeleton
[4]: https://www.docker.com/
[5]: https://www.asp.net/
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
