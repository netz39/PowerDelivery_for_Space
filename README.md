# PowerDelivery für den Hackerspace
![Beispiel](/media/gallery/20210102_160408.jpg)<div align="center">*einsatzbereite Ladestation*</div>

Der Arbeitstisch sollte um eine zentrale Ladeeinrichtung für Laptops, Smartphones und andere elektrische Geräte erweitert werden.<br>
Dafür bietet sich der mitterweile weit verbreitete "USB PowerDelivery" Ladestandart an, welcher Spannungen im Bereich **3,3V bis 20V mit bis zu 5A** (also max. 100W) zur Verfügung stellt.

Die Grundlage dieses Projektes ist ein fertiges Board, dass man unter dem Namen "PDS100" bei den üblichen asiatischen Kaufplattformen erwerben kann. 

## Das Lademodul "PDS100"

<img src="/media/PDS100_1.jpg" width="50%"/><img src="/media/PDS100_2.jpg" width="50%"/><br><div align="center">*Bilder sind von einem Aliexpress Händler *</div>

Das Board basiert auf dem Chip "SW3518S" vom Hersteller ISMARTWARE.<br>
Leider gibt es nur sehr wenig Informationen und Daten über das Lademodul. Daher wurden viele Daten durch eigene Test und Analysen zusammengetragen.
Die genaue Analyse und überprüfung des Boards kann hier nachgelesen werden:

[**Analyse des PDS100 Boards**](analyse.md)

Das Lademodul muss mit einer Gleichspannung im Bereich 6V - 35V betrieben werden. Als Spannungseingang kann auf einen herkömmlichen Hohlstecker vom Typ 5,5x2,5mm zurück gegriffen werden. Als alternativen Spannungseingang gibt es eine USB-C Buchse, welche über PowerDelivery 2.0 eine Spannung von 20V triggert.<br>
Da das Modul Spannungen nur herunterregeln kann, muss die Eingangspannung min. 1V über der maximalen genutzten Spannung sein.

Als Ausgang stehen eine USB-C und eine USB-A Buchse zur Verfügung. Zudem werden über die 3 stellige 7-Segment Anzeige verschiedene Informationen angezeigt:
* das getriggerte Charge Protokoll (siehe in der Charge Tabelle unter "Display")
* ausgehende Spannung an beiden Buchsen
* ausgehende Stromstärke für jeweils USB-A & USB-C

Um zwischen den 3 verfügbaren Werten (Spannung und Stromstärke der 2 Buchsen) zu unterscheiden gibt es 3 LEDs:

 Info | Linke LED | Mittlere LED | Rechte LED
----- | ----- | ----- | ------
**Farbe**|Rot|Grün|Blau
**Funktion** | ausgehende Spannung<br>für USB-C & USB-A| Stromstärke für<br>USB-C | Stromstärke für<br>USB-A

Wenn beide Buchsen gleichzeitig genutzt werden, wird die ausgehende Spannung automatisch auf 5V festgesetzt und der maximale Strom auf 2,7A begrenzt.

Bei der Nutzung von nur einer Buchse, können die vorhanden Charge Protokolle getriggert werden. Die Ausgangsspannung der jeweils anderen Buchse wird aus Schutz deaktiviert.

## Unterstütze Charge Protokolle

Für die folgende Übersicht von unterstützten Charge Protokollen wurde das [Datenblatt vom SW3518S](/datasheets/Datasheet_SW3518.pdf) und das Analysegerät vom Typ "Qway-U2p" genutzt.

![Qway-U2p Analyse](/media/IMG_20210117_105745.jpg)<div align="center">*detektierte Ladeprotokolle über die vorhandene USB-C Schnittstelle*</div><br>
  
Protokoll | USB Anschluss | Display | Hersteller | Spannungen & Strom
--------- | ---------| ------- | ---------- | ------------------
Quick Charge 2 | A & C | C2.0  | Qualcomm   | 5V, 9V, 12V, 20V<br>max. 3A
Quick Charge 3 | A & C | C3.0  | Qualcomm   | 3,7V - 20V (0,2V Steps)<br>max. 3A
PowerDelivery 2<br>aka Quick Charge 4| C | PD2  | offen      | 5V, 9V, 12V, 15V, 20V<br>max. 5A
PowerDelivery 3<br>aka PPS oder Quick Charge 4+ | C | PD3  | offen      | 3,3V - 20V (0,2V Steps)<br>max. 5A
Adaptive Fast Charge | A & C | AFS  | Samsung   | 5V, 9V, 12V<br>max. 3A
Fast Charge Protocol | A & C | FCP  | Huawei   | 5V, 9V, 12V<br>max. 2A
Super Charge Protocol | A & C | SCP  | Huawei   | 3,4V - 5,5V<br>max. 5A
Super Fast Charge Protocol | A & C | ?  | Huawei   | 5V, 9V, 12V
Pump Express 1.1 | A & C | PE1  | Mediatek   | 5V, 7V, 9V, 12V
Pump Express 2.0 | A & C | PE2  | Mediatek   | 5V - 20V (0,5V Steps)
Apple Charge (*1)     | A & C     | n0n    | Apple      | 5V max. 3A
Samsung Charge (*2) | A & C | n0n | Samsung | 5V max. 2A
USB BC1.2 (*3) | A & C | n0n | offen | 5V max. 1,5A
Dash Charge (*4)| ? | n0n | OPPO | 5V max. 4A

**(*1)** wird getriggert, wenn D+ & D- auf 2,7V gezogen werden<br>
**(*2)** wird getriggert, wenn D+ & D- auf 1,2V gezogen werden<br>
**(*3)** wird getriggert, wenn D+ & D- miteinander kurz geschlossen werden<br>
**(*4)** ist laut Datenblatt verfügbar, aber anscheinend im verbauten Chip nicht aktiviert

