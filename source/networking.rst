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
| 49500-49699 ||    **ScaleIT-Org**                                                                |
+-------+-----+------------------------------------------------------------------------------------+
| 49500 | Rancher Server                                                                           |
+-------+------------------------------------------------------------------------------------------+
| 49501 | App Registry                                                                             |
+-------+------------------------------------------------------------------------------------------+
| 49502 | Identity Management                                                                      |
+-------+-----+------------------------------------------------------------------------------------+
| 49700-49900 ||   **Ondics GmbH**                                                                 |
+-------+-----+------------------------------------------------------------------------------------+
| 49900-50200 ||   **Karlsruher Institut für Technologie**                                         |
+-------+-----+------------------------------------------------------------------------------------+
| 50200-50500 ||   **Zeiss**                                                                       |
+-------+-----+------------------------------------------------------------------------------------+
| 50500-50800 ||   **SICK AG**                                                                     |
+-------+-----+------------------------------------------------------------------------------------+
| 50800-51100 ||   **HS Esslingen**                                                                |
+-------+-----+------------------------------------------------------------------------------------+
| 50800-51100 ||   **Frei**                                                                        |
+-------+-----+------------------------------------------------------------------------------------+
| 50800-51100 ||   **Frei**                                                                        |
+-------+-----+------------------------------------------------------------------------------------+
| 50800-51100 ||   **Frei**                                                                        |
+-------+-----+------------------------------------------------------------------------------------+
| 50800-51100 ||   **Frei**                                                                        |
+-------+-----+------------------------------------------------------------------------------------+
| 51100 |             ...                                                                          |
+-------+------------------------------------------------------------------------------------------+
| 49701 |            ...                                                                           |
+-------+------------------------------------------------------------------------------------------+


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

