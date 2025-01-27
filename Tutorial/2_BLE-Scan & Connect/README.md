# BLE-Scan & Connect (DEBUG-Version)
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
die UUIDs als globale Variablen bereitzustellen und in der Folge zu verwenden. Dabei handelt es sich um das
**Nordic UART Service** als **PRIMARY SERVICE** mit der **TX Characteristic** und **RX Characteristic**.

![blocks_0](https://github.com/user-attachments/assets/238ffce2-28a9-4cb2-8f8c-48a0bc33c1e8)

## 2) BLE-Scan
Hier beginnt auch die Verbindung zur Benutzeroberfläche, dem Erscheinungsbild der APP mit ihren Bedienelementen,
Anzeigen und Eingabefeldern u.a.
Es ist das Ziel eines guten MMI (Mensch-Maschine-Interface), die Bedienung so sicher wie möglich zu machen und
Bedienungsfehler größtmöglich auszuschließen. Das erfolgt dadurch, dass nur jene Elemente freigegeben werden,
die im jeweiligen Zustand auch sinnvoll und zulässig sind. Dies erfolgt auch durch Implementierung einer FSM
(Finiten State Machine), wobei je nach Zustand die einzelnen Elemente auf `enabled true|false` bzw. `visible true|false`
geschaltet werden. Diese Absicherung stellt einen erheblichen Teil der Logik dar.

![grafik](https://github.com/user-attachments/assets/41e80a3e-afb3-40a9-a1d8-1ce7e78dcb71)

Hier wird die **FSM** auf **{S}** gesetzt. Die für diesen Zustand, aber auch allen anderen Zuständen, erforderliche
Verriegelung, dh. `enabled` und `visible` der einzelnen Elemente übernimmt die Prozedur **setFSM**.

### Procedure (setFSM) bisher

![grafik](https://github.com/user-attachments/assets/f6d2bc04-d97d-4fe8-950c-97b2475b3cf4)

___
***:copyright: 27.1.2025 by OE3WAS - Wolfgang***
