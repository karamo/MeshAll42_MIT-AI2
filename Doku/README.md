# MeshAll42_MIT-AI2
Beschreibung von spezifischen Teilen der APP.

## 1) Protokoll-Datei (Log-File) [ab V0.5.9]

### 1.1) Dateiname
zB.: **`MeshAll42_2025_03_15_01_11_25.txt`**  
`APP-Titel`\_`Erstellungsdatum`\_`Uhrzeit`**.txt**  
* Titel: MeshAll42
* Datum: 15.3.2025
* Uhrzeit: 1:11:25

### 1.2) Inhalt
Die einzelnen Protokollzeilen sind UTF-8 codiert und haben folgenden grundlegenden Aufbau:  
`Uhrzeit`  `ID`  `Daten`

#### 1.2.1) ID = `#`
`01:11:25 # MeshAll42 - V0.5.9 | v 1.0`  
`Uhrzeit` **#** `APP-Titel` - `APP-Version` \| `Proto-Version`

#### 1.2.2) ID = `$`
Jedes einzelne Pakete wird in 2-3 Zeilen dargestellt.  
1.Zeile: 
`01:12:04 $ 44 7B 22 54 ... 73 65 7D 00 00`
`Uhrzeit` **$** `Rohdaten Hex codiert`  

#### 1.2.3) Folgezeile ID = `-` = Datenpaket
`01:12:04 - D{"TYP":"I","FWVER":"4.34 s","CALL":"OE3WAS-12","ID":632488560, "HWID":3,"MAXV":4.125,"BLE":"short","BATP":100,"BATV":4.283311523, "GCB0":0,"GCB1":0,"GCB2":0,"GCB3":0,"GCB4":0,"GCB5":0,"CTRY":"EU8","BOOST":false}`  

#### 1.2.4) Folgezeile ID = `>` = Text-Message Paket
Text-Message Pakete werden in 3 Zeilen dargestellt:

| Rohdaten: | `01:22:19 $ 40 3A 61 ... D4 C8 38 00` |
|:---|:---|
| Messagetext: | `01:22:19 > Eintrag für mein Proto testen` |
| Parameter: | `01:22:19 . 15.03.2025 01:22:19 \|#8C59DA61 🔷 OE3WAS,OE3WAS-12 ➜ * 🔷  H:B4 HW:0 M:136 FCS:4914 FW:0 LH:131` |

#### 1.2.5) Folgezeile ID = `> @A` = ACK-Message-Paket
ACK-Pakete werden in 3 Zeilen dargestellt:

| Rohdaten: | `01:12:09 $ 40 41 9A 2C EC 05 00 00 67 D4 BF 50 00` |
|:---|:---|
| dekodiert: **@A** = ACK | `01:12:09 > @A  0000 67D4 BF50` |
| Parameter: | `01:12:09 . 15.03.2025 01:12:09 #05EC2C9A 🔷  ➜  🔷` |

#### 1.2.6) Folgezeile ID = `> {CET}` = TimeStamp-Message

| Rohdaten: | `01:18:12 $ 40 3A B1 ... 67 D4 C7 42 00` |
|:---|:---|
| Timestamp: | `01:18:12 > {CET}2025-03-15 00:18:10` |
| Parameter: | `01:18:12 . 15.03.2025 01:18:12 \|#67D399B1 🔷 OE1XAR-45,OE3WAS-12 ➜ * 🔷  H:B2 HW:0 M:136 FCS:CC0E FW:0 LH:131 #` |

___
***:copyright: 16.3.2025 by OE3WAS - Wolfgang***
