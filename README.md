# PowerDelivery für den Hackerspace
![Table](/media/CAD_rendering_table.png)<div align="center">*Ein-/Ausschalter, 3x XT60 Buchsen, 6x USB-Ladestationen*</div>

Der Arbeitstisch sollte um eine zentrale Ladeeinrichtung für Smartphones, Laptops und andere Gerätschaften erweitert werden.<br>
Dafür bietet sich der mitterweile weit verbreitete "USB PowerDelivery" Ladestandart an, welcher Spannungen im Bereich **5V bis 20V mit bis zu 5A** (also max. 100W) zur Verfügung stellt.

Die Grundlage dieses Projektes ist ein fertiges Board, dass man unter dem Namen "PDS100" bei den üblichen asiatischen Kaufplattformen erwerben kann. 

## Das Lademodul "PDS100"

<img src="/media/PDS100_1.jpg" width="50%"/><img src="/media/PDS100_2.jpg" width="50%"/><br><div align="center">*Bilder sind vom Händler "TZT Official Store"*</div>

Das Board basiert auf dem Chip "SW3518S" vom Hersteller ISMARTWARE.<br>
Die genaue Analyse und überprüfung des Boards kann [hier](analyse.md) nachgelesen werden.

Das Lademodul muss mit einer Gleichspannung im Bereich 6V - 30V betrieben werden. Als Spannungseingang kann auf einen herkömlichen Hohlstecker vom Typ 5,5x2,5mm zurück gegriffen werden. Als alternativen Spannungseingang gibt es eine USB-C Buchse, welche über PowerDelivery 2.0 eine Spannung von 20V triggert.<br>
Da das Modul Spannungen nur herunterregeln kann, muss die Eingangspannung min. 1V über der maximalen genutzten Spannung sein.

Als Ausgang stehen eine USB-C und eine USB-A Buchse zur Verfügung. Zudem werden über die 3 stellige 7-Segment Anzeige verschiedene Informationen angezeigt:
* das getriggerte Charge Protokoll (siehe in der Charge Tabelle unter "Display")
* ausgehende Spannung an beiden Buchsen
* ausgehende Stromstärke für jeweils USB-A & USB-C

Um zwischen den 3 verfügbaren Werten (Spannung und Stromstärke der 2 Buchsen) zu unterscheiden gibt es 3 LEDs:

 Info | Linke LED | Mittlere LED | Recht LED
----- | ----- | ----- | ------
**Farbe**|Rot|Grün|Blau
**Funktion** | ausgehende Spannung<br>für USB-C & USB-A| Stromstärke für<br>USB-C | Stromstärke für<br>USB-A

Wenn beide Buchsen gleichzeitig genutzt werden, wird die ausgehende Spannung automatisch auf 5V festgesetzt und der maximale Strom auf 2,7A begrenzt.

Bei der Nutzung von nur einer Buchse, können die vorhanden Charge Protokolle getriggert werden. Die Ausgangsspannung der jeweils anderen Buchse wird aus Schutz deaktiviert.

## Unterstütze Charge Protokolle

Für die folgende Übersicht von unterstützten Charge Protokollen wurde das [Datenblatt vom SW3518](/datasheets/Datasheet_SW3518.pdf) und das Analysegerät vom Typ "Qway-U2p" genutzt.

- [ ] Foto vom Ergebniss vom Analysegerät 
  
Protokoll | Kurzform | Display | Hersteller | Spannungen & Strom
--------- | ---------| ------- | ---------- | ------------------
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
keins     |    -     | n0n     | -          | 5V 2A <br>(**ToDo:** testen!)
Apple Charge (*1)     | -     | n0n    | Apple      | 5V max. 2,4A
Samsung Charge (*2) | - | n0n | Samsung | 5V max. 2A
USB BC1.2 (*3) | DCP | n0n | offen | 5V max. 1,5A
Dash Charge | VOOC | ? | OPPO | 5V max. 4A

**(*1)** wird getriggert, wenn D+ & D- auf 2,7V gezogen werden<br>
**(*2)** wird getriggert, wenn D+ & D- auf 1,2V gezogen werden<br>
**(*3)** wird getriggert, wenn D+ & D- miteinander kurz geschlossen werden

