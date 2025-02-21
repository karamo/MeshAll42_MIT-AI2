# Receive & Send (Strings)

Eine Kommunikation mit dem BLE-Gerät kann über verschiedene Datentype. könnte einfach über Strings erfolgen.  
Das hat sich aber im konkreten Fall der **MeshCom-FW** in Teilen als unmöglich herausgestellt,
da das **Message-Format** eine Kombination von ASCII-Zeichen, Bytes und UTF-8 String ist.  
Daher wurde der automatische Empfang auf `RegisterForBytes` umgestellt.  
Dies war aber mit den verfügbaren Methoden des AI2 nicht möglich. Erst mit einer für diesen Fall erweiterte Version 1.6
[AI2 Byte-Array Extension](https://ullisroboterseite.de/android-AI2-ByteArray.html) wurde dies möglich. Dank an Ulrich!  
Dadurch ist es nun möglich, die einzelnen Elemente eines Message-Paketes einzeln zu decodieren.

Die **Datenpakete** sind in JSON formatiert und es muss nur aus den einzeln empfangenen Bytes ein JSON-String
rekonstruiert werden, der dann weiter verarbeitet werden kann.

Das Senden von Messages und Commands erfolgt als ein Byte-Paket (String).

___
***:copyright: 21.2.2025 by OE3WAS - Wolfgang***
