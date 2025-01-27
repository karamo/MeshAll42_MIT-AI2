# BLE-Scan & Connect & DisConnect (DEBUG-Version)
Die DEBUG-Version ist für die grundsätzliche Entwicklung und das Testen der Funktionalität vorgesehen und
ist daher noch nicht auf schönes optisches Erscheinungsbild hin optimiert.

Der 1. Schritt zu einer BLE-Kommunikation ist das Scannen von BLE-Geräten in der Nähe.  
https://de.wikipedia.org/wiki/Bluetooth_Low_Energy  
*"Alle Bluetooth-LE-Geräte senden unabhängig voneinander kurze Advertising Events (Aufmerksamkeitshinweise)
auf einem der drei Advertising Channels (effektiv Anmeldekanäle). Anschließend lauscht das Gerät auf diesem Kanal
nach einer Verbindungsanfrage, worauf dann auf einen der verbliebenen 37 Kanäle gewechselt wird, um einen
größeren Datenblock vom Gerät zu erhalten."*  

## 1) UUID
Für die Kommunikation sind UUIDs erforderlich. Bei einem bekanntem BLE-Gerät ist eine einfache Möglichkeit,
die UUIDs als globale Variablen bereitzustellen und in der Folge zu verwenden. Im vorliegenden Fall handelt es sich
um das **Nordic UART Service** als **PRIMARY SERVICE** mit der **TX Characteristic** und **RX Characteristic**.

![blocks_0](https://github.com/user-attachments/assets/238ffce2-28a9-4cb2-8f8c-48a0bc33c1e8)

## 2) BLE-Scan
Hier beginnt auch die Verbindung zur Benutzeroberfläche, dem Erscheinungsbild der APP mit ihren Bedienelementen,
Anzeigen und Eingabefeldern u.a.
Es ist das Ziel eines guten MMI (Mensch-Maschine-Interface), die Bedienung so sicher wie möglich zu machen und
Bedienungsfehler größtmöglich auszuschließen. Das erfolgt dadurch, dass nur jene Elemente freigegeben werden,
die im jeweiligen Zustand auch sinnvoll und zulässig sind. Dies erfolgt auch durch Implementierung einer FSM
(Finiten State Machine), wobei je nach Zustand die einzelnen Elemente auf `enabled true|false` bzw. `visible true|false`
geschaltet werden. Diese Absicherung stellt einen erheblichen Teil der Logik dar.  
Die erforderlichen Verriegelung, dh. `enabled` und `visible` der einzelnen Elemente für die jeweiligen Zustände
übernimmt die Prozedur **setFSM**. 

Damit beginnt des Scan-Prozess und die **FSM** wird auf **"S"** gesetzt.  
![grafik](https://github.com/user-attachments/assets/41e80a3e-afb3-40a9-a1d8-1ce7e78dcb71)

Wenn nun ein BLE-Gerät gefunden wurde, wird dieses Gerät in die `DeviceList` eingetragen. **FSM := "SF"**  
![grafik](https://github.com/user-attachments/assets/efdbba3c-e587-425f-b33d-6b863f3938d8)

## 3) Select BLE-Device
Nachdem man im nächsten Schritt ein BLE-Gerät aus der `DeviceList` ausgewählt hat, werden die zu diesem Zeitpunkt
verfügbaren Infos ausgelesen und angezeigt: `DeviceAddress` (=MAC-Adresse), `DeviceName` und `DeviceRssi`.  
Zu diesem Zeitpunkt wird die Auswahl auf eine gültige **MeshCom-FW** getestet und **FSM := "CV"**.  
![grafik](https://github.com/user-attachments/assets/cb5edc16-c8f7-487a-9212-31efd415c7a3)

## 4) Connect
Nun kann der Versuch eines Verbindungsaufbaus (connect) unternommen werden.  
![grafik](https://github.com/user-attachments/assets/44bfafd8-753e-4fc6-8717-aa5f9d6d8852)

Dieser Verbindungsaufbau kann aber misslingen: **FSM := "CX"**  
Dann zurück für eine neue Auswahl.  
![grafik](https://github.com/user-attachments/assets/ef82e5bf-7d05-48b0-bcdb-2535adc3b47a)  

Oder der Verbindungsaufbau gelingt, dann wird sofort ein neues MTU = 250 ausgehandelt.
Und weitere Daten werden verfügbar. Unter anderem auch die `DeviceServices` und `DeviceCharacteristics`.
**FSM := "CC"**  
![grafik](https://github.com/user-attachments/assets/58e61693-817d-43f1-b665-e8f0a81a3fa9)

Die neu verhandelte `MTUvalue` wird angezeigt:  
![grafik](https://github.com/user-attachments/assets/f085f9eb-cc12-4780-9c12-964fd728e3ed)

## 5) DisConnect
Bei einem **DisConnect** wird ein neuer **Scan** oder **Connect** möglich. **FSM := "0"**  
![grafik](https://github.com/user-attachments/assets/26db232d-390a-454c-9377-76f3ad6ce38a)

___
***:copyright: 27.1.2025 by OE3WAS - Wolfgang***
