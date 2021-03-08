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

## FirmWare
Il Firmware dedicato e' presente sotto la cartella [FirmWare](https://github.com/TheFidax/TFX040_ROCO_EUROFIMA_2CLASSE_H0/tree/main/FirmWare), per poterlo caricare è consigliata la seguente [Shield](https://github.com/TheFidax/ProgrammerUpdaterShield).</br>
Le cifre finali del file .HEX identificano la versione del FirmWare.

------------

## HardWare

------------

## Caratteristiche della Scheda Luci
Di seguito sono riportate le caratteristiche della scheda, poi spiegate in dettaglio nei vari paragrafi dedicati.
- [Schottky Diodes](https://github.com/TheFidax/TFX040_ROCO_EUROFIMA_2CLASSE_H0#ponte-di-diodi-schottky) to provide CC power from Tracks
- MCP16331 to power Board at 5v
- PowerPack system by 4x 100uF Tantalum capacitors with slow charge system and Overvoltage Isoltion system.
- Board can be operate with these systems: CC Analog (from 7v), PWM CC Analog, AC Analog, Digital (DCC & Motorola)
- AtMega128A to Digital Operation
- Optoisolator to read DCC signal
- ACK System
- JST SH 6 connector to program AtMega with ISP system and to provide I2C Bus from external target
- All compartments illuminated independently (with Day and Night lights)
- Bathrooms illuminated independently
- Pads for tail red lights
- Space for 20mm round speaker (recommended 8Ω 2w)
- PluX22 Interfaces (with Sound and SUSI BUS)
- Optoisolator to detect presence of PluX Decoder and activate the SUSI bus
- MINIMUM CLEARANCE: 6mil

------------

#### Ponte di Diodi Schottky

Il circuito di alimentazione e' realizzato meadiante 4 diodi Schottky in configurazione [Ponte di Graetz](https://it.wikipedia.org/wiki/Raddrizzatore#Ponte_di_Graetz).</br>
Tale configurazione permette di *raddrizzare* la tensione captata dalle prese di corrente in Conrrente Continua a prescindere del sistema di alimentazione:
- Corrente Continua Analogica (fornisce sempre gli stessi poli in uscita)
- Corrente PWM (raddrizza l'onda quadra fornendo una tensione simil continua)
- Corrente Alternata Analogica (raddrizza l'onda sinusoidale fornendo una tensione simil continua)
- Digitale (raddrizza l'onda quadra fornendo una tensione simil continua)

------------

#### Chip Step Down Buck MCP16331

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
