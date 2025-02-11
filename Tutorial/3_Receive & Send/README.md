# Receive & Send (Strings)

Eine mögliche grundlegende Kommunikation könnte einfach über Strings erfolgen.  
Das hat sich aber im konkreten Fall der **MeshCom-FW** in Teilen als unmöglich herausgestellt,
da das Message-Format eine Kombination von ASCII-Zeichen, Bytes und UTF-8 String ist.  
Daher wurde der automatische Empfang auf `RegisterForBytes` umgestellt. Dadurch ist es nun möglich,
die einzelnen Elemente eines Message-Paketes einzeln zu decodieren.

Die Datenpakete sind in JSON formatiert und es muss nur aus den einzelnen Bytes ein JSON-String
erstellt werden, der dann weiter verarbeitet werden kann.

Das Senden von Messages und Commands erfolgt als ein Byte-Paket (String).

___
***:copyright: 11.2.2025 by OE3WAS - Wolfgang***
