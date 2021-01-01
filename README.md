# PowerDelivery für den Hackerspace
Der Arbeitstisch sollte um eine zentrale Ladeeinrichtung für Smartphones, Laptops und andere Gerätschaften erweitert werden.<br>
Dafür bietet sich der mitterweile weit verbreitete "USB PowerDelivery" Ladestandart an, welcher Spannungen im Bereich **5V bis 20V mit bis zu 5A** (also max. 100W) zur Verfügung stellt.

Die Grundlage dieses Projektes ist ein fertig Board, dass man unter dem Namen "PDS100" bei den bekannten asiatischen Kaufplattformen erwerben kann. Das Board basiert auf dem Chip SW3518S vom Hersteller ISMARTWARE.<br>
Die genaue Analyse und überprüfung des Boards kann [hier](analyse.md) nachgelesen werden.

- [ ] Bilder vom Tisch mit Lademodulen machen

## Das Lademodul "PDS100"

- [ ] Bilder von dem Modul mit Gehäuse
- [ ] Ein paar Fakten zu dem Modul schreiben (z.B. Spannungsversorgung, StepDown Regler)


## Unterstütze Charge Protokolle

### getestet durch ein Qway-U2p Analysegerät
* **Quick Charge 2.0** -QC2
  * Qualcomm
  * 5V, 9V, 12V, 15V, 20V mit max. 3A
* **Quick Charge 3.0** -QC3
  * Qualcomm
  * 3,7V - 20V (0,2V Steps) mit max. 3A
* **PowerDelivery 2.0** -PD2
  * 5V, 9V, 12V, 15V, 20V mit max. 5A
  * aka Quick Charge 4
* **PowerDelivery 3.0** -PD3
  * 3,3V - 20V (0,2V Steps) mit max. 5A
  * aka PPS oder Quick Charge 4+
* **Adaptive Fast Charge** -AFS
  * Samsung
  * 5V, 9V, 12V mit max. 3A
* **Fast Charge Protocol** -FCP
  * Huawei
  * 5V, 9V, 12V mit max. 2A
* **Super Charge Protocol** -SCP
  * Huawei
  * 3,4V - 5,5V mit max. 5A
* **Pump Express 1.1** -PE1.1
  * Mediatek
  * 5V, 7V, 9V, 12V
* **Pump Express 2.0** -PE2.0
  * Mediatek
  * 5V - 20V (0,5V Steps)
* **Apple Charge**
  * 5V mit max. 2,4A

### laut Datenblatt 
* **Super Fast Charge Protocol** -SFCP
  * Huawei
* **Voltage Open Loop Multi-step Constant-Current Charging** -VOOC
  * OPPO / VIVO
  * aka Dash Charge or Warp Charge

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




