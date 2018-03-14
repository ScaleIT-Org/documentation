Kommunikation auf der ScaleIT Plattform
=======================================

Die Kommunikation auf der ScaleIT Plattform 

Es wird unterschieden zwischen

Meldungen die an eine einzige Entität gehen 



an eine einzige Instanz oder 

Kommunikation zwischen Apps (App-2-App)
---------------------------------------

1:1 Kommunikation (Peer2Peer,Resourcenanfragen)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1:n Kommunikation 9
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


Kommunikation zwischen Apps und der Plattform (App-2-Platform)
--------------------------------------------------------------

Die Kommunikation zwischen Apps und der Plattform (App-2-Platform) wird über den Sidecar-Mechanismus realisiert. Entwickler binden die Platform-Sidecars ein und nutzen die standardisierten HTTP APIs, um darauf zuzugreifen. Dabei ist zu beachten, dass die Sidecars im internen Netzwerk der App mit ihren docker-compose Service Namen angesprochen werden können.

Requests die durch das Routing Sidecar an die App gegeben werden enthalten je nach ausbaustufe der Plattform Informationen zu Identität, Authorisierung, Lizenz etc. - z.B. als HTTP Header. Dadurch, dass der Entwickler dem Sidecar vertraut können diese in der App genutzt werden ohne die zentralen Instanzen anzusprechen. Dadurch wird die Abhängigkeit zu einer bestimmten Plattforminstanz reduziert.

Die Sidecars melden den zentralen Plattformkomponenten (Platform-Essentials?) und Business Essentials wenn es Änderungen gibt. Z.B. HTTP API.

Weil sich hinter diesen zentralisierten Komponenten meist ein Cluster von Anwendungen verbirgt, ... Master-Komponenten und Slave Komponenten...

Kommunikation mit der App Registry
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Kommunikation mit dem Identity-Manager
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Kommunikation mit dem License-Manager
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^