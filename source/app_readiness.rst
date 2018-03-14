.. _app readiness:

Industry 4.0 App Readiness
==========================

DockerCompose is the chosen aggregation unit for an App. However, it can be replaced with Kubernetes Pods or Rancherfiles without changing the logical construction of an App.

.. todo::
    Work in progress

App Containers (Docker Subsystem)
---------------------------------

|checkbox| Git repository conforms to ScaleIT template \(Domain Apps, Sidecars folders\)

.. code-block:: none

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
    | | ├── catalogIcon-<app1>.svg //jpg or other format ok
    | | ├── appHubIcon-<app1>.svg //jpg or other format ok
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


|checkbox| Dockerfile -> Docker Build -> Image: includes all needed Dependencies \(Self Contained-ness/in sich geschlossen\)

|checkbox| Docker Compose declares all needed Services \(no other services will be started within the app\)

|checkbox| The App can be started with a single "click" \(docker-compose up\)

|checkbox| Docker Compose declares all needed Volumes \(Data Volume + Log Volume\)

|checkbox| The App can be stopped and restarted without domain data loss or \(docker-compose stop/restart\)

|checkbox| The App containers can be deleted without domain data loss \(docker-compose down\)

|checkbox| The App containers can be replaced by new containers without domain data loss or corruption \(docker-compose down + build + up\)

|checkbox| Data Migration check may be necessary

|checkbox| The created containers shut down properly \(no PID 1 zombies\)

|checkbox| Adhere to the `Dockerfile best practices`_

.. _Dockerfile best practices: https://docs.docker.com/develop/develop-images/dockerfile_best-practices/

App Interfaces
--------------

Sinn dieser Interfaces: "Eine Web-UI zu haben um Administration und Datensicht auf die App und das was sie macht zu erlauben".

Administration Endpoint `/admin`

* admin/config
* admin/doc
* admin/log
* admin/status

User Endpoint `/user`

* user/doc
* user/status

Developer Endpoint `/dev`

* dev/doc
* dev/rest
* dev/swagger.yaml

.. todo::
    Insert Link to Spec as Swagger file

App Catalog Entry
---------------------

|checkbox| A separate git repository contains the meta-data from the Resources/Store directory 
in a Rancher-compatible directory structure

|checkbox| Auto-generated entries for this repository \(e.g. git post commit hooks that push 
meta-data to this app-store repository\)

.. code-block:: none
    
    -- templates
    |-- <app1>
    | |-- 0 // App1-Version 0
    | | |-- docker-compose.yml
    | | |-- rancher-compose.yml
    | | |-- answers.txt //environment variables for rancher-compose
    | | |-- README.md
    | |-- 1 // App-Version 1
    | | |-- docker-compose.yml
    | | |-- rancher-compose.yml
    | | |-- README.md
    | |-- catalogIcon-<app1>.svg //jpg or other format ok
    | |-- appHubIcon-<app1>.svg //jpg or other format ok
    | |-- config.yml // meta-data about the app
    | |-- README.md
    |-- <app2>
    | |-- 0 // App2-Version 0
    ...


Contents of the `config.yml`

.. code-block:: none
    
    name: # Name of the Catalog Entry
    description: |
    # Description of the Catalog Entry
    version: # Version of the Catalog to be used
    category: # Category to be used for searching catalog entries
    maintainer: # The maintainer of the catalog entry
    license: # The license
    projectURL: # A URL related to the catalog entry

This information is strongly inspired by the Rancher Catalog system: [http://rancher.com/docs/rancher/v1.2/en/catalog/private-catalog/](http://rancher.com/docs/rancher/v1.2/en/catalog/private-catalog/)

A catalog entry generator can be found here: [https://github.com/slashgear/generator-rancher-catalog](https://github.com/slashgear/generator-rancher-catalog)


App Documentation
-----------------

|checkbox| Readme states the purpose of the App

|checkbox| Readme lists the services and describes them shortly

|checkbox| Playbook includes App Lifecycle commands (pull, start, stop, upgrade)

|checkbox| FAQ

|checkbox| Known common Errors

|checkbox| Architecture Diagramm (eg. UML Deployment Diagramm)

|checkbox| Readme includes logo and screenshots

|checkbox| App Requirements (RAM, CPU, HDD)

|checkbox| Examples:

* `Chronocommand <https://projects.teco.edu/projects/chronocommand-time-sheet-management/repository/chronocommand>`_

* `ScaleIT Gitlab <https://github.com/ScaleIT-Org/sapp-teco-gitlab>`_

### ScaleIT App Compliance Level

|checkbox| App has a User UI

|checkbox| App has an Administration UI

|checkbox| App has the networking information included \(routing address\)


App Behaviour
-------------

|checkbox| Logging

|checkbox| Graceful degradation


Software Engineering
--------------------

|checkbox| Reactive Design \(App Richtlinien\)

|checkbox| [https://projects.teco.edu/projects/scaleit-ap2/wiki/Richtlinien\_App-Entwicklung](
https://projects.teco.edu/projects/scaleit-ap2/wiki/Richtlinien_App-Entwicklung)

Development Process
-------------------

|checkbox| Automated build pipeline


|checkbox| Continuous Integration


|checkbox| Use Dynamic Port ranges 49,152 through 65,535.



.. |checkbox| image:: img/icon_checkbox.png
            :scale: 20%

