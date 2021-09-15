# Analyse der PDS100 Platine
Auf dieser Seite werden die Messergebnisse von dem verwendeten Modul für das Schnellladen aufgelistet.

Ein erster Ansatz für die Analysen und das Reverse Engineering war das Datenblatt vom zentralem IC SW3518S [[Datasheet](/datasheet/Datasheet_SW3518S.pdf)].

## Aufbau der Platine

### Elektrischer Schaltplan
Aus dem verlinkten Datenblatt konnte der empfohlende Schaltplan entnommen werden. Dieser stimmte so ziemlich mit den Komponenten auf der Platine überein.
Die große Spule, die laut Datenblatt 22µH haben sollte, hat jedoch nur 19µH, was den Ripple am USB Ausgang etwas erhöht.
- [ ] Screenshot mit Oszi vom Ripple machen

<div align="center"> <img src="/media/Schematic.PNG" width="100%"/></div>

### Platinenaufbau Oben
Auf der Oberseite sind vor allem große Bauteile montiert:
- Barrel Jack Buchse (Eingangsspannung)
- USB-C Buchse (Eingangsspannung)
- Aluminium Polymer Kondensator für die Eingangspannung (100µF; 35V)
- 7-Segment Display (3 Nummern)
- USB-A Buchse (Ausgangsspannung)
- Aluminium Polymer Kondensator für die Ausgangsspannung (220µF; 25V)
- nicht geschirmte Spule (19µH)

Beim Überprüfen der Komponenten ist mir aufgefallen, dass die Spulenkontakte nicht immer nah an der Platine befestigt waren. Daher habe ich vorsorglich jede Spule erneut angelötet, damit der Übergangswiderstand durch das Lotzinn so gering wie möglich ist.

Da die Spule nicht geschirmt ist, kann es bei der Verwendung ohne das Aluminiumgehäuse das EMV Verhalten verschlechtern.
Jedoch wurden bei Messungen mit einem Oszilloskop keine signifikanten Störungen gemessen.

Auf dem Fotos ist die Platine bereits für das eigene Gehäuse vorbereitet, so dass die Eingangsbuchsen bereits entfernt wurden.
<div align="center"> <img src="/media/PCB_Top_label.jpg" width="60%"/></div>


### Platinenaufbau Unten
Auf der Unterseite sind sehr viel mehr Komponenten montiert, die vorallem für das konvertieren der Spannungen und die Kommunikation mit dem Lade-Chip da sind.
- USB-C Buchse (Ausgangsspannung)
- 3 Status LEDs
- SW3518S IC + Peripherie ([Datasheet](/datasheets/Datasheet_SW3518S.pdf))
- Mosfets mit Wärmeleitkleber an einer kleinen Aluplatte montiert (für die synchrone Step-Down Regelung; [Datasheet](/datasheets/Datasheet_AON6236.pdf))
- 8Bit Mikrocontroller (liest über I²C den SW3518S Chip aus und steuert LEDS an; [Datasheet](/datasheets/Datasheet_N76E003AT20.pdf))
- linear Regler + Peripherie (Eingangsspannung zu 3,3V; [Datasheet](/datasheets/Datasheet_HM5318A.pdf))
- PowerDelivery Trigger + Peripherie (auf 20V gestellt, IP2721Max, [Datasheet](/datasheets/Datasheet_IP2721Max.pdf))
- Keramik Kondensator für die Eingangsspannung

Auf dem Fotos ist die Platine bereits für das eigene Gehäuse vorbereitet, so dass der Trigger IC entfernt wurde und die Kabel für die Eingangsspannung angelötet wurden.
<div align="center"> <img src="/media/PCB_Down_label.jpg" width="90%"/></div>


## Untersuchung der Eigenschaften
Das PDS100 Modul soll auf sein Verhalten und dessen Eigenschaften in verschiedenen Situationen untersucht werden. Vorallem der Wirkungsgrad und das Temperaturverhalten ist von Interesse.

### Versuchsaufbau
Das Modul kann mit einer Spannung von 6-35V betrieben werden. Wobei die Eingangsspannung ca. 1V mehr betragen muss als die max. genutzte Ausgangsspannung. Daher wurde sich für eine Spannung von 21V, 24V und 30V als Eingangsspannung entschieden.

