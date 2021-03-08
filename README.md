# Scheda di Illuminazione Digitale per vetture Roco Eurofima di Seconda Classe in Scala H0
Questa scheda e' pensata per illuminare in maniera digitale le vetture Roco Eurofima, di *seconda classe*, in scala H0.
E' stata progettata espressamente sugli ingombri stutturali della carrozza per massimizzare il realismo luminoso garantendo **tutte** le zone illuminate in maniera indipendente: Corridoio, *Luci Diurne Comapartimenti*, **Luci Notturne Blu Compartimenti**, *Bagni* e predisposizione per le luci di coda *rosse*.</br> 
<img src="https://github.com/TheFidax/ProgrammerUpdaterShield/blob/main/images/shield.jpg" width="1280">

------------

## Indice
* [Video Presentazione del Progetto](#video-presentazione-del-progetto)
* [Manuale Scheda](#manuale-scheda)
* [FirmWare](#firmware)
* [HardWare](#hardware)
* [Caratteristiche della Scheda](##caratteristiche-della-scheda)
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

## Manuale Scheda
Il manuale della scheda è [disponibile qui](https://github.com/TheFidax/TFX040_ROCO_EUROFIMA_2CLASSE_H0/blob/main/TFX040_MANUALE.odt).

------------

## FirmWare
Il Firmware dedicato e' presente sotto la cartella [FirmWare](https://github.com/TheFidax/TFX040_ROCO_EUROFIMA_2CLASSE_H0/tree/main/FirmWare), per poterlo caricare è consigliata la seguente [Shield](https://github.com/TheFidax/ProgrammerUpdaterShield).</br>
Le cifre finali del file .HEX identificano la versione del FirmWare.

------------

## HardWare

------------

## Caratteristiche della Scheda
Di seguito sono riportate le caratteristiche della scheda, poi spiegate in dettaglio nei vari paragrafi dedicati.
- [Schottky Diodes](https://github.com/TheFidax/TFX040_ROCO_EUROFIMA_2CLASSE_H0#ponte-di-diodi-schottky) to provide CC power from Tracks
- [MCP16331](https://github.com/TheFidax/TFX040_ROCO_EUROFIMA_2CLASSE_H0#chip-step-down-buck-mcp16331) to power Board at 5v
- [PowerPack](https://github.com/TheFidax/TFX040_ROCO_EUROFIMA_2CLASSE_H0#condensatori-powerpack) system by 4x 100uF Tantalum capacitors with slow charge system and [Overvoltage Isolation system](https://github.com/TheFidax/TFX040_ROCO_EUROFIMA_2CLASSE_H0#protezione-sovratensioni-opzionale).
- Board can be operate with these systems: CC Analog (from 7v), PWM CC Analog, AC Analog, Digital (DCC & Motorola)
- [AtMega128A](https://github.com/TheFidax/TFX040_ROCO_EUROFIMA_2CLASSE_H0#microchip-atmega128a) to Digital Operation
- Optoisolator to read [DCC signal]
- [ACK System]
- JST SH 6 connector to program AtMega with ISP system and to provide I2C Bus from external target
- All compartments illuminated independently (with Day and Night lights)
- Bathrooms illuminated independently
- Pads for tail red lights
- Space for 20mm round speaker (recommended 8Ω 2w)
- PluX22 Interfaces (with Sound and SUSI BUS)
- Optoisolator to detect presence of PluX Decoder and activate the SUSI bus
- MINIMUM CLEARANCE: 6mil

------------

### Ponte di Diodi Schottky

Il circuito di alimentazione e' realizzato meadiante 4 diodi Schottky in configurazione [Ponte di Graetz](https://it.wikipedia.org/wiki/Raddrizzatore#Ponte_di_Graetz).</br>
Tale configurazione permette di *raddrizzare* la tensione captata dalle prese di corrente in Conrente Continua a prescindere del sistema di alimentazione:
- Corrente Continua Analogica (fornisce sempre gli stessi poli in uscita)
- Corrente PWM (raddrizza l'onda quadra fornendo una tensione simil continua)
- Corrente Alternata Analogica (raddrizza l'onda sinusoidale fornendo una tensione simil continua)
- Digitale (raddrizza l'onda quadra fornendo una tensione simil continua)

------------

### Chip Step Down Buck MCP16331
L'alimentazione a 5 volt e' fornita dal chip [Microchip MCP16331](https://www.microchip.com/wwwproducts/en/MCP16331), un regolatore di tensione di tipo [Step Down Buck](https://it.wikipedia.org/wiki/Convertitore_buck) in gradi di ricevere in ingresso tensioni fino a 50 volt e di fornire in uscita una tensione stabile a 5 volt con sviluppo di calore minimo.</br>

------------

### Condensatori PowerPack
Per sopperire a problemi di captazione di corrente e' previsto un sistema *powerpack* formato da 4 condensatori al Tantalio da 100uF con tensione **massima** di 25 volt.</br>
I condensatori sono separati dal circuito di alimentazione da un Diodo ed un Resistore che rappresentano *il sistema di ricarica lenta*.
Come ulteriore protezione la scheda **può essere equipaggiata** con un sistema di [protezione dalle sovratensioni](https://github.com/TheFidax/TFX040_ROCO_EUROFIMA_2CLASSE_H0#protezione-sovratensioni-opzionale).

------------

### Protezione Sovratensioni (Opzionale)
Questa protezione **e' opzionale**: la sua mancanza **e' segnalata dal Jumper J1 *chiuso***.
Le normative [NMRA](https://www.nmra.org/sites/default/files/standards/sandrp/pdf/s-9.1_electrical_standards_2020.pdf) e [NEM](https://morop.org/downloads/nem/fr/nem670_f.pdf) **impongono** che un decoder digitali *supportino* tensioni fino a 27 volt.</br>
L'utilizzo di condensatori a 25 volt *non e' a norma*. **Tuttavia** le stesse normative impongono che la centrale fornisca tensione *massima* di 22 volt.</br>
Pertanto in condizioni di *funzionamento corretto* i condensatori non riceveranno tensioni che possano danneggiarli.

**In caso di impiego della Scheda su sistemi a Corrente Alternata Analogica questa protezione E' OBBLIGATORIA!** 

Il sistema di protezione si basa sul chip [LTC4367](https://www.analog.com/en/products/ltc4367.html) che **isola** mediante *MOSFET* i condensatori in caso di tensioni *superiori a 23,7 volt*; quando la tensione scende sotto questa soglia i condensatori torneranno alimentati.</br>

------------

### Microchip ATmega128A
Il *cervello* della scheda e' un microcontrollore [ATmega128](https://www.microchip.com/wwwproducts/en/ATmega128A) a 64 pin operante a 5 volt con frequenza di 16MHz.</br>
Il microcontrollore comanda *in maniera indipendente* tutti (leggere NOTA) i LED, in modo tale da garantire la massima flessibilita' di funzionamento.

*NOTA* Il corridoio e' progettato con *5 segmenti* da 3 led ognuno: il microcontrollore comanda il segmento e *non* il singolo LED.

------------

### Lettura DCC
Il segnale digitale e' letto mediante [Optoisolatore TLP2168](https://toshiba.semicon-storage.com/eu/semiconductor/product/optoelectronics/detail.TLP2168.html) che fornisce l'[isolamento galvanico](https://it.wikipedia.org/wiki/Isolamento_elettrico) del microcontrollore dalla tensione delle rotaie.</br> 
L'optoisolatore e' protetto dall'inversione di corrente mediante Diodo e da un eccessiva corrente mediante resistore.
Tale chip e' bicanale e permette, inoltre, il rilevamento della presenza di un Decoder Esterno analizzando la linea U+ fornita da esso.

------------

### Sistema ACK
La scheda e' dotata di sistema per fornire l'ACK nella programmazione DCC mediante binario di programmazione.

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
