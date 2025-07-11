# MeshCOM FW V 4.xx - Interna
Hier werden die "Geheimnisse" der Kommunikation mit der [**MeshCom-FW**  ](https://github.com/icssw-org/MeshCom-Firmware  ) 
via BLE aufgezeigt, da zum Zeitpunkt der Entwicklung der APP keine aureichenden, detailierten Infos verfügbar waren.

## 1) Das Geheimnis der BLE-Pakete

* (FW -> BLE -> APP) Arten und Aufbau der Pakete
* (FW <- BLE <- APP) Aufforderungen an die FW via BLE

#### 1.1) Die verschiedenen Arten der BLE-Pakete
Derzeitiger Stand der Erkenntnis ist, dass grundzätzlich 2 unterschiedliche BLE-Pakete existieren, die man über BLE
von der FW empfängt und die sich im 1. Zeichen (ASCII/Byte) zu erkennen geben:
* Messages allgemein: **`@...`**
* Datenpakete (JSON): **`D{"KEY":"value", ...}`**
* _gibt es noch andere?_

#### 1.1.1) Messages via BLE empfangen
Der Aufbau eines Message-Paketes stammt aus den allerersten Anfängen der FW-Entwicklung und es wird schwierig sein, dies in der
FW v4.xx zu ändern. Ev. werden in der FW v5.xx Änderungen im Aufbau erfolgen.  
Der Aufbau des Message-Protokolls (FW -> BLE -> APP) ist eine Mischung aus ASCII + Bytes + Combo-Bytes + UTF-8, was die Dekodierung
schwieriger gestaltet.  

`bb` = Byte  
`hh` = binary combo  
`aa` = Path [ASCII]  
`dt` = Destination + Typ [ASCII] (verschiedene Varianten)  
[weitere Parameter] sind abhängig von der Unterart einer Message

| Typ | Msg-ID | Hop | Path | del | dest | Message | del | [weitere Parameter] |
|----|---|---|---|---|---|---|---|---|
| @: | bb bb bb bb | hh | aa ... aa | > | _**dt**_ | UTF-8 ... | 00 | bb .. bb |

<ins>Varianten für _**`dt`**_</ins>
* `*:` = Message to all
* `123:` = Message to Group __*123*__
* `OE3WAS-12:` = DM (DirectMessage) to __*OE3WAS-12*__
* `*:{CET}` = Date & Time (wird nur übertragen, wenn GW ist; bei CL nicht)
* `*!` = POS-String

* DM ist dann, wenn DM == eigener CALL
* GRP-Msg dient zum Vergleich mit den abonnierten Gruppen

#### 1.1.2) ACK-Paket empfangen

| Typ | Msg-ID | ACK |
|---|---|---|
| @A | bb bb bb bb | bb bb bb bb bb bb |
|---|---|---|

#### 1.1.3) response Messages
...  
...  
[TODO] Diese Datenstruktur & Liste sind u.U. unvollständig und können auf Grund neuer Erkenntnisse geändert werden.  

#### 1.1.4) Datenpakete via BLE empfangen
Da Datenpakete als ein JSON-String formatiert sind, lassen sich die **`"key":"value"`** Paare recht einfach dekodieren.
Es wäre so einfach gewesen, alle BLE-Daten als String empfangen zu können. Aber auf Grund des unsäglichen Aufbaus des Message
Protokolls war es erforderlich, **alle Daten als Bytes zu empfangen** und diese Byte-Folge in UTF-8 umzukonvertieren.

Bei den Datenpaketen ist der grundsätzliche Aufbau so, dass im Key **`"TYP":"xx"`** das **`"xx"`** (Value) verschiedene Werte
annehmen kann und so die Pakete unterscheidet.  

Folgende Typen (Value) sind derzeit bekannt:  
* **"I"** == `--info`
* **"SE"** == `--seset`
* **"SW"** == `--wifiset`
* **"SN"** == `--nodeset`
* **"W"** == `--wx` | `--weather`
* **"G"** == `--pos`
* **"SA"** == `--aprsset`
* **"MH"**


## 1.2) Anforderungspakete aus der APP an die FW
Es gibt verschiedene Anforderungspakete an die FW, also das "Senden".  
Falls nicht anderes vermerkt, ist Darstellung als Hex-Bytes (0x..).

#### 1.2.1) {HELLO}
Zu aller erst muss einmal der initiale Start der Kommunikation durch das sog. {HELLO}-Paket erfolgen,
welches gesendet werden muss.
| 04 10 20 30 |
|---|

In der Folge kommen von der FW mehrere Datenpakete, die die Parameter enthalten (I, SE, SW, SN, W, G, SA).  
Auch die noch in der FW empfangenen und gespeicherten Nachrichten werden übertragen (@:).  
Das Datenpaket mit dem **"TYP":"MH"** wird zwischendurch mal gesendet.  
Das Ende dieser Übertragung wird durch ein spezielles Datenpaket signalisiert:

| D{"TYP":"CONFFIN"} |
|---|

#### 1.2.1.1) Timestamp
Anschließend an **CONFFIN** schickt die APP ein Timestamp-Paket, z.B.:  
```
06 20 CF 7D DE 67 
[BLE] Timestamp from phone (sec) <UTC>: 1742634447 -> 2025.03.22 09:07:27
```
![grafik](https://github.com/user-attachments/assets/3630bd99-e84d-4d96-b1a1-6ccc4b72c983)

Daran anschließend können eigene Commands & Messages an die FW geschickt werden.

#### 1.2.2) (Text)Messages & Commands an die FW via BLE senden
Messages und Commands sind grundsätzlich gleich aufgebaut, wobei `len` die Anzahl der Message-Bytes ist,
gefolgt von der Msg-ID und den Message-Bytes.  
**ACHTUNG:** In UTF-8 sind tw. mehr als 1 Byte/Zeichen!  

| len+2 | A0 | Message-Bytes |
|---|---|---|

#### 1.2.2.1) Beispiele:

`len` & `ID` sind als Hex-Byte dargestellt, die Message bzw. der Command sind als ASCII/UTF-8 dargestellt.
Bei den Commands ist Groß-/Kleinschreibung unbedeutend und wird hier nur der Klarheit wegen unterschiedlich geschrieben.  

| len+2 | ID | (Text)Message/Command |
|---|---|---|
| 08 | A0 | --info |
| 15 | A0 | --setCALL OE3WAS-12 |
| 1C | A0 | {123}Message an Gruppe 123 |
| 27 | A0 | {OE3WAS-11}Direktmessage an OE3WAS-11 |
|---|---|---|

#### 1.2.3) Config Messages
Es gibt eine Gruppe von Commands, die einen anderen ID habe, aber grundsätzlich gleich aufgebaut sind.
Der jeweilige Command hat aber logischerweise eine eigene Syntax.  
Einige dieser Config Messages sind auch möglich als `--command` abzusenden.

<ins>Msg-ID:</ins>
* 0x20 - Timestamp from phone [4B]
* 0x50 - Callsign (`--setCALL`) [1B len - Callsign]
* 0x55 - Wifi SSID (`--setSSID`) and PWD (`--setPWD`) [1B - SSID Length - SSID - 1B PWD Length - PWD]
* 0x70 - Latitude (`--setLAT`) [1B length + 1B Msg-ID + 4B lat + 1B save_flag]
* 0x80 - Longitude (`--setLON`) [1B length + 1B Msg-ID + 4B lon + 1B save_flag]
* 0x90 - Altitude (`--setALT`) [1B length + 1B Msg-ID + 4B alt + 1B save_flag]
* 0x95 - APRS Symbols (`--symID` `--symCD`)
* 0xF0 - Save Settings to Flash
* **save_flag** is `0x0A` for save and `0x0B` for don't save
* If phone send periodicaly position, we don't save them. (???)  
(Aus Z.365ff https://github.com/icssw-org/MeshCom-Firmware/blob/oe1kfr_434q/src/phone_commands.cpp)


[TODO] weitere Infos folgen ...


## 2) Externe Hardware
Als "externe Hardware" werden verschiedene Sensoren und eine Digital-I/O-Erweiterung beschrieben.

### 2.1) Sensoren
In der MT-FW 4.34v werden verschiedene Sensoren unterstützt. Nicht alle sind derzeit ausreichend beschrieben. Daher versuche ich hier ein möglichst detailierte Beschreibung zu erstellen, mit den einzelnen Parametern zu den jeweiligen Sensoren.

#### 2.1.1) Umweltdaten
Die wichtigsten üblichen Umweltdaten sind: **Temperatur** [°C], **rel.Feuchte** [%rH], **Luftdruck** [hPa]  
Weiter Parameter sind: **Luftqualität**, **CO<sub>2</sub>** [ppm] u.a.

| Type | IO | Addr | Messwerte |
|---|---|---|---|
| BMP280 | I²C | 76 | T* [°C] - P [hPa]<br>/T=[°C] /P=[hPa]<br>BLE: ... |
| BME280 | I²C | 76 | T* [°C] - H [%rH] - P [hPa]<br>/T=[°C] /H=[%rH] /P=[hPa] /Q=[hPa]<br>BLE: ...|
| BME680 | I²C | 76/77 | T [°C] - H [%rH] - P [hPa] - GASres [kΩ]<br>/T=[°C] /H=[%rH] /P=[hPa] /F=[m] /G=[kΩ] /V=3<br>BLE: ... |
| DS18B20 | 1-W | -- | T [°C]<br>/O=[°C]<br>BLE: ... |
| MCU811 | I²C | 5A | CO<sub>2</sub> [ppm]<br>/C=[ppm] /V=2<br>BLE: ... |

* **Addr** in Hex  
* **/X** = Kennung in POS-Msg (V=2 hat Priorität gegenüber V=3)  
* **(*)** = die Temperatur dient zur internen Kompensation und ist daher etwas höher als reale Umwelt.  
* **MCU811** WAK-GND Verbindung zusätzlich zu I²C.

#### 2.1.2) Messwerte
Derzeit wird offiziell nur ein **INA226** (Spannung[V]-Strom[A]-Leistung[W] Sensor in der 20A-Ausführung mit einem **R<sub>S</sub>=2 mΩ** [R002]) unterstützt.

| Type | IO | Addr | Messwerte |
|---|---|---|---|
| INA226 | I²C | 40 | /U=vbus[V], /I=vcurrent[A] /V=5<br>BLE: ... |

#### 2.1.3) Digital-I/O MCP23017
Es wird ein **MCP23017** 16-Pin-I/O auf **I²C** Addr=**0x20** unterstützt.  
Die 16 IOs sind durch A0..A7, B0..B7 gekennzeichnet.
Die Steuerung ist via **Terminal**, **BLE** & **UDP** (Web-Client) möglich.  

| Type | IO | Addr | Messwerte als BLE-JSON Paket |
|---|---|---|---|
| MCP23017 | I²C | 20 | D{"TYP":"IO","MCP23017":true,"AxOUT":"00000000","AxVAL":"11111111", "BxOUT":"00000000","BxVAL":"11111111"} |

| Parameter | |
|---|---|
| MCP23017 | {true \| false} = erkannt? |
| AxOUT | "00000000" = A7..A0, "1" = OUTPUT, "0" = INPUT |
| AxVAL | "00000000" = A7..A0, "1" = HIGH, "0" = LOW |
| BxOUT | "00000000" = B7..B0, "1" = OUTPUT, "0" = INPUT |
| BxVAL | "00000000" = B7..B0, "1" = HIGH, "0" = LOW |

<ins>Befehle via Terminal & BLE-APP:</ins>
* **`--io`** liefert auf BLE ein JSON-Paket
* **`--setio clear`** setzt alle IOs auf INPUT
* **`--setio {A0..A7,B0..B7} {in | out}`** setzt die Funktion des gewählten IO auf **INPUT** oder **OUTPUT**
* **`--setout {A0..A7,B0..B7} {high | low}`** setzt den gewählten IO auf **HIGH** oder **LOW**



___
***:copyright: 11.7.2025 by OE3WAS - Wolfgang***
