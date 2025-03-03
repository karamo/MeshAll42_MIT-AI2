# MeshCOM FW V 4.xx - Interna
Hier werden die "Geheimnisse" der Kommunikation mit der FW via BLE aufgezeigt, da sie zum Zeitpunkt der Entwicklung der APP nicht
verfügbar sind.

## 1) Das Geheimnis der BLE-Pakete

* Arten der Pakete
* Aufbau der Pakete
* Aufforderungen an die FW via BLE

[TODO]

### 1.1) Die verschiedenen Arten der BLE-Pakete
Derzeitiger Stand der Erkenntnis ist, dass grundzätzlich 2 unterschiedliche BLE-Pakete existieren, die sich im 1.Zeichen (ASCII/Byte)
zu erkennen geben:
* Messages allgemein: **`"@..."`**
* Datenpakete: **`"D{...JSON...}"`**
* _gibt es noch andere?_

#### 1.1.1) Messages
Der Aufbau eines Message-Paketes stammt aus den allerersten Anfängen der FW-Entwicklung und es wird schwierig sein, dies in der
FW v4.xx zu ändern. Ev. werden in der FW v5.xx Änderungen im Aufbau erfolgen.  
Der Aufbau des Message-Protokolls ist eine Mischung aus ASCII + Bytes + UTF-8, was die Dekodierung schwieriger gestaltet.  

| .. | Msg-ID | Hop | Path | . | dest | Message | del | [weitere Parameter] |
|----|---|---|---|---|---|---|---|---|
| @: | bb bb bb bb | hh | aa ... aa | > | dt | UTF-8 ... | 00 | bb .. bb |

`bb` = Byte  
`hh` = binary combo  
`aa` = ASCII  
`dt` = Destination + Typ [ASCII] (verschiedene Varianten)  
"weitere Parameter" sind abhängig von der Unterart einer Message

<ins>Varianten für `dt`</ins>
* `*:` = Message to all
* `123:` = Message to Group __*123*__
* `OE3WAS-12:` = DM (DirectMessage) to __*OE3WAS-12*__
* `*:{CET}` = Date & Time
* `*!` = POS-String
* ...

* DM ist dann, wenn DM == eigener CALL
* GRP-Msg dient zum Vergleich mit den abonnierten Gruppen

Diese Datenstruktur & Liste sind u.U. unvollständig und können auf Grund neuer Erkenntnisse geändert werden.  
[TODO]

#### 1.1.2) Datenpakete
Da Datenpakete als ein JSON-String formatiert sind, lassen sich die **`"key":"value"`** Paare recht einfach dekodieren.
Es wäre so einfach gewesen, alle BLE-Daten als String empfangen zu können. Aber auf Grund des unsäglichen Aufbaus des Message
Protokolls war es erforderlich, alle Daten als Bytes zu empfangen und diese Byte-Folge in UTF-8 umzukonvertieren.

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
* ...
[TODO]

___
***:copyright: 3.3.2025 by OE3WAS - Wolfgang***
