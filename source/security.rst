Sicherheit (Security) auf der ScaleIT Plattform
==============

Für Entwickler
----------

Gegen wen und gegen welche Angriffe schützen wir unsere ScaleIT Instanz?
    Externe Angreifer: 
        Im Falle einer horizontalen Vernetzung oder Erreichbarkeit der Infrastruktur aus dem Internet oder durch ungesicherte WLAN Access-Points.
    Interne Angreifer:
        Interne Angreifer sind immer ein hohes Risiko. ScaleIT bietet durch den App-Aufbau aber Mechanismen, die den Zugriff limitieren, wie z.B. separate Netzwerke für sensible Komponenten innerhalb eine App oder Rollenbasierte API-Zugriffskontrolle.
    Schlechte Software:
        Eine Software kann wissentlich oder unwissentlich Schaden verursachen. Ein Beispiel dafür ist die Ressourcennutzung (PIDs, CPU etc.) oder der Zugriff auf das root Filesystem. Einstellungen die die Angriffsfläche mindern sind in dem ScaleIT SDK eingebaut. Es wird den Entwicklern empfohlen die Standardwerte zu nutzen. Der Review-Prozess im offiziellen ScaleIT-App-Store verifiziert (automatisch) jede neue App, um solche Szenarien zu vermeiden.

.. todo::
    Welche innerhalb und außerhalb von Docker liegenden sicherheitsrisiken gibt es und was tun wir dagegen?
        Beantworten
       

Wenn das "ScaleIT System" nicht auf Kommandozeilenebene zugänglich ist, fallen damit wesentliche risiken weg?
    Nein, solange Container im privilegiertem Modus, mit dem Docker Socket arbeiten oder auf das root Filesystem Zugriff haben, kann man das nicht pauschal sagen.

.. todo::
    Wie organisieren wir das ssl-zertifikat management?
        Brauchen wir eine eigene certificate authority, um an die apps zertifikate auszustellen bzw. diese zu überprüfen? 
            Beantworten

        Wie gehen wir mit ablaufenden zertifikaten um?
            Beantworten

.. todo::
    Welchen Bezug gibt es zu den standards, die auf dem hallenboden und im betrieblichen umfeld gelten (bsi, ...)?
        Beantworten


     iIch bin der Architekt im ScaleIT Projekt.

Für IT-Safety (Data Safety) gibt es Ansätze, aber diese sind im Protoypenstadium. Backups sollen in der komerziellen Version von der Firma Ondics bereitgestellt werden. Fingerprinting, Checksum-Verifikation, Blockchain-Audit oder andere Mechanismen höchstwahrscheinlich nicht. Kritische Apps sollten in separaten VMs laufen damit ein Kernel-Panic nicht das gesamte System mitnimmt. Apps die den maximalen Data Safety App-Level implementieren müssen migrationsskripte und daten-checks mitliefern sowie bei Ausfällen wieder von alleine auf Konsistenz kommen.

Zum Punkt IT-Security an:

Das gesamte System basiert auf Virtualisierung mit Docker und kann zusätzlich auf mehreren physischen oder virtuellen Maschinen installiert werden, je nach dem wie kritisch bestimmte Daten sind und wie stark eine Isolierung erwünscht ist.

Verschlüßelung der Daten innerhalb der Container ist noch experimentell aber prinzipiell leicht zu erreichen, in dem man mit virtuellen Platten und verschlüßelten Dateisystemen arbeitet. RAM Verschlüßelung ist soweit mein Wissensstand ist, auch in der Wissenschaft noch nicht richtig gelöst (oder über spezielle CPUs und Betriebssysteme). Intel SGX may be a solution or TPMs or homomorphic encryption schemes?

Da die Apps komponentenbasiert aufgebaut sind, ist die interne Kommunikation nicht nach außen sichtbar, und nur zugelassene Kommunikation darf nach außen (wenn die passenden Sidecars in der App konfiguriert sind - InApp-Firewall). Den Austausch der Sidecars innerhalb der Apps durch sicherere Komponenten ist eine Operation die sehr wenig Ressourcen in Anspruch nimmt.

Kommunikationsverschlüßelung geht über die gängigen Standards wie HTTPS und MQTTS.

Eine Zugriffskontrolle über Single-Sign-On (OAuth2) ist bald auch komerziell verfügbar, um die Nutzerauthentifizierung zu Erlauben. Über denselben Mechanismus sind dann auch API-Zugriffe implementierbar (wir haben aber diesen Fall noch nicht implementiert - die Konfiguration der Schnittstelle muss noch gemacht werden).

Theoretisch funktionieren alle Sicherheitsmechanismen die in Docker, Cloud-Systemen und dem Web zum Einsatz kommen.

Nutzt man komerzielle Docker-Registries (wie z.B. die Firma SICK), dann gibt es die Möglichkeit für die App-Betriebssysteme und installierten libraries einen automatischen Security Check durchzuführen. (https://coreos.com/quay-enterprise/docs/latest/security-scanning.html) 

Unsere Dokumentation ist noch im entstehen, aber Sie können immer den aktuellen Stand hier aufrufen:
https://github.com/ScaleIT-Org/documentation
