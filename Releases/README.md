# Android APP - Releases

### MeshAll42_V0_5_3.apk
Die erste hier verfügbare Pre-Version beherrscht folgende Grundfunktionen:

<ins>Ablauf:</ins>  
* **[SCAN]** Scannen von BLE-Geräten
* **[CONNECT]** verbinden mit einem **MeshCom-Node**
  * **[Reg]** registrieren für den Empfang von Daten (automatisch)
  * **{HELLO}** Start der Kommunikation (automatisch)
  * empfangen der Grundeinstellungen und teilweises Darstellen derselben (automatisch)
* **[disCON]** Verbindung trennen - **!!! nicht vergessen !!!**

<ins>weitere Möglichkeiten:</ins>
* **[commands]** senden von verschiedenen Commands, zB. `--info` `--display off` `--display on` u.a.
* **[<=Send]** senden einer Msg aus einem Eingabefeld
* senden von Command mit Parameter(n) zB. **`--setCALL OE3XXX-12`** u.a.

Empfangene Msg und andere Datenpakete werden decodiert und dargestellt.  
Die Funktionalität der APP wird laufend erweitert.

___
***:copyright: 21.2.2025 by OE3WAS - Wolfgang***
