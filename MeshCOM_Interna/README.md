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
