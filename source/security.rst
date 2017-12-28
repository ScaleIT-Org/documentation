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
