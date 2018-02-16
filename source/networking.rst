Networking
==========

Port-Vergabe
------------

Network Ports für Apps
^^^^^^^^^^^^^^^^^^^^^^

Als Konvention werden Ports innerhalb der Plattform zwischen den dynamischen Ports 49,152 und 65,535 vergeben.

* Port range 49500 through 49599 for platform components
* Port range 49600 through 49699 for business essentials components
* Port range 49700 and above for apps

Port ranges are assigned for companies, e.g. 49700-49900 for Ondics Apps

Tabelle der Port-Konventionen in ScaleIT:

+-------+----------------+-------------------------------------------------------------------------+
|  Port |   Komponente   | Organisation                                                            |
+=======+================+=========================================================================+
|   80  | ScaleIT Proxy  |  ScaleIT-Org                                                            |
+-------+-----+----------+-------------------------------------------------------------------------+
| 49500-50000 ||    **ScaleIT-Org**                                                                |
+-------+-----+------------------------------------------------------------------------------------+
| 49500 | Rancher Server                                                                           |
+-------+------------------------------------------------------------------------------------------+
| 49501 | App Registry                                                                             |
+-------+------------------------------------------------------------------------------------------+
| 49502 | Identity Management                                                                      |
+-------+------------------------------------------------------------------------------------------+
| 49503 | MQTT Broker                                                                              |
+-------+------------------------------------------------------------------------------------------+
| ScaleIT Entwicklungs-Partner                                                                     |
+-------------+------------------------------------------------------------------------------------+
| 50000-50500 ||   ATOS                                                                            |
+-------+-----+------------------------------------------------------------------------------------+
| 50500-51000 ||   Fraunhofer                                                                      |
+-------+-----+------------------------------------------------------------------------------------+
| 51000-51500 ||   KIT                                                                             |
+-------+-----+------------------------------------------------------------------------------------+
| 51500-52000 ||   ondics                                                                          |
+-------+-----+------------------------------------------------------------------------------------+
| 52000-52500 ||   SICK                                                                            |
+-------+-----+------------------------------------------------------------------------------------+
| 53000-53500 ||   SmartHMI                                                                        |
+-------------+------------------------------------------------------------------------------------+
| 54000-54500 ||   ZEISS                                                                           |
+-------------+------------------------------------------------------------------------------------+
| ScaleIT Anwendungs-Partner                                                                       |
+-------------+------------------------------------------------------------------------------------+
| 54500-54600 ||   digiraster                                                                      |
+-------+-----+------------------------------------------------------------------------------------+
| 54600-54700 ||   Feinmetall                                                                      |
+-------+-----+------------------------------------------------------------------------------------+
| 54700-54800 ||   microTEC Südwest                                                                |
+-------+-----+------------------------------------------------------------------------------------+
| 54800-54900 ||   Rood Microtec                                                                   |
+-------+-----+------------------------------------------------------------------------------------+
| 59000-55000 ||   Universität Stuttgart                                                           |  
+-------------+------------------------------------------------------------------------------------+
| Externe Partner                                                                                  |
+-------+-----+------------------------------------------------------------------------------------+
| 55000-55100 ||   ITstrategen                                                                     |
+-------+-----+------------------------------------------------------------------------------------+
| 55100-55200 ||   YUMA technologies                                                               |
+-------+-----+------------------------------------------------------------------------------------+
| 55200-55300 ||   Ingenieurbüro Teichgräber                                                       |
+-------+-----+------------------------------------------------------------------------------------+
| 55300-55400 ||   HS Esslingen                                                                    |
+-------+-----+------------------------------------------------------------------------------------+
| 55400-65536 ||   Frei                                                                            |
+-------+-----+------------------------------------------------------------------------------------+

.. Da wir gleichberechtigte Partner sind, schlage ich die gleiche Zahl von Ports (500 Ports) für alle vor. Nehmen sie bei der Zuteilung am besten eine alphabetische Reihenfolge.

.. je 50 ports für die projektexternen partner,
.. je 100 port für die anwendungspartner im projekt
.. je 500 ports für die entwicklungspartner im projekt
.. ich gehe davon aus, dass i.d.r. eine normale app 2-3
.. ports benötigt (sidecar+app-admin+app-user)

Funktionen der Plattform Essentials (Zentrale Services)
-------------------------------------------------------

App Registry
^^^^^^^^^^^^

In der Referenzplattform durch ETCD implementiert.

- kann von jeder app als key-value store genutzt werden
- der top-node muss der fqdn-name der app sein (z.b.
 /pacman_1.host_1.scaleit)
weitere regeln dazu:
- jede app sollte nur die einträge der eigenen app lesen
- die zentralen apps haben spezielle root-nodes, z.b.
 /apphub
- wenn eine app gelöscht wird kann der node gelöscht werden
 (z.b. von einem registry-cleaner-prozess)
- die apps dürfen den etcd nicht als massendatenspeicher
 nutzen
- systemweite einstellungen finden sich unter /scaleit,
 z.b. /scaleit/language oder /scaleit/brand/company-name...
 alle apps solten das berücksichtigen


Fragen zu den Anforderungen and das Networking in ScaleIT
---------------------------------------------------------

* Der Zugang nach außen soll möglich sein (z.B. "ping google.de")
* Wie werden zentrale Services aus einem Container angesprochen?
    * Ideal wäre sowas wie "ping apphub.coreservice.scaleit"?
* Wie werden andere Container angesprochen? Achtung: Apps können mehrfach instantiiert werden oder auf verschiedenen Hosts laufen!
    * Ideal wäre "ping pacman_1.host_1.scaleit"
* Wie können Services von außen angesprochen werden?
    * Hierzu sollte im Firmennetz *.scaleit.company.com an die ScaleIT-Plattform weitergeleitet werden
    * Der DNS-Name pacman_1.host_1.scaleit.company.com würde dann zur App führen


Was muss in den docker-compose stehen?
    Springe zu `Docker Compose network configuration`_

Was muss auf Docker-Ebene passieren (sollen wir ein eigenes Docker-Netzwerk definieren?)
    Ja, auf Docker (Container) Ebene wird es mehrere Netzwerke geben. Siehe `ScaleIT App Networking`_ 


.. _Docker Compose network configuration:
Docker Compose hier!

.. _ScaleIT App Networking:

ScaleIT App Networking
----------------------

Ein logischer Server mit zentralen Diensten, die nur einmalig im System vorkommen können:

* Rancher
* App-Hub
* Licence Manager
* Yellow Pages (ETCD)
* LDAP / OAuth-Server

Ein oder mehrere Hosts, auf dem Apps laufen.

Diagrams inspired by `_1Backend <https://github.com/1backend/1backend/blob/master/docs/services.md>`_

.. code-block:: none


                Internet                                            Firmen-Intranet
    /------------------------------\ /--------------------------------------------------------------------------------------\
                                                                    ScaleIT-Netz
                                                                  /---------------------------------------------------------\


               client request                  client request                               client request
               to service A                    to service A                                 to service A
    (        ) -----------------> |----------| -----------------> |-----------------------| -----------------> |------------|
    ( client )                    | Firewall |                    | ScaleIT Reverse Proxy |                    |    Apps    |
    (        ) <----------------- |----------| <----------------- |-----------------------| <----------------- |------------|
               service A response              service A response                           service A response
               to client                       to client                                    to client
                                                                  ^
                                                                  |
                                                                  |---- place of instrumentation and other magic

HTTP Request Headers
--------------------

Copy from Github repo

