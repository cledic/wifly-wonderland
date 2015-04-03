# Configurazione del WiFly come AP con il nuovo firmware #


  * All'avvio il nostro WiFly ripete di continuo questo errore:
```
Auto-Assoc roving1 chan=4 mode=NONE FAILED
Auto-Assoc roving1 chan=4 mode=NONE FAILED
```

  * ed è difficile  far interpretare il comando $$$
O ci mettiamo con pazienza ad inviarlo di continuo, o possiamo fare così:

  1. accendere il WiFly tenendo al positivo 3.3V PIO9 (pin 8)
  1. collegarsi al SSID “WiFly”
  1. fare Telnet IP 169.254.1.1:2000 A questo punto il WiFly rispondera' HELLO
  1. inviare $$$ SENZA "Invio" ed aspettare la stringa CMD in risposta
  1. Eseguire i comandi:

```
set wlan phrase YOUR_PASS_PHRASE
set wlan ssid YOUR_SSID
set wlan join 1
save
reboot
```

  * Il sito da cui scaricare il nuovo firmware è il seguente: rn.microchip.com. Nel comando useremo l'IP diretto
Il sito FTP Microchip ha numeroso files al suo interno. Questi dovrebbero esserci utili:
```
-r-xr-xr-x   1 owner    group           79659 Sep 27 22:01 wifly-EZX.img
-r-xr-xr-x   1 owner    group           83623 Oct  9 14:22 wifly-EZX-AP.img
-r-xr-xr-x   1 owner    group           79719 Sep 27 22:00 wifly-GSX.img
-r-xr-xr-x   1 owner    group           83695 Oct  9 14:54 wifly-GSX-AP.img
```

  * A seguire i comandi per prepararci ad aggiornare il firmware:
```
set ftp address 198.175.253.161
set ftp dir ./public
set ftp user roving
set ftp pass Pass123
save 
reboot 
```

  * Al riavvio eseguiremo il comando di aggiornamento specificando il file da scaricare:
```
<2.32> ftp update wifly-EZX-AP.img
<2.32> FTP connecting to 198.175.253.161
FTP file=54
...........................................................
FTP OK.
UPDATE OK

<2.32> ls

FL# SIZ FLAGS
  2  20   3 WiFly_EZX-2.31
 22  11   3 wps_app
 33   1  10 config
 34  20   3 WiFly_EZX-2.32
 54  21   3 WiFly_EZX-2.45

181 Free, Boot=54, Backup=34
<2.32> factory RESET
Set Factory Defaults
<2.32>
<2.32> ls

FL# SIZ FLAGS
  2  20   3 WiFly_EZX-2.31
 22  11   3 wps_app
 33   1  10 config
 34  20   3 WiFly_EZX-2.32
 54  21   3 WiFly_EZX-2.45

181 Free, Boot=54, Backup=34
<2.32> reboot
```


  * A questo punto possiamo mettere in piedi una nostra configurazione. Con questo nuovo firmware esiste una configurazione AP di defualt che viene impostata automaticamente se all'avvio poniamo a +3.3V il pin GPIO9. Per i dettagli vedere la Tab.15 del .PDF
> (http://ww1.microchip.com/downloads/en/DeviceDoc/rn-wiflycr-um-1.0r.pdf)


  * I comandi per configurare il wifly come AP sono i seguenti:
```
set wlan join 7
set wlan channel 9
set wlan ssid wifly_tst
set ip dhcp 4 
set ip address 192.168.2.1
set ip net 255.255.255.0
set ip gateway 192.168.2.1
save
reboot
```

  * La scelta del canale è importante se si hanno molti AP nelle vicinanze. Di norma i canali da utilizzare sono: 1, 6, 11. Ovviamente sono quelli più popolati perché sono a default negli apparati installati dai ISP. Nel palazzo dove abito ad esempio "vedo" ben 18 AP e solo due hanno canali "non standard". Tutti gli altri sono distribuiti su questi tre canali.

  * Al riavvio ho associato prima il tablet Android e poi il cellulare al nuovo AP _wifly\_tst_. Come da manuale: hanno acquisito un IP dal DHCP del wifly, nel network da me programmato, e si vedevano tra di loro. Il limite di IP disponibili è sette.

```
DHCP: 192.168.2.10 lease to android-90d5573b
CMD

<2.45> show lease
192.168.2.10,00:9d:13:0e:f9:3c,9,android-90d5573b
192.168.2.11,00:00:00:00:00:00,0,
192.168.2.12,00:00:00:00:00:00,0,
192.168.2.13,00:00:00:00:00:00,0,
192.168.2.14,00:00:00:00:00:00,0,
192.168.2.15,00:00:00:00:00:00,0,
192.168.2.16,00:00:00:00:00:00,0,
<2.45> show z
0.0.0.0
<2.45> show associated
1,00:9d:13:0e:f9:3c,10698,0,0
<2.45> DHCP: 192.168.2.10 lease to android-90d5573b
DHCP: 192.168.2.11 lease to *

<2.45> show asso
1,00:9d:13:0e:f9:3c,25480,0,1
2,38:ec:e4:8e:42:2a,2993,0,1
<2.45> show lease
192.168.2.10,00:9d:13:0e:f9:3c,4,android-90d5573b
192.168.2.11,38:ec:e4:8e:42:2a,0,*
192.168.2.12,00:00:00:00:00:00,0,
192.168.2.13,00:00:00:00:00:00,0,
192.168.2.14,00:00:00:00:00:00,0,
192.168.2.15,00:00:00:00:00:00,0,
192.168.2.16,00:00:00:00:00:00,0,
```

  * I comandi **show lease** e **show associated** permettono di verificare gli utenti collegati all'AP ed il loro traffico.

  * Nel manuale PDF si fa riferimento all'utilizzo di tre pin: **GPIO4, 5 & 6** che possono venir usati come link monitor (pag.46, Table 16)