# MeshCom-Commands erklärt

Einige komplexere MeshCom-Befehle werden hier für ihre Anwendung erklärt.

## • MCP23017 - digital IO Erweiterung
https://github.com/karamo/MeshAll42_MIT-AI2/blob/main/MeshCOM_Interna/README.md#213-digital-io-mcp23017

## • WiFiTXpower

**Quellen:**  
* https://docs.espressif.com/projects/esp-idf/en/v5.4.1/esp32/api-reference/network/esp_wifi.html#_CPPv425esp_wifi_set_max_tx_power6int8_t
* https://docs.espressif.com/projects/esp-idf/en/stable/esp32s3/api-reference/network/esp_wifi.html#_CPPv425esp_wifi_set_max_tx_power6int8_t

In Übereinstimmung mit diesen Quellen gelten folgende Infos für **ESP32** & **ESP32-S3** gleichermaßen.

Der Aufruf der Funktion **--WiFiTXpower {2..20}** (Angabe der gewünschten Sendeleistung in [dBm]) bewirkt `esp_wifi_set_max_tx_power(int8_t power);`  
und setzt die Sendeleistung von WiFi, wobei **power = dBm * 4** bzw. **TXpower[dBm] = power * 0,25 dBm** gilt.

Das Mapping zwischen dem Wert von **power** und der Sendeleistung in **dBm** ist wie folgt definiert:  
![Image](https://github.com/user-attachments/assets/4d01db29-f526-4887-9685-a99afb86d944)

In **command_functions.cpp**
* Eingabe der Leistung in **dBm** im Bereich **{2..20}** ist anschaulicher.
* `--WiFiTXpower dBm` hat nichts mit dem Befehl `--TXpower dBm` zu tun, welcher für **LoRa** gilt und wo die Grenzen mit **TX_POWER_MIN, TX_POWER_MAX** für die jeweiligen Module fix festgelegt sind.  
* Änderung von **WiFiTXpower** erfordert ein **REBOOT**.



___
***:copyright: 22.11.2025 by OE3WAS - Wolfgang***
