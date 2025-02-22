# Android APP - Releases

## 1) Versionen

### 1.1) MeshAll42_V0_5_3b.apk
Download unter [Releases -> Tags ...](https://github.com/karamo/MeshAll42_MIT-AI2/tags)  
Die erste hier verfügbare Pre-Version beherrscht folgende Grundfunktionen:

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
Die Funktionalität der APP wird laufend erweitert.

## 20) wichtige Hinweise zur Installation  (Android)
* Grundsätzlich ist **Google Play Protect** eingeschaltet. Der Durchlauf dauert einige Zeit.
* Das **Google Play Protect** zickt herum und sagt mir dauernd, dass die Internetverbindung schlecht wäre. Daher musste ich es es ausschalten und dann ging die Installation durch.
* Am Smartphone unter **Downloads** gibt es eine Protokoll-Datei **`MeshAll42.txt`**.
* das mit dem `Display on/off` ist in der **FW 4.34o 02.15** noch ein **Bug**. siehe [#2](https://github.com/karamo/MeshAll42_MIT-AI2/issues/6)
* Installiert und getestet unter **Android 8** und **Android 13** und **Android 15**

## 21) und Bedienung (V 0.5.3 -> 0.5.4)
* Die 1. Buttonreihe schaltet die die Sichtbarkeit der einzelnen Bereiche:
 **SCAN&CONNECT | INFO | CHAT | CONFIG | SETUP & DEBUG** um.
* **INFO** lässt sich nur einschalten, wenn auch **SCAN&CONNECT** aktiv ist.  
 ![ButtonsBereiche](https://github.com/user-attachments/assets/0b72f1c2-540e-48b8-8a52-6cc86db2d5ae)  
* im Bereich **CHAT** sind unter dem Button **[commands]** mehrere Befehle verfügbar.
* **[CLR]** löscht die Chat-Einträge (Liste unterhalb), **[CL]** löscht das Eingabefeld.  
 ![CHATcommands](https://github.com/user-attachments/assets/831c4a95-f4d3-4e03-aaef-78158347c546)
* im Bereich **CONFIG** gibt es ein DropDown **select...v**  in dem sich jene Befehle befinden, die einen zusätzlichen Parameter erfordern, der in das nebenstehende Textfeld einzugeben ist.
* mit dem Button **[set]** wird der Befehl mit dem Parameter abgesendet.  
  ![CommandsParameter](https://github.com/user-attachments/assets/90c898f1-52be-435a-a20f-41ca8e16cd09)
* das Filtern der Msg-Pakete ist vorbereitet, aber noch nicht implementiert. Daher werden alle Pakete im Chat angezeigt.  
 ![chatElemente](https://github.com/user-attachments/assets/6d76f70e-b34b-4faf-b2f6-695da1e3d675)

___
***:copyright: 22.2.2025 by OE3WAS - Wolfgang***