Für die Ausgangsleistungen wurde sich für die Spannungen von 3,3V; 5V; 9V; 12V; 15V; 20V entschieden, die jeweils mit 1-5A belastet werden.

Beim Versuchsaufbau wird das PDS100 Modoul über zwei Stromkabel mit einem Labornetzteil versorgt. Das Labornetzteil kann bis zu 30V und 5A bereit stellen.
Das PDS100 Modul wird über ein USB-C Kabel mit der elektrischen Last verbunden. Das USB-C Kabel kann durch einen zusätzlichen integrierten Chip bis zu 5A genutzt werden.

Die CC1 (über welche die Signale für das Triggern der Spannung verläuft), Ground und VCC Leitung werden bei der elektronischen Last herausgeführt und mit einem externen Trigger Modul verbunden.

Somit kann über das Labornetzteil die Eingangsspannung eingestellt werden und der eingehende Strom gemessen werden. Über ein Multimeter wird die anliegende Spannung direkt am PDS100 gemessen.

Über die elektronische Last kann die ausgehende Stromstärke geregelt werden und die ausgehende Spannung (hinter dem USB-C Kabel) gemessen werden.

Das Trigger Modul stellt lediglich über die herausgeführte CC1 Leitung das Spannungslevel des PDS100 ein und wird über eine externe Stromversorgung  versorgt.

Hier der Versuchsaufbau im schematischen Aufbau:

![Aufbau_Messung](/media/Aufbau_Messung.png)


In einem ersten Versuch wurde der Strom direkt über ein Trigger Modul geleitet. Was zu minimalen Leistungsänderungen geführt hat.
![Aufbau_Messung](/media/Aufbau_Messung_old.png)<br>

#### Bilder vom Versuchsaufbau 
<div align="center">
	<img src="/media/IMG_20210117_041318.jpg" width="19%"/> 
	<img src="/media/IMG_20210117_065042.jpg" width="19%"/> 
	<img src="/media/IMG_20210117_065056.jpg" width="19%"/> 
	<img src="/media/IMG_20210117_041333.jpg" width="19%"/> 
	<img src="/media/IMG_20210117_065902.jpg" width="19%"/>
</div>

### Wirkungsgrad
Die Messergebnisse wurden in eine Tabelle eingetragen: [Link zur Tabelle](https://docs.google.com/spreadsheets/d/e/2PACX-1vQ-uOuzFzesg3JFXQvdbmoFWdgVVLropliUy922riJwF3p_uEHaYvuCekLJsn0rVFE3M9WAN4aL1quC/pubhtml) 

<div align="center"> <img src="https://docs.google.com/spreadsheets/d/e/2PACX-1vQ-uOuzFzesg3JFXQvdbmoFWdgVVLropliUy922riJwF3p_uEHaYvuCekLJsn0rVFE3M9WAN4aL1quC/pubchart?oid=1326213271&format=image" width="100%"/></div>
Die verschiedenen Ausgangsspannungen 

<div align="center"> <img src="https://docs.google.com/spreadsheets/d/e/2PACX-1vQ-uOuzFzesg3JFXQvdbmoFWdgVVLropliUy922riJwF3p_uEHaYvuCekLJsn0rVFE3M9WAN4aL1quC/pubchart?oid=1716160355&format=image" width="100%"/></div>

### Temperatur
- [ ] verschiedene Belastungen (Spannung und Strom) testen

- [ ] Die Heatpoints auflisten und die Ursache beschreiben

Strom/Spannung | Platine von unten | Platine von oben
-------------- | ----------------- | ---------------
IN: 29V / 3,5A (101W)<br> OUT: 19,5V / 4,9A (94,6W)<br><br> Wirkungsgrad:  94%| ![Bild von Unten](/media/ThermalCam_down1.JPG)|![Bild von Oben](/media/ThermalCam_top4.JPG)

- [ ] Überprüfen bei 24V Input:
* 5V / 3A
* 5V / 5A
* 9V / 3A
* 9V / 5A
* 12V / 3A
* 12V / 5A
* 15V / 3A
* 15V / 5A
* 20V / 1A
* 20V / 2A
* 20V / 3A
* 20V / 4A
* 20V / 5A

## Spannung

- [ ] Platine mit verschiedenen Spannungen / Strömen belasten und den Ripple messen