# Android APP - Releases

## 1) Versionen
Hier sind die Versionen/Releases in umgekehrter Reihenfolge aufgelistet, dh. die neueste Version steht als erster Punkt hier.

### 1.6) MeshAll42_V0.5.13.apk - aviso
Einige Ergänzungen und Issues behoben.  
* neues "--tel" Paket unterstützt  
### Download - noch nicht verfügbar, da ich noch die letzten Neuerungen der FW v4.34z einbauen muss !!!
[Releases -> Tags ...](https://github.com/karamo/MeshAll42_MIT-AI2/releases/tag/v0.5.13)  



### 1.5) MeshAll42_V0.5.12.apk
Einige Ergänzungen und Issues behoben.  
Download [Releases -> Tags ...](https://github.com/karamo/MeshAll42_MIT-AI2/releases/tag/v0.5.12)  
* (#15) Sensor MCU-811 & INA226 (20A) ergänzt.
* MCP23017 IO-Erweiterung (derzeit nur **A0..A3** schaltbar, mehr auf Wunsch) (ab FW **4.34w.04.08**)
* HW 45 ergänzt
* GPS farbliche Info
* Multi-Command-Line verwenden.


### 1.4) MeshAll42_V0_5_11.apk
Einige Ergänzungen und Issues behoben.  
Download [Releases -> Tags ...](https://github.com/karamo/MeshAll42_MIT-AI2/releases/tag/v0.5.11)  
* +wahlweise Chat-Elemente (#5)
* (#7) [CONNECT] - [disCON] in einem Button zusammengefasst
* **+Sensoren** Readout & Buttons ON/OFF: BMP280, BME280, BME680, 1-Wire DS18B20 (#15)
* BLE-Liste sicherere Handhabung (#27)
* +POS-Pakete extrahieren & darstellen (#28 u. #29)
* (#30) BUTTON ON/OFF nun ok
* +eigene Aussendungen anzeigen
* +GW/CL in Statuszeile
* +copy->download @ disconnect & back
* +Log-Datei abschaltbar
* weitere Buttons: NO ALL MSG RX [SN:NOALL], TRACK
* eigene Aussendungen farblich gekennzeichnet
* POS-Pakete aus Sprachausgabe genommen

### 1.3) MeshAll42_V0_5_10.apk
Einige Ergänzungen und Issues behoben.  
Download [Releases -> Tags ...](https://github.com/karamo/MeshAll42_MIT-AI2/releases/tag/v0.5.10)  
* +Sprachausgabe der Nachrichten (experimentell)
* +verschiedene Sound-Effekte (abschaltbar)
* +Protokoll-Datei (LogFile) mit Rohdaten (Bytes) und dekodiert
* +Setup-Parameter in der APP speichern
* +DM & GRP Eingabe (#21)
___
### 1.2) MeshAll42_V0_5_5.apk
Einige Ergänzungen und Issues behoben.  
* Schalten von einigen Funktionen ist bereits realisiert. Sensoren fehlen noch. Dafür muss ich erst die kleinen Boards finden, anbauen und in der APP auswerten, was ab **v0.6.0** kommen wird.
* **GPS** sollte schon funktionieren, habe ich aber auch noch nicht am Board. Falls man es einschaltet und es wird nicht gefunden, dann schaltet es sich richtigerweise von selber wieder aus.
___
### 1.1) MeshAll42_V0_5_4.apk
Gegenüber V0.5.3 Verbesserte und erweiterte Version beherrscht u.a. folgende Grundfunktionen:

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

___
***:copyright: 30.4.2025 by OE3WAS - Wolfgang***
