# MeshAll42_MIT-AI2
[**MeshCom-FW**  ](https://github.com/icssw-org/MeshCom-Firmware  ) kompatible APP für Android. Zuletzt gestestet mit der **FW 4.34u**.

## 1) Download & Installation (Android)
* Download [Releases -> Tags ...](https://github.com/karamo/MeshAll42_MIT-AI2/releases/tag/v0.5.10)
* APPs, die mit dem AI2 erstellt wurden, sollten ab **Android V5+** lauffähig sein. Installiert und getestet wurde unter **Android 8** und **Android 13** und **Android 15**
* Grundsätzlich ist **Google Play Protect** eingeschaltet. Der Durchlauf dauert einige Zeit.
* Das **Google Play Protect** zickt herum und sagt mir dauernd, dass die Internetverbindung schlecht wäre. Daher musste ich es es ausschalten und dann ging die Installation durch.

## 2) Bedienung (V 0.5.10) [in Arbeit]
* Die 1. Buttonreihe schaltet die Sichtbarkeit der einzelnen Bereiche um:  
 **[BLE] [INFO] [CHAT] [CONFIG] [SETUP&DEBUG]**  
![ButtonsBereiche](https://github.com/user-attachments/assets/061460c8-9b4d-4019-ae09-b67d06d1a605)  
___
* im Bereich **CHAT** sind unter dem Button **[commands]** mehrere Befehle verfügbar.
* **[CLR]** löscht die Chat-Einträge (Liste unterhalb), **[CL]** löscht das Eingabefeld, der **[Flieger]** sendet die Message.  
 ![v0-5-4_MsgInput](https://github.com/user-attachments/assets/e22cdd25-911e-4dfd-8832-37150151a506)
___
* im Bereich **CONFIG** gibt es ein DropDown **select...v**  in dem sich jene Befehle befinden, die einen zusätzlichen Parameter erfordern, der in das nebenstehende Textfeld einzugeben ist.
* mit dem Button **[set]** wird der Befehl mit dem Parameter abgesendet. Derzeit wird generell der Notifier "Wait for REBOOT..." ausgelöst, was aber bei einigen Befehlen nicht erforderlich wäre. Wird in einer Folgeversion geklärt.  
  ![CommandsParameter](https://github.com/user-attachments/assets/90c898f1-52be-435a-a20f-41ca8e16cd09)
___
* das Filtern der Msg-Pakete ist vorbereitet, aber noch nicht implementiert. Daher werden alle Pakete im Chat angezeigt.  
 ![chatElemente](https://github.com/user-attachments/assets/6d76f70e-b34b-4faf-b2f6-695da1e3d675)

___
## 80) Protokoll-Datei (Log-File) [ab V0.5.10]
### 80.1) Dateiname
zB.: **`MeshAll42_2025_03_15_01_11_25.txt`**  
`APP-Titel`\_`Erstellungsdatum`\_`Uhrzeit`**.txt**  
* Titel: MeshAll42
* Datum: 15.3.2025
* Uhrzeit: 1:11:25

### 80.2) Inhalt
Die einzelnen Protokollzeilen sind UTF-8 codiert und haben folgenden grundlegenden Aufbau:  
`Uhrzeit`  `ID`  `Daten`

#### 80.2.1) ID = `#`
`01:11:25 # MeshAll42 - V0.5.9 | v 1.0`  
`Uhrzeit` **#** `APP-Titel` - `APP-Version` \| `Proto-Version`

#### 80.2.2) ID = `$`
Jedes einzelne Pakete wird in 2-3 Zeilen dargestellt.  
1.Zeile: 
`01:12:04 $ 44 7B 22 54 ... 73 65 7D 00 00`
`Uhrzeit` **$** `Rohdaten Hex codiert`  

#### 80.2.3) Folgezeile ID = `-` = Datenpaket
`01:12:04 - D{"TYP":"I","FWVER":"4.34 s","CALL":"OE3WAS-12","ID":632488560, "HWID":3,"MAXV":4.125,"BLE":"short","BATP":100,"BATV":4.283311523, "GCB0":0,"GCB1":0,"GCB2":0,"GCB3":0,"GCB4":0,"GCB5":0,"CTRY":"EU8","BOOST":false}`  

#### 80.2.4) Folgezeile ID = `>` = Text-Message Paket
Text-Message Pakete werden in 3 Zeilen dargestellt:

| Rohdaten: | `01:22:19 $ 40 3A 61 ... D4 C8 38 00` |
|:---|:---|
| Messagetext: | `01:22:19 > Eintrag für mein Proto testen` |
| Parameter: | `01:22:19 . 15.03.2025 01:22:19 \|#8C59DA61 🔷 OE3WAS,OE3WAS-12 ➜ * 🔷  H:B4 HW:0 M:136 FCS:4914 FW:0 LH:131` |

#### 80.2.5) Folgezeile ID = `> @A` = ACK-Message-Paket
ACK-Pakete werden in 3 Zeilen dargestellt:

| Rohdaten: | `01:12:09 $ 40 41 9A 2C EC 05 00 00 67 D4 BF 50 00` |
|:---|:---|
| dekodiert: **@A** = ACK | `01:12:09 > @A  0000 67D4 BF50` |
| Parameter: | `01:12:09 . 15.03.2025 01:12:09 #05EC2C9A 🔷  ➜  🔷` |

#### 80.2.6) Folgezeile ID = `> {CET}` = TimeStamp-Message

| Rohdaten: | `01:18:12 $ 40 3A B1 ... 67 D4 C7 42 00` |
|:---|:---|
| Timestamp: | `01:18:12 > {CET}2025-03-15 00:18:10` |
| Parameter: | `01:18:12 . 15.03.2025 01:18:12 \|#67D399B1 🔷 OE1XAR-45,OE3WAS-12 ➜ * 🔷  H:B2 HW:0 M:136 FCS:CC0E FW:0 LH:131 #` |

___
***:copyright: 17.3.2025 by OE3WAS - Wolfgang***
