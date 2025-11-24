# MeshCom-Commands FW 4.xx
Hier werden die jeweils verfügbaren Befehle/Commands aufgelistet von [**MeshCom-FW**  ](https://github.com/icssw-org/MeshCom-Firmware  ).

* Alle Befehle werden mit **`"--"`** eingeleitet und sind via Terminal und BLE absetzbar.
* Einzelne Befehle sind mit **`"*"`** gekennzeichnet. Diese sind hier https://github.com/karamo/MeshAll42_MIT-AI2/blob/main/MeshCOM_Interna/MeshCom-Commands_info.md genauer beschrieben.
* Manche einfachen Befehle sind hier in der vollen Syntax (Mengenschreibweise) bereits ausgeführt.
* Mengenschreibweise: **"{ }"** kennzeichnet eine Menge, **"|"** kennzeichnet alternative Elemente (oder), **".."** kennzeichnet von/bis, ein **","** Trennung von Elementen der Menge.
* Bei Befehlen, die ein **`" "`** (Leerzeichen) vor dem **"** haben, sind weitere Parameter erforderlich. Dies ist aber nicht bei allen solchen Befehlen konsequent durchgeführt.
* Bei einigen Befehlen gibt es den Parameter **"none"** mit dem ein String/Wert gelöscht werden kann.
* **Disclamer**: manche Befehle sind u.U. nicht für normale Verwendung verfügbar u/o unterliegen bestimmter Einschränkungen!

## FW 4.35c.07.20

```
"utcoff"
"settime"
"maxv"
"posshot"
"postime "
"volt"
"proz"
--setinfo {off | on}
--setcont {off | on}
--shortpath {off | on}
"reboot"
"spectrum"
"ota-update"
"help"
"info"
"all"
"msg"
--t5 {on | off}
--display {on | off}
--button {on | off | gpio}
"analog gpio "
"analog factor "
"analog alpha "
"analog slope "
"analog offset "
"analog atten "
"analog filter on"
"analog filter off"
"analog check on"
"analog check off"
"batt factor "
--board led {on | off}
--track {on | off}
--gps {on | off | reset}
"bleshort"
"blelong"
"save"
--bmp {on | off}
--bme {on | off}
--680 {on | off}
--811 {on | off}
--390 {on | off}
--aht20 {on | off}
--nomsgall {on | off}
"bmx off"
--lps33 {on | off}
--onewire {on | off | gpio}
"setpress"
--gateway {on | off | pos | nopos | srv}
--webserver {on | off}
"webpwd "
"webtimer 0"
"setname "
--mesh {on | off}
--extudp {on | off}
"extudpip"
--debug {on | off}
--loradebug {on | off}
--setboostedgain {on | off}
--bledebug {on | off}
--wxdebug {on | off}
--gpsdebug {on | off}
--softserdebug {on | off}
--softserread {on | off}
"softser on"
"softser off"
"softser send"
"softser app"
"softser app0"
"softser test0"
"softser test"
"softser baud "
"softser rxpin "
"softser txpin "
"softser fixpegel "
"softser fixpegel2 "
"softser fixtemp "
"softser xml"
"passwd "
"btcode "
--pos
"tempoff in "
"tempoff out "
--weather
--wx
--sendhey
--sendpos
--sendtele
--sendtrack
"symid"
"symcd"
"atxt "
"setcall "
"setudpcall "
"setssid "
"setpwd "
--wifiap {on | off}
"setownip "
"setowngw "
"setownms "
"sethamnet"
"setinet"
"setlat "
"setlon "
"setalt "
"setrtc "
* --io
* --setio clear
* --setout {A0..A7,B0..B7} {high | low}
* --setio  {A0..A7,B0..B7} {in | out}
"setctry "
* --wifitxpower {2..20}
"txpower "
"txfreq "
"txbw "
"txsf "
"txcr "
"specstart "
"specend "
"specstep "
"specsamples "
"lora"
--mheard
--mh
"path"
"hey"
--showi2c
"setgrc"
* --seset
* --wifiset
* --nodeset
* --analogset
* --aprsset
"conffin"
"parm "
"unit "
"format "
"eqns "
"values "
"ptime "
* --tel
```

ungeordnet weitere in nachfolgenden Versionen:  
`--shunt {0.001 .. 0.5}` Shunt-Widerstand am INA226, kann auch zur Kalibrierung verwendet werden.
___
***Stand: 24.11.2025 by OE3WAS - Wolfgang***
