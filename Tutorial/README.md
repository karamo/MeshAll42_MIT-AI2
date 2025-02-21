# Tutorial
In diesem Tutorial stelle ich **meinen Weg**, meine steile Lernkurve, bis zu einer erfolgreichen Kommunikation mit BLE-Geräten dar.  
Die einzelnen Schritte sind in Kapitel unterteilt und zeigen meinen jeweiligen Erkenntnisstand.  
Fehler, Änderungsvorschläge, Ideen u.v.a.m. bitte als **Issue** oder unter **Discussions** erstellen.  

Startend mit einer Übersicht von verschiedenen Quellen folgen die weiteren Schritte, die grundsätzlich unabhängig von einem
speziellen BLE-Gerät und können für jede beliebige Anwendung als Ausgangsbasis genommen werden.  
In einzelnen Punkten gehe ich auf die spezielle Kommunikation mit einer **MeshCom-Node** ein.
Diese Teile können aber auch für jedes beliebige andere BLE-Gerät - u.U. in leicht angewandelter Form - verwendet werden.  
Parallel zu dem Programmabschnitten (Blöcken) wird auch das MMI (Mensch-Maschine-Interface), dh. das Design der APP-Oberfläche beschrieben,
welches einen großen Teil der Arbeit ausmacht. Währen der Entwicklung war immer zuerst die **Funktion** wichtiger als das Aussehen.  
Das optische Design sollte dann übersichtlich, logisch und leicht bedienbar sein.

* [TODO] Links zu BLE Entstehung & Spezifizierung
* **BLE-Scan** & "Was ist ohne Connect sichtbar?"
* **Connect** & Abfrage von **Services** & **Characteristics**
* **Receive** empfangen von Daten (Strings,Bytes u.a.)
* **Send** senden von Daten (Strings, Bytes u.a.)

___
***:copyright: 17.2.2025 by OE3WAS - Wolfgang***