Die meisten Charge Protokolle werden über die differentielle Leitung (D+ & D-) des USB-Kabels getriggert. Somit können alle (alten) USB-Kabel genutzt werden, welche diese 2 Leitungen besitzten.<br>
Der USB PowerDelivery Standart hat für seine Kommunikation eine extra CC (Control Channel) Datenleitung. Somit können USB Kabel welche einen klassischen USB Stecker haben (Typ-A, Typ-B, Mini, Micro) nicht für PowerDelivery genutzt werden.<br>
Da normale USB Kabel für max. 3A ausgelegt sind (diese müssen dann auch schon recht hochwertig sein), sind lediglich Leistungen von max. 60W  (3A bei 20V) möglich.<br>
PowerDelivery ist jedoch in der Lage höhere Stromstärken anzubieten. Dazu müssen spezielle USB-C Kabel genutzt werden, welche über einen eingebauten E-Marker Chip verfügen und mit dem Ladegerät kommunizieren können.

Das Analysegerät "Qway-U2p" bietet die Möglichkeit solche E-Marker Chips auszulesen.


## Integration in den Space

Da mehrere Personen gleichzeitig am Basteltisch arbeiten können, wurde sich für 6 Ladestationen entschieden, die gleichmäßig auf dem mittleren Brett montiert werden sollen. Das Kabelmanagment und die dazugehörige Stromversorgung soll unter dem Tisch montiert und verlegt werden.
<br>![Table](/media/gallery/20210102_160404.jpg)<div align="center">*alle 6 verbauten Ladestationen & zentraler On/Off Schalter*</div><br>
### Neues Gehäuse
Damit die PDS100 Module sicher und auch optisch (einigermaßen) passend montiert werden können, wurde ein neues Gehäuse für den 3D Druck benötigt. Dabei sind folgende Kriterien zu erfüllen:
* Die Platine muss geschützt sein
* Module müssen fest montierbar sein
* Nutzbarkeit darf nicht eingeschränkt werden
* Abwärme muss entweichen können
* Stromkabel müssen verlegbar sein

Der erste Schritt war die nachmodelierung der vorhanden Platine: [hier zum 3D Modell](/3D_models/PowerDelivery_Board.stl)<br>
Mithilfe dieser Polygon-Version der PDS100-Platine konnte das neue Gehäuse angefertig werden: [neues Gehäuse](/3D_models/case.stl) & [Deckel](/3D_models/case_cap.stl)<br>
<img src="/media/CAD_rendering2.png" width="50%"/><img src="/media/CAD_rendering.png" width="50%"/><br>
Das Gehäuse besteht aus einer Halterung, in welche die Platine einfach reingesteckt werden kann. Ein Deckel wird passend auf den vorderen Teil der Platine raufgesteckt und schließt bündig mit der vorhanden Halterung ab. Die Öffnungen an der Ober- und Unterseite dienen der Kühlung.
<br>![animatedView](/media/CAD_rendering.gif)<br>
Zum Befestigen sind zwei Einsparungen für Muttern der Größe M4 vorgesehen. Über die Öffnung an Unterseite können die Stromkabel verlegt werden.<br>
![rendered Picture for mounting](/media/CAD_rendering_mounting.png)

#### Materialwahl
Da der Abstand zwischen Gehäuse und Spule (welche bei max. Belastung ca. 100°C erreichen kann) nur sehr wenige Millimeter beträgt, kann nicht jedes Material verwendet werden.

Material | Glastemperatur 
--- | ---
PLA | 60°C
PETG | 88°C
ABS | 104°C
annealed PLA | 150°C
Polycarbonat | 148°C

Somit würden für unsere 3D Drucker nur ABS und annealed PLA infrage kommen. Da ABS ohne Hitzekammer nur schwer zu drucken ist und wir noch keine Erfahrung über das Härten von Kunststoffen haben, haben wir die Halterungen in Polycarbonat drucken lassen.

### Platine anpassen
Damit die PDS100 Platine in das neue Gehäuse passt, müssen ein paar kleinere Änderungen vorgenommen werden. Mit einer Heizluftstation lässt sich das leicht entlöten.<br>
<img src="/media/PCB_Top_edit.jpg" width="50%"/><img src="/media/PCB_Down_edit.jpg" width="50%"/><br>
1. USB-C Buchse entfernen
2. Barrel Jack Buchse entfernen
3. Lötstopmaske mit Schleifpapier oder einen Glasfaserstift entfernen
4. Kondensator entfernen
5. Lötstopmaske mit Schleifpapier oder einen Glasfaserstift entfernen
6. (optional) PowerDelivery Trigger-IC entfernen (eventuell für andere Projekte interessant)
7. (optional) Schutz Mosfet entfernen (eventuell für andere Projekte interessant)

Durch das Entfernen der Komponenten passt die Platine nun in das Gehäuse und über die freigewordenen Durchkontaktierungen unter dem Barrel Jack kann die Stromversorgung angelötet werden (rotes Kabel = positive Spannung und blaues Kabel = Ground). Das entfernen der Lötstopmaske erleichtert das Anlöten der Kabel.

### Montage & Verkabelung
<br>![Verkabelung](/media/Verkabelung.png)<br>

- [ ] DXF Files hochladen
- [ ] Sicherungskasten fotografieren
- [ ] Verkabelung Fotografieren
- [ ] Schaltaufbau grob als Funktionsblock abbilden

### Spannungsversorgung
- [ ] verschiedene Möglichkeiten auflisten (Servernetzteile, MeanWell Netzteil)






