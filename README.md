# MeshAll42_MIT-AI2
**BLE-Komunikation mit IoT-Devices - gebaut mit dem MIT-APP-Inventor 2 (MIT-AI2)**

## Meine Vision/Motivation
* einfache APP-Erstellung (bevorzugt für Android)
* Verständnis der BLE-Kommunikation
* Dokumentation des Aufbaus einer BLE Kommunikation wie ich es bislang noch nicht lesen konnte
* APP für die Kommunikation mit meinen Sensoren auf Basis ESP32 u.ä. (IoT-Devices)
* Diese meine Sensoren sollen zB. unter **MicroPython** laufen

## Vorgeschichte
Viele übliche Entwicklungsumgebungen für APPs (Android/iOS) bedürfen eines nicht unerheblichen Aufwands.  
Für einfache Anwendungen war mir diese Aufwand zu groß und ich suchte nach einfacheren Möglichkeiten.  
Da fand ich den [**MIT-APP-Inventor 2 (AI2)**](https://appinventor.mit.edu/),
der meiner Art von Softwareentwicklung sehr entsprach, da ich schon Jahrzehnte lang Anwendungen mit Delphi entwickle.  


## Realisierung
Ohne irgendwelche Vorkenntnisse bez. BLE konnte ich mir innerhalb von ein paar Tagen den grundsätzlichen Ablauf
von **BLE-Scan** (suchen von BLE-Geräten) und **BLE-Connect** (verbinden mit einem BLE-Gerät) erarbeiten;
ebenso das empfangen und senden von Strings oder Bytes oder anderer Datentypen. Hierfür gab es zwar schon viele
mehr oder weniger gute Beispielprogramme, die aber alle nicht meinen Bedürfnissen entsprachen und eigentlich nur Fragmente waren.  
Um nicht auf 2 Baustellen gleichzeitig entwickeln und Fehler suchen zu müssen, habe ich mich an Stelle des Sensors
für eine **MeshCom-Node** entschieden.  
Dabei gab es einige Hürden zu überwinden.  
* Zu aller erst war es erforderlich, die **Entwicklungsumgebung** des **MIT-AI2** kennen zu lernen.
* Dann die Eigenheiten von BLE.
* Und wegen der nicht vorhandenen Dokumentation der speziellen BLE-Kommunikation der
[**MeshCom-FW**  ](https://github.com/icssw-org/MeshCom-Firmware  ) mit der **MeshCom-APP**.  
Hier waren das Studium der Sourcen der FW und der APP, und auch viele Tests & Tricks erforderlich,
um zu einem zufriedenstellenden Ergebnis zu kommen.  

In weiterer Folge waren noch sehr spezielle Probleme zu lösen.  
Somit entstand, sozusagen als Nebenprodukt, eine **MeshCom** kompatible APP mit den grundlegenden Funktionen.  

___
***:copyright: 3.3.2025 by OE3WAS - Wolfgang***