Die meisten Charge Protokolle werden über die differentielle Leitung (D+ & D-) des USB-Kabels getriggert. Somit können alle (alten) USB-Kabel genutzt werden, welche diese 2 Leitungen besitzten.<br>
Der USB PowerDelivery Standart hat für seine Kommunikation eine extra CC (Control Channel) Datenleitung. Somit können USB Kabel welche einen klassischen USB Stecker haben (Typ-A, Typ-B, Mini, Micro) nicht für PowerDelivery genutzt werden.<br>
Da normale USB Kabel für max. 3A ausgelegt sind (diese müssen dann auch schon recht hochwertig sein), sind lediglich Leistungen von max. 60W  (3A bei 20V) möglich.<br>
PowerDelivery ist jedoch in der Lage höhere Stromstärken anzubieten. Dazu müssen spezielle USB-C Kabel henutzt werden, welche über einen eingebauten E-Marker Chip verfügen und mit dem Ladegerät kommunizieren können.

Das Analysegerät "Qway-U2p" bietet die Möglichkeit solche E-Marker Chips auszulesen.


## Integration in den Space

Da mehrere Personen gleichzeitig am Basteltisch arbeiten können, wurde sich für 6 Ladestationen entschieden, die gleichmäßig auf dem mittleren Brett montiert werden sollen. Das Kabelmanagment und die dazugehörige Stromversorgung soll unter dem Tisch montiert und verlegt werden.

### Neues Gehäuse
Damit die PDS100 Module sicher und auch optisch (einigermaßen) passend montiert werden können, wurde ein neues Gehäuse für den 3D Druck benötigt. Dabei sind folgende Kriterien zu erfüllen:
* Die Platine muss geschützt sein
* Module müssen fest montierbar sein
* Nutzbarkeit darf nicht eingeschränkt werden
* Abwärme muss entweichen können
* Stromkabel müssen verlegbar sein

Der erste Schritt war die nachmodelierung der vorhanden Platine: [hier zum 3D Modell](/3D_models/PowerDelivery_Board.stl)
Mithilfe dieser Polygon-Version der PDS100-Platine konnte das neue Gehäuse angefertig werden: [neues Gehäuse](/3D_models/case.stl) & [Deckel](/3D_models/case_cap.stl)<br>
<img src="/media/CAD_rendering2.png" width="50%"/><img src="/media/CAD_rendering.png" width="50%"/><br>
Das Gehäuse besteht aus einer Halterung, in welche die Platine einfach reingesteckt werden kann. Ein Deckel wird passend auf den vorderen Teil der Platine raufgesteckt und schließt bündig mit der vorhanden Halterung ab. Die Öffnungen an der Ober- und Unterseite dienen der Kühlung.
<br>![animatedView](/media/CAD_rendering.gif)<br>

Zum Befestigen sind zwei Einsparungen für Muttern der Größe M4 vorgesehen. Über die Öffnung an Unterseite können die Stromkabel verlegt werden.<br>
![rendered Picture for mounting](/media/CAD_rendering_mounting.png)

#### Materialwahl
Da der Abstand zwischen Gehäuse und Spule (welche bei max. Belastung ca. 100°C erreichen kann) nur sehr wenige Milimeter beträgt, kann nicht jedes Material verwendet werden.

Material | Glastemperatur 
--- | ---
PLA | 60°C
PETG | 88°C
ABS | 104°C
annealed PLA | 150°C
Polycarbonat | 148°C

Somit würden für unsere 3D Drucker nur ABS und annealed PLA infrage kommen. Da ABS ohne Hitzekammer nur schwer zu drucken ist und wir noch keine Erfahrung über das Härten von Kunststoffen haben, haben wir die Halterungen in Polycarbonat drucken lassen.

### Montage & Verkabelung


- [ ] DXF Files hochladen
- [ ] Sicherungskasten fotografieren
- [ ] Verkabelung Fotografieren
- [ ] Schaltaufbau grob als Funktionsblock abbilden

### Spannungsversorgung
- [ ] verschiedene Möglichkeiten auflisten (Servernetzteile, MeanWell Netzteil)






