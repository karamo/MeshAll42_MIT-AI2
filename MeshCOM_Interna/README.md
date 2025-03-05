# MeshCOM FW V 4.xx - Interna
Hier werden die "Geheimnisse" der Kommunikation mit der FW via BLE aufgezeigt, da sie zum Zeitpunkt der Entwicklung der APP nicht
verfügbar sind.

## 1) Das Geheimnis der BLE-Pakete

* Arten und Aufbau der Pakete
* Aufforderungen an die FW via BLE

[TODO]

### 1.1) Die verschiedenen Arten der BLE-Pakete
Derzeitiger Stand der Erkenntnis ist, dass grundzätzlich 2 unterschiedliche BLE-Pakete existieren, die man über BLE von der FW 
empfängt und die sich im 1. Zeichen (ASCII/Byte) zu erkennen geben:
* Messages allgemein: **`@...`**
* Datenpakete (JSON): **`D{"KEY":"value", ...}`**
* _gibt es noch andere?_

#### 1.1.1) Messages BLE Empfang
Der Aufbau eines Message-Paketes stammt aus den allerersten Anfängen der FW-Entwicklung und es wird schwierig sein, dies in der
FW v4.xx zu ändern. Ev. werden in der FW v5.xx Änderungen im Aufbau erfolgen.  
Der Aufbau des Message-Protokolls (FW -> BLE -> ...) ist eine Mischung aus ASCII + Bytes + UTF-8, was die Dekodierung schwieriger gestaltet.  

`bb` = Byte  
`hh` = binary combo  
`aa` = Path [ASCII]  
`dt` = Destination + Typ [ASCII] (verschiedene Varianten)  
[weitere Parameter] sind abhängig von der Unterart einer Message

| Typ | Msg-ID | Hop | Path | . | dest | Message | del | [weitere Parameter] |
|----|---|---|---|---|---|---|---|---|
| @: | bb bb bb bb | hh | aa ... aa | > | _**dt**_ | UTF-8 ... | 00 | bb .. bb |

<ins>Varianten für _**`dt`**_</ins>
* `*:` = Message to all
* `123:` = Message to Group __*123*__
* `OE3WAS-12:` = DM (DirectMessage) to __*OE3WAS-12*__
* `*:{CET}` = Date & Time
* `*!` = POS-String

* DM ist dann, wenn DM == eigener CALL
* GRP-Msg dient zum Vergleich mit den abonnierten Gruppen

| Typ | Msg-ID | ??? |
|---|---|---|
| @A | bb bb bb bb | bb bb bb bb bb bb |
| .. | ... | ... |
|---|---|---|

...

Diese Datenstruktur & Liste sind u.U. unvollständig und können auf Grund neuer Erkenntnisse geändert werden.  
[TODO]

#### 1.1.2) Datenpakete via BLE empfangen
Da Datenpakete als ein JSON-String formatiert sind, lassen sich die **`"key":"value"`** Paare recht einfach dekodieren.
Es wäre so einfach gewesen, alle BLE-Daten als String empfangen zu können. Aber auf Grund des unsäglichen Aufbaus des Message
Protokolls war es erforderlich, **alle Daten als Bytes zu empfangen** und diese Byte-Folge in UTF-8 umzukonvertieren.

Bei den Datenpaketen ist der grundsätzliche Aufbau so, dass im Key **`"TYP":"xx"`** das **`"xx"`** verschiedene Werte annehmen
kann und so die Pakete unterscheidet.  

Folgende Typen (Value) sind derzeit bekannt:  
* **"I"** == `--info`
* **"SE"** == `--seset`
* **"SW"** == `--wifiset`
* **"SN"** == `--nodeset`
* **"W"** == `--wx` | `--weather`
* **"G"** == `--pos`
* **"SA"** == `--aprsset`
* **"MH"**

#### 1.1.3) response Messages
...

## 2) Anforderungspakete aus der APP an die FW
Es gibt verschiedene Anforderungspakete an die FW, also das "Senden".  

#### 2.1) {HELLO}
Zu aller erst muss einmal der initiale Start der Kommunikation durch das sog. {HELLO}-Paket erfolgen,
welches gesendet werden muss. Darstellung als Hex-Bytes:

| 04 10 20 30 |
|---|

In der Folge kommen von der FW mehrere Datenpakete, die die Parameter enthalten (I, SE, ...).  
Auch die noch in der FW empfangenen und gespeicherten Nachrichten werden übertragen (@:).  
Das Ende dieser Übertragung wird durch ein spezielles Datenpaket signalisiert:

| D{"TYP":"CONFFIN"} |
|---|

Daran anschließend können eigene Commands & Messages an die FW geschickt werden.

#### 2.2) (Text)Messages & Commands an die FW via BLE senden
Messages und Commands sind grundsätzlich genauso aufgebaut, wobei `len` die Anzahl der Bytes der Message ist.  
**ACHTUNG:** In UTF-8 sind tw. mehr als 1 Byte/Zeichen!  

| len+2 | A0 | Message Bytes |
|---|---|---|

#### 2.2.1) Beispiele:

`len` & `ID` sind als Hex-Byte dargestellt, die Message bzw. der Command sind als ASCII/UTF-8 dargestellt.
Bei den Commands ist Groß-/Kleinschreibung unbedeutend und wird hier nur der Klarheit wegen unterschiedlich geschrieben.  

| len+2 | ID | (Text)Message/Command |
|---|---|---|
| 08 | A0 | --info |
| 15 | A0 | --setCALL OE3WAS-12 |
| 1C | A0 | {123}Message an Gruppe 123 |
| 27 | A0 | {OE3WAS-11}Direktmessage an OE3WAS-11 |
|---|---|---|

#### 2.3) Config Messages
Es gibt eine Gruppe von Commands, die einen anderen ID habe, aber grundsätzlich gleich aufgebaut sind.
Der jeweilige Command hat aber logischerweise eine eigene Syntax.  
Einige dieser Config Messages sind auch möglich als `--command` abzusenden.

**Config Messages:** 1B length - 1B Msg-ID - Data
<ins>Msg-ID:</ins>
* 0x20 - Timestamp from phone (4B)
* 0x50 - Callsign
* 0x55 - Wifi SSID and PW (1B len - SSID - 1B len - PW)
* 0x70 - Latitude
* 0x80 - Longitude
* 0x90 - Altitude
* 0x95 - APRS Symbols
* 0xF0 - Save Settings to Flash
  * Data:
  * Callsign: 1B len - Callsign
  * Latitude: 4B Float
  * Longitude: 4B Float
  * Altitude: 4B Integer
* WiFi SSID and PWD:
  * 1B - SSID Length - SSID - 1B PWD Length - PWD
* Position Settings from phone are: length 1B | Msg ID 1B | 4B lat/lon/alt | 1B save_settings_flag
	* Save_flag is 0x0A for save and 0x0B for don't save
* If phone send periodicaly position, we don't save them.
* currently we save the settings when the last config arrives which is APRS SYMBOLS - adapt is needed!  
(Aus **FW4.34o03.04(dev)** `phone_commands.cpp` Z.365ff.)


[TODO]

___
***:copyright: 4.3.2025 by OE3WAS - Wolfgang***
