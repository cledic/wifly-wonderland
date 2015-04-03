# Aggiornamento alla versione 4.0 #

E' disponibile una nuova versione di firmware. Le novità sono molte. Quella più interessante è aggiornando al nuovo firmware, il wifly sarà in grado di scaricare e gestire un nuovo formato immagine chiamato **nomefile.imf**

Questo nuovo formato è un contenitore che oltre al file immagine del firmware potrà ospitare anche uno o più applicativi.

# Aggiornare alla nuova versione #

Per aggiornare alla nuova versione i passi sono due:

  * seguite la procedura di aggiornamento descritta nel wiki. In questa maniera, al riavvio, il wifly sarà aggiornato alla 4.0
  * una volta riavviato e collegato al vostro AP, assicuratevi che sia configurato l'FTP server o impostate nuovamente l'IP e username e password. Poi eseguite il comando:
```
ftp update wifly7-400.mif
```
  * il modulo wifly scaricherà la nuova immagine e automaticamente la spacchetterà riavviandosi una volta terminato il processo.