# Android APP - Releases
=> [Installation & Bedienung](https://github.com/karamo/MeshAll42_MIT-AI2/blob/main/Versionen/README.md#2-wichtige-hinweise-zur-installation-android) 

## 1) Versionen
Hier sind die Versionen/Releases in umgekehrter Reihenfolge aufgelistet, dh. die neueste Version steht als erster Punkt hier.

### 1.3) MeshAll42_V0_6_0.apk - preview
* +Sprachausgabe der Nachrichten (experimentell)
* +Protokoll-Datei (LogFile) mit Rohdaten (Bytes) und dekodiert
* +Setup-Parameter in der APP speichern
___
### 1.2) MeshAll42_V0_5_5.apk
Einige Ergänzungen und Issues behoben.  
Download [Releases -> Tags ...](https://github.com/karamo/MeshAll42_MIT-AI2/releases/tag/v0.5.5)  

* Schalten von einigen Funktionen ist bereits realisiert. Sensoren fehlen noch. Dafür muss ich erst die kleinen Boards finden, anbauen und in der APP auswerten, was in **v0.5.6** kommen wird.
* **GPS** sollte schon funktionieren, habe ich aber auch noch nicht am Board. Falls man es einschaltet und es wird nicht gefunden, dann schaltet es sich richtigerweise von selber wieder aus.
___
### 1.1) MeshAll42_V0_5_4.apk
Gegenüber V0.5.3 Verbesserte und erweiterte Version beherrscht u.a. folgende Grundfunktionen:

<ins>Ablauf:</ins>  
* **[SCAN]** Scannen von BLE-Geräten
* **[CONNECT]** verbinden mit einem **MeshCom-Node**
  * **[Reg]** registrieren für den Empfang von Daten (automatisch)
  * **{HELLO}** Start der Kommunikation (automatisch)
  * empfangen der Grundeinstellungen und teilweises Darstellen derselben (automatisch)
* **[disCON]** Verbindung trennen - **!!! nicht vergessen !!!**

<ins>weitere Möglichkeiten:</ins>
* **[commands]** senden von verschiedenen Commands, zB. `--info` `--display off` `--display on` u.a.
* **[<=Send]** senden einer Msg aus einem Eingabefeld
* senden von Command mit Parameter(n) zB. **`--setCALL OE3XXX-12`** u.a.

Empfangene Msg und andere Datenpakete werden decodiert und dargestellt.
___
## 2) wichtige Hinweise zur Installation (Android)
* APPs, die mit dem AI2 erstellt wurden, sollten ab **Android V5+** lauffähig sein. Installiert und getestet wurde es unter **Android 8** und **Android 13** und **Android 15**
* Grundsätzlich ist **Google Play Protect** eingeschaltet. Der Durchlauf dauert einige Zeit.
* Das **Google Play Protect** zickt herum und sagt mir dauernd, dass die Internetverbindung schlecht wäre. Daher musste ich es es ausschalten und dann ging die Installation durch.

## 2.1) und Bedienung (V 0.5.5)
* Die 1. Buttonreihe schaltet die Sichtbarkeit der einzelnen Bereiche um:  
 **[BLE] [INFO] [CHAT] [CONFIG] [SETUP&DEBUG]**  
![ButtonsBereiche](https://github.com/user-attachments/assets/061460c8-9b4d-4019-ae09-b67d06d1a605)  
* im Bereich **CHAT** sind unter dem Button **[commands]** mehrere Befehle verfügbar.
* **[CLR]** löscht die Chat-Einträge (Liste unterhalb), **[CL]** löscht das Eingabefeld, der **[Flieger]** sendet die Message.  
 ![v0-5-4_MsgInput](https://github.com/user-attachments/assets/e22cdd25-911e-4dfd-8832-37150151a506)
* im Bereich **CONFIG** gibt es ein DropDown **select...v**  in dem sich jene Befehle befinden, die einen zusätzlichen Parameter erfordern, der in das nebenstehende Textfeld einzugeben ist.
* mit dem Button **[set]** wird der Befehl mit dem Parameter abgesendet. Derzeit wird generell der Notifier "Wait for REBOOT..." ausgelöst, was aber bei einigen Befehlen nicht erforderlich wäre. Wird in einer Folgeversion geklärt.  
  ![CommandsParameter](https://github.com/user-attachments/assets/90c898f1-52be-435a-a20f-41ca8e16cd09)
* das Filtern der Msg-Pakete ist vorbereitet, aber noch nicht implementiert. Daher werden alle Pakete im Chat angezeigt.  
 ![chatElemente](https://github.com/user-attachments/assets/6d76f70e-b34b-4faf-b2f6-695da1e3d675)
___
***:copyright: 12.3.2025 by OE3WAS - Wolfgang***
