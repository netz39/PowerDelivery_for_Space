# PowerDelivery für den Hackerspace
Der Arbeitstisch sollte um eine zentrale Ladeeinrichtung für Smartphones, Laptops und andere Gerätschaften erweitert werden.<br>
Dafür bietet sich der mitterweile weit verbreitete "USB PowerDelivery" Ladestandart an, welcher Spannungen im Bereich **5V bis 20V mit bis zu 5A** (also max. 100W) zur Verfügung stellt.

Die Grundlage dieses Projektes ist ein fertig Board, dass man unter dem Namen "PDS100" bei den üblichen asiatischen Kaufplattformen erwerben kann. Das Board basiert auf dem Chip SW3518S vom Hersteller ISMARTWARE.<br>
Die genaue Analyse und überprüfung des Boards kann [hier](analyse.md) nachgelesen werden.

- [ ] Bilder vom Tisch mit Lademodulen machen

## Das Lademodul "PDS100"

- [ ] Bilder von dem Modul mit Gehäuse
- [ ] Ein paar Fakten zu dem Modul schreiben (z.B. Spannungsversorgung, StepDown Regler)
- [ ] minimale Spannung testen

Das Lademodul muss mit einer Gleichspannung im Bereich xV - 30V betrieben werden. Als Spannungseingang kann auf einen herkömlichen Hohlstecker vom Typ 5,5x2,5mm zurück gegriffen werden. Desweiteren gibt es eine USB-C Buchse, welche über USB PowerDelivery 2 versucht 20V zu triggern.

Da der PDS100 Spannungen nur herunterregeln kann, muss die Eingangspannung min. 1V über der maximalen genutzten Spannung sein.


## Unterstütze Charge Protokolle

Für die folgende Übersicht von unterstützten Charge Protokollen wurde das [Datenblatt vom SW3518](/datasheets/Datasheet_SW3518.pdf) und das Analysegerät vom Typ "Qway-U2p" genutzt.

- [ ] Foto vom Ergebniss vom Analysegerät 
  
Protokoll | Kurzform | Display | Hersteller | Spannungen & Strom
--------- | ---------| ------- | ---------- | ------------------
keins     |    -     | n0n     | -          | 5V 2A (**ToDo:** testen!)
Quick Charge 2.0 | QC2 | C2.0  | Qualcomm   | 5V, 9V, 12V, 15V, 20V<br>max. 3A
Quick Charge 3.0 | QC3 | C3.0  | Qualcomm   | 3,7V - 20V (0,2V Steps)<br>max. 3A
PowerDelivery 2.0<br>aka Quick Charge 4| PD2 | PD2  | offen      | 5V, 9V, 12V, 15V, 20V<br>max. 5A
PowerDelivery 3.0<br>aka PPS oder Quick Charge 4+ | PD3 | PD3  | offen      | 3,3V - 20V (0,2V Steps)<br>max. 5A
Adaptive Fast Charge | AFS | AFS  | Samsung   | 5V, 9V, 12V<br>max. 3A
Fast Charge Protocol | FCP | FCP  | Huawei   | 5V, 9V, 12V<br>max. 2A
Super Charge Protocol | SCP | SCP  | Huawei   | 3,4V - 5,5V<br>max. 5A
Super Fast Charge Protocol | SFCP | ?  | Huawei   | 5V, 9V, 12V
Pump Express 1.1 | PE1.1 | PE1  | Mediatek   | 5V, 7V, 9V, 12V
Pump Express 2.0 | PE2.0 | PE2  | Mediatek   | 5V - 20V (0,5V Steps)
Apple Charge (*1)     | -     | ?    | Apple      | 5V max. 2,4A
Samsung Charge (*2) | - | ? | Samsung | 5V max. 2A
USB BC1.2 (*3) | DCP | ? | offen | 5V max. 1,5A
Dash Charge | VOOC | ? | OPPO | 5V max. 4A

**(*1)** wird getriggert, wenn D+ & D- auf 2,7V gezogen werden<br>
**(*2)** wird getriggert, wenn D+ & D- auf 1,2V gezogen werden<br>
**(*3)** wird getriggert, wenn D+ & D- miteinander kurz geschlossen werden

Die meisten Charge Protokolle werden über die differentielle Leitung (D+ & D-) des USB-Kabels getriggert. Somit können alle (alten) USB-Kabel genutzt werden, welche diese 2 Leitungen besitzten.<br>
Der USB PowerDelivery Standart hat für seine Kommunikation eine extra CC (Control Channel) Datenleitung. Somit können USB Kabel welche einen klassischen USB Stecker haben (Typ-A, Typ-B, Mini, Micro) nicht für PowerDelivery genutzt werden.
Da normale USB Kabel für max. 3A ausgelegt sind (diese müssen dann auch schon recht hochwertig sein), sind lediglich Leistungen von max. 60W  (3A bei 20V) möglich.<br>
Da PowerDelivery jedoch auch höhere Stromstärken anbietet, müssen spezielle USB-C Kabel henutzt werden, welche über einen eingebauten E-Marker Chip verfügen, welche mit dem Ladegerät kommunizieren können.

Das Analysegerät "Qway-U2p" bietet die Möglichkeit solche E-Marker Chips auszulesen.


## Integration in den Space

### Neues Gehäuse

- [ ] Modell von Platine
- [ ] Auswahl des Materials vom Gehäuse (Temperatur)

<img src="/media/CAD_rendering2.png" width="50%"/><img src="/media/CAD_rendering.png" width="50%"/>
![animatedView](/media/CAD_rendering.gif)

### Montage
![rendered Picture for mounting](/media/CAD_rendering_mounting.png)

- [ ] DXF Files hochladen

### Spannungsversorgung
- [ ] verschiedene Möglichkeiten auflisten (Servernetzteile, MeanWell Netzteil)

### Verkabelung

- [ ] Sicherungskasten fotografieren
- [ ] Verkabelung Fotografieren
- [ ] Schaltaufbau grob als Funktionsblock abbilden




