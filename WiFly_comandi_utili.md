# Alcuni comandi utili per gestire il WiFly #

  * Programmazione del time server NTP
```
<2.45>
<2.45> set time address 193.204.114.233
<2.45> set time enable 1
<2.45> time

<2.45> show time
Time=20:19:37
UpTime=15 s

<2.45> get time
TimeEna=1
TIMEADR=193.204.114.233:123
Zone=0
<2.45>
<2.45>
```

  * Alcuni comandi per verificare lo stato del collegamento. L'output è quello del mio WiFly programmato per collegarsi all'AP di casa.
```
<2.45> show net
SSid=dd-wrt_vap
Chan=11
Assoc=OK
Rate=12, 24Mb
Auth=OK
Mode=WPA2
DHCP=OK,renew=-1350317700
Boot=-1350332358675
Time=OK
Links=1
<2.45>

<2.45> show rssi
RSSI=(-53) dBm
<2.45>

<2.45> show stat
Conns=0, WRX=0/0, WTX=0/0, RTRY=0, RTRYfail=0
 URX=3, UTX=655, RXdrop=0, RXerr=0,
FlwSet=0, FlwClr=0
 TX-UDP=0, netbufs=0, evt=0, adhoc_lost=0
Boots=1, Wdogs=0,TXon=1
<2.45>

<2.45> get ip
IF=UP
DHCP=ON
IP=192.168.1.11:2000
NM=255.255.255.0
GW=192.168.1.1
HOST=0.0.0.0:2000
PROTO=TCP,
MTU=1524
FLAGS=0x7
TCPMODE=0x0
BACKUP=0.0.0.0
<2.45>

<2.45> get sys
SleepTmr=0
WakeTmr=0
Trigger=0x41
Autoconn=0
IoFunc=0x0
IoMask=0x21f0
IoValu=0x0
DebugReg=0x0
PrintLvl=0x1
<2.45>
```

  * Comandi per verificare la visibilità nella rete
```
<2.45> ping 8.8.8.8
Ping try (len=32) 8.8.8.8
<2.45> PING reply from 8.8.8.8

<2.45> ping 192.168.1.1
Ping try (len=32) 192.168.1.1
<2.45> PING reply from 192.168.1.1

<2.45> lookup www.google.com
www.google.com=173.194.35.178
```

  * Collegamento al server NTP INRIM (http://www.inrim.it/ntp/services_i.shtml) per leggere la data e l'ora
```
set ip proto 18
set ip host 193.204.114.233
set ip remote_port 13
open
*OPEN*15 OCT 2012 22:44:39 CEST
*CLOS*
```
  * A seguire della open il wifly invierà l'output dal server remoto preceduto da :
```
  *OPEN*
```
  * e chiuso da:
```
  *CLOS*
```
  * Ricordarsi che a questo punto il wifly è uscito dalla modalità comandi.

  * Lettura delle news dell'ANSA:
```
set ip proto 18
set dns name ansa.it
set ip host 0
set ip remote 80
set com remote GET$/web/notizie/rubriche/topnews/topnews_rss.xml
set option format 1
open
```

  * Lettura del meteo di Google **ATTENZIONE: io sono stato "bannato per le troppe richieste"**, quindi usatelo con parsimonia:
```
set ip proto 18
set dns name www.google.com
set ip host 0
set ip remote 80
set com remote GET$/ig/api?weather=Roma&hl=it
set option format 1
open
```

  * In ambedue i comandi _set com remote_ il carattere **$** è in sostituzione dello spazio.