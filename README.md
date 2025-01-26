# MeshAll42_MIT-AI2
BLE-Komunikation mit Geräten - Erzeugt mit dem MIT-APP-Inventor 2

## Meine Vision
• einfache APP-Erstellung  
• Verständnis der BLE-Kommunikation  
• Dokumentation des Aufbaus einer BLE Kommunikation wie ich es bislang noch nicht lesen konnte  
• APP für die Kommunikation mit meinen Sensoren auf Basis ESP32 u.ä.  
• Diese meine Sensoren sollen unter **MicroPython** laufen

## Vorgeschichte
Viele übliche Entwicklungsumgebungen für APPs (Android/IOs) bedürfen einen nicht unerheblichen Aufwand.  
Für einfache Anwendungen war mir diese Aufwand zu groß und ich suchte nach einfacheren Möglichkeiten.  
Da fand ich dann den **MIT-APP-Inventor 2 (AI2)**, der meiner Art von Softwareentwicklung sehr entsprach, 
da ich schon Jahrzehnte lang Anwendungen mit Delphi entwickle.  

## Realisierung
Ohne irgendwelche Vorkenntnisse bez. BLE konnte ich mir innerhalb innerhalb von ein paar Tagen den Ablauf
des **BLE-Scan** (suchen von BLE-Geräten) und **Connect** (verbinden mit einem BLE-Gerät) erarbeiten;
ebenso das empfangen und senden von Strings.  
Hierfür gab es zwar schon viele mehr oder weniger gute Beispielprogramme, die aber alle nicht meinen
Bedürfnissen entsprachen und eigentlich nur Fragmente waren.  
Um nicht auf 2 Baustellen gleichzeitig entwickeln und Fehler suchen zu müssen, habe ich mich an Stelle des Sensors für eine **MeshCom-Node** entschieden.
Dabei gab es einige Hürden zu überwinden. Einerseits die Eigenheiten von BLE und andererseits die fehlende
Dokumentation über die BLE-Kommunikation der **MeshCom FW** mit der **MeshCom-APP**.  
[TODO] Link zu **MeshCom**  
Das Studium der Sourcen der FW und viele Tests & Tricks waren erforderlich.  
...

Ein erster kleiner Vorgeschmack, woraus die **APP V0.8** derzeit besteht:  
Bestehende rudimentäre Funktionen:  
• BLE-Scan  
• Connect  
• Start der Verbindung mit "Hello"  
• Empfangen der Parameter-Einstellungen  
• Empfangen von Msg
• Senden von Msg  
![grafik](https://github.com/user-attachments/assets/34e9df30-c42c-4cae-92f2-f0ba4e84f871)
