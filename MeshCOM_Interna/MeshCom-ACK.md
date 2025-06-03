# MeshCom ACK System Dokumentation

## Überblick

Das MeshCom ACK (Acknowledgment) System verwendet spezielle Nachrichten zur Bestätigung des Empfangs. ACK-Nachrichten haben eine feste Struktur und verwenden verschiedene Statuswerte.

## ACK Nachrichtenformat

Eine ACK-Nachricht hat folgende Struktur:

```
[0x41] [MSG_ID - 4 Bytes] [FLAGS] [ACK_MSG_ID - 4 Bytes] [ACK_TYPE] [0x00]
```

### Byte-Aufschlüsselung:

1. **Byte 0: Message Type (0x41)**
   - Kennzeichnet die Nachricht als ACK-Nachricht

2. **Bytes 1-4: MSG_ID**
   - 32-Bit Message ID der ACK-Nachricht selbst
   - Byte 1: LSB (Least Significant Byte)
   - Byte 2: 
   - Byte 3: 
   - Byte 4: MSB (Most Significant Byte)
   - Format: Little-Endian

3. **Byte 5: FLAGS**
   - Bit 7 (0x80): Server Flag
     - 1 = Nachricht kommt vom/geht zum Server
     - 0 = Normale Peer-to-Peer Nachricht
   - Bits 0-6 (0x7F): Max Hop Count
     - Anzahl der verbleibenden Hops für Mesh-Weiterleitung
     - Wird bei jeder Weiterleitung dekrementiert

4. **Bytes 6-9: ACK_MSG_ID**
   - 32-Bit Message ID der Original-Nachricht, die bestätigt wird
   - Byte 6: LSB
   - Byte 7:
   - Byte 8:
   - Byte 9: MSB
   - Format: Little-Endian

5. **Byte 10: ACK_TYPE**
   - 0x00: Node ACK (Bestätigung von einem normalen Knoten)
   - 0x01: Gateway ACK (Bestätigung von einem Gateway)

6. **Byte 11: Terminator (0x00)**
   - Markiert das Ende der ACK-Nachricht

## ACK Status-Codes

Im Code werden folgende Status-Werte für die Nachrichtenverfolgung verwendet:

```cpp
own_msg_id[index][4] = status
```

- **0x00**: Nachricht noch nicht gehört
- **0x01**: Nachricht wurde gehört (HEARD)
- **0x02**: ACK wurde empfangen

## Message ID Struktur

Die Message ID ist ein 32-Bit Wert, der wie folgt aufgebaut sein kann:

### Standard Message ID
- Basiert auf `millis()` (Millisekunden seit Start)
- Eindeutig pro Knoten während einer Session

### Gateway Message ID Format
```cpp
msg_counter = ((_GW_ID & 0x3FFFFF) << 10) | (iAckId & 0x3FF);
```
- Bits 31-10: Gateway ID (22 Bits)
- Bits 9-0: ACK ID (10 Bits)

## ACK Verarbeitungslogik

### 1. Empfang einer normalen Nachricht
- System prüft, ob es eine eigene Message ID ist
- Falls ja und Status = 0x00, wird Status auf 0x01 gesetzt (HEARD)
- Eine HEARD-Benachrichtigung wird an das Phone/BLE gesendet

### 2. Empfang einer ACK-Nachricht
- System prüft die ACK_MSG_ID gegen eigene gesendete Nachrichten
- Falls gefunden und Status < 0x02, wird:
  - Status auf 0x02 gesetzt (ACK empfangen)
  - ACK an Phone/BLE weitergeleitet

### 3. Gateway ACK-Generierung
Gateways senden automatisch ACKs für:
- Nachrichten an "*" (Broadcast)
- Nachrichten an "WLNK-1"
- Nachrichten an "APRS2SOTA"
- Gruppen-Nachrichten

### 4. ACK-Weiterleitung im Mesh
- ACKs werden nur weitergeleitet, wenn:
  - Max Hop Count > 0
  - Mesh-Funktion aktiviert ist
  - Es sich um eine neue Message ID handelt
  - Die Nachricht nicht bereits vom Server kommt

## Spezielle ACK-Fälle

### Direct Message ACK
Bei Direktnachrichten mit "{" am Ende:
```
:Nachrichtentext{123
```
Die Zahl nach "{" ist die ACK-ID, die in der Antwort referenziert wird.

### ACK/REJ Nachrichten
Format im Payload:
- `:ack123` - Positive Bestätigung für Nachricht 123
- `:rej123` - Ablehnung für Nachricht 123

## Beispiel einer ACK-Sequenz

1. **Original-Nachricht gesendet:**
   ```
   MSG_ID: 0x12345678
   ```

2. **HEARD-Status (wenn Nachricht im Netz gehört):**
   ```
   [0x41] [0x78,0x56,0x34,0x12] [0x00] [0x00,0x00]
   Status → 0x01
   ```

3. **ACK empfangen:**
   ```
   [0x41] [neue_msg_id] [0x83] [0x78,0x56,0x34,0x12] [0x01] [0x00]
   Status → 0x02
   ```

## Implementierungshinweise

- ACKs werden nicht für Telemetrie-Nachrichten (Ziel: "100001") generiert
- Broadcast-Nachrichten mit speziellen Präfixen ({MCP}, {SET}, {CET}) erzeugen keine Gateway-ACKs
- Die Retransmission-Logik nutzt den ACK-Status zur Entscheidung über Wiederholungen
- ACK-Nachrichten selbst werden mit Status 0xFF markiert (keine Wiederholung)
