## Scheda di Illuminazione Digitale per vetture Roco Eurofima di Seconda Classe in Scala H0
Questa scheda e' pensata per illuminare in maniera digitale le vetture Roco Eurofima, di *seconda classe*, in scala H0.
E' stata progettata espressamente sugli ingombri stutturali della carrozza per massimizzare il realismo luminoso garantendo **tutte** le zone illuminate in maniera indipendente: Corridoio, *Luci Diurne Comapartimenti*, **Luci Notturne Blu Compartimenti**, *Bagni* e predisposizione per le luci di coda *rosse*.</br> 
<img src="https://github.com/TheFidax/ProgrammerUpdaterShield/blob/main/images/shield.jpg" width="1280">

------------

## Indice
* [Upload FirmWare](#Upload-FirmWare)
* [Caricare FirmWare su un Dispositivo](#Caricare-FirmWare-su-un-Dispositivo)
* [Modalita' Di Funzionamento](#Modalita-Di-Funzionamento)
  - [Modalita' ISP](#Modalita-ISP)
  - [Modalita' I2C](#Modalita-I2C)
* [Caratteristiche della Shield](#Caratteristiche-della-SHield) 
  - [Porta AVR ISP](#Porta-AVR-ISP)
  - [Porta JST](#Porta-JST)
  - [Selettore Reset](#Selettore-Reset)
  - [ISP LED](#ISP-LED)
  - [LED Modalita'](#LED-Modalita)
  - [I2C Resistori PullUp](#I2C-Resistori-PullUp)
* [File Gerber](#File-Gerber)
* [HardWare](#HardWare)

------------


## Video Presentazione del Progetto
[![Video Presentazione](https://img.youtube.com/vi/wB8cmPJ338o/0.jpg)](http://www.youtube.com/watch?v=wB8cmPJ338o)

------------

## Upload FirmWare
Il Firmware dedicato e' presente sotto la cartella [FirmWare](https://github.com/TheFidax/TFX040_ROCO_EUROFIMA_2CLASSE_H0/tree/main/FirmWare), per poterlo caricare è consigliata la seguente [Shield](https://github.com/TheFidax/ProgrammerUpdaterShield).</br>
Le cifre finali del file .HEX identificano la versione del FirmWare.

------------

## Caricare FirmWare su un Dispositivo
Per caricare un FirmWare/Skecth in formato .HEX, dopo aver collegato la Shield al dispositivo mediante AVR ISP oppure JST ISP, su un dispositivo sono necessari i seguenti passaggi (sono **molto** simili a quelli per caricare il Firmware della Shield, ma **non identici**):</br>
- **Programmer (-c)** : *Arduino*
- **Port (-P)** : la porta COM a cui e' connessa la scheda Arduino
- **Baud rate (-b)** : **19200**
- Premere **Detect** : Nella *console* verra' restituito il modello del Micro che *si intende programmare*
- **Flash** : il file .hex che *si vuole caricare*
- Infine premere **Programm**

------------

## Modalita' Di Funzionamento
La shield presenta *due modalita'* di funzionamento: **ISP** e **I2C**.</br>
Le due modalita' sono *selezionabili* tramite l'interruttore dei resistori di PullUp: se i resistori sono attivi (LED acceso) e' attiva la modalita' **I2C**, se i led e' spento e' attiva la modalita' *ISP*.</br>
*Per passare da una modalita' all'altra*, dopo aver mosso l'interruttore, **e' necessario** eseguire un *Reset* della scheda Arduino mediante apposito pulsante.

#### *Modalita' ISP*:</br>
La modalita' ISP e' basta sul software [ArduinoAsISP](https://www.arduino.cc/en/Tutorial/BuiltInExamples/ArduinoISP) e permette di utilizzare la scheda Arduino come programmatore ISP per target esterni, utile per scrivere bootloader o per caricare Sketch senza l'ausilio del Bootloader.</br>

#### *Modalita' I2C*:</br>
In sviluppo.

------------

## Caratteristiche della Shield
#### **Porta AVR ISP**</br>

<img src="https://github.com/TheFidax/ProgrammerUpdaterShield/blob/main/images/avr_isp.jpg" width="1280">
La porta AVR ISP permette alla Shield di interfacciarsi con i target esterni e rispecchia lo schema standard degli AVR:</br>
<img src="https://www.waveshare.com/img/devkit/general/10-pin_ISP_Connector_standard.jpg" width="400"></br>

**N.B.** Il pin *VCC* e' collegato alla linea **5 volt**.

------------

#### **Porta JST**

<img src="https://github.com/TheFidax/ProgrammerUpdaterShield/blob/main/images/jst_isp.jpg" width="1280">

E' presente una porta JST SH6 che fornisce, al posto dei 5 volt, una linea *non regolata* collegata al pin **VIN** di Arduino.</br> 
Questa porta svolge la doppia funzione di **Porta ISP** e **Porta I2C**.</br>

<img src="https://github.com/TheFidax/ProgrammerUpdaterShield/blob/main/images/jst_scheme.jpg" width="1280"></br>

Tale porta fornisce il Bus I2C mediante il seguente schema:</br>
<img src="https://github.com/TheFidax/ProgrammerUpdaterShield/blob/main/images/jst_i2c.jpg" width="600">

------------

#### **Selettore Reset**</br>

<img src="https://github.com/TheFidax/ProgrammerUpdaterShield/blob/main/images/reset_target.jpg" width="1280"></br>

Tramite questo ponticello e' possibile reindirizzare la linea di Reset delle **Porte ISP** al micro della Scheda Arduino; **e' utile** per poter utilizzare un *programmatore ISP* dotato di porta AVR a 10 pin per scrivere il BootLoader sulla scheda Arduino.</br>

------------

#### **ISP LED**</br>

<img src="https://github.com/TheFidax/ProgrammerUpdaterShield/blob/main/images/isp_led.jpg" width="1280"></br>

LED di stato della programmazione ISP, per maggiori informazioni leggere la seguente [pagina](https://www.arduino.cc/en/Tutorial/BuiltInExamples/ArduinoISP#load-the-sketch)</br>

------------

#### **LED Modalita'**</br>

<img src="https://github.com/TheFidax/ProgrammerUpdaterShield/blob/main/images/mode_led.jpg" width="1280"></br>

Questi led forniscono un riscontro visivo sulla Modalita' (I2C o ISP) attualmente in esecuzione nel Firmware.

------------

#### **I2C Resistori PullUp**

<img src="https://github.com/TheFidax/ProgrammerUpdaterShield/blob/main/images/i2c_pullup.jpg" width="1280"></br>

La shield monta due resistori di *pullup* da **2kΩ** per il bus I2C Wire a 400kHz. </br>
Tali resistori sono abilitabili tramite un interruttore, il riscontro visivo sull'effettiva abilitazione e' fornito da un Led che risultera' acceso quando i resistori sono attivi.</br>
Quando i resistori sono attivi, il firmware entrera' in modalita' I2C; in caso di *spostamento interruttore* con scheda Arduino alimentata **e' necessario** eseguire un reset della scheda per rendere edffettivo il passaggio da una modalita' all'altra.</br>
**ATTENZIONE**: *Nella versione HardWare 1.00* le scritte 'ON' e 'OFF' dell'interruttore sono **invertite**! Il reale stato dei resistori e' fornito dal LED.

------------

## File Gerber
Nella cartella [Hardware](https://github.com/TheFidax/ProgrammerUpdaterShield/tree/main/HardWare) sono presenti i file, in formato .zip, Gerber per la produzione in proprio della Shield.

------------

## HardWare
Maggori informazioni sull'HardWare della Shield sono reperibili dentro la cartella [HardWare](https://github.com/TheFidax/ProgrammerUpdaterShield/tree/main/HardWare) e nel file [HARDWARE README](https://github.com/TheFidax/ProgrammerUpdaterShield/blob/main/HardWare/Hardware.md).
