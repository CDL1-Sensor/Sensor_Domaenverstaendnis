# Domänenverständnis

Hier in diesem Repository teilen das Domänenverständnis unterinander und bereiten uns auf die mündlichen Abschlussprüfungen vor. 

## Sensoren
Ein Sensor ist ein Gerät, das physikalische oder chemische Veränderungen in der Umgebung misst oder erkennt und sie in ein elektrisches oder digitales Signal umwandelt. Einige gängige Arten von Sensoren sind Beschleunigungsmesser, Gyroskope und Magnetometer. Diese Sensoren werden oft in Verbindung miteinander verwendet, um genauere und umfassendere Daten zu erhalten.

### Unkalibrierte Messungen
Sensor Logger bietet uns die Möglichkeit, unkalibrierte Rohdaten von Beschleunigungsmesser, Gyroskop und Magnetometer aufzuzeichnen. Ebenfalls werden
zu den unkalibrierten Rohdaten die "normalen" Daten ebenfalls mit aufgenommen. Sensor Logger selbst gibt uns an, die unkalibrierten Rohdaten nicht zu verwenden.  
[Sensor Logger auf GitHub](https://github.com/tszheichoi/awesome-sensor-logger/)

### Beschleunigungsmesser
Die Beschleunigung und Neigung kann mit einem kleinen elektronischen Gerät, einem so genannten Beschleunigungsmesser, gemessen werden. Der Beschleunigungsmesser im mobilen Gerät liefert die XYZ-Koordinatenwerte, die zur Messung der Position und der Beschleunigung des Geräts verwendet werden. Die XYZ-Koordinate gibt die Richtung und Position des Geräts an, bei der die Beschleunigung aufgetreten ist. Die X-Achse (links/rechts), die Y-Achse (oben/unten) und die Z-Achse (vorn/hinten)

### Gesamtbeschleunigungsmesser


### Schwerkraft
Ein Smartphone mit einem Schwerkraftsensor kann den Winkel, die Höhe und die Neigung der aktuellen Position bestimmen. Ein mobiles Gerät muss über ein Gyroskop und einen Beschleunigungsmesser verfügen, um die Schwerkraft richtig zu erkennen. Der Schwerkraftsensor kann kein Magnetometer als Input verwenden.

### Gyroskop
Gyroskop sind wesentliche Komponenten zur Messung von Orientierung und Bewegung. Gyroskop sind besonders nützlich bei der Erkennung von Rotationsbewegungen und Änderungen der Ausrichtung. So können sie beispielsweise erkennen, wenn ein Smartphone gekippt oder gedreht wird, was eine Bildschirmdrehung und gestenbasierte Steuerung ermöglicht. 

### Magnetometer
Das Magnetometer ist ein digitaler Kompass, der wie ein analoger Kompass arbeitet und genutzt werden kann. Das Magnetometer nutzt das Megnetfeld  der Erde, um die Nordrichtung zu ermitteln. Sie messen also die Stärke und Richtung von Magnetfeldern und ermöglichen es dem Smartphone, sich im Verhältnis zum Magnetfeld der Erde zu orientieren.

### Orientierung
Die Orientierungssensoren verwenden Daten von den Beschleunigungsmessern, um die Richtung der Schwerkraft und Änderungen der linearen Beschleunigung zu bestimmen. Die Gyroskope liefern Informationen über Winkelgeschwindigkeit und Drehung, während Magnetometer die Richtung des Telefons relativ zum Erdmagnetfeld bestimmen.

## Verarbeitung von Signaldaten


## Machine Learning Modellen


## Deep Learning Modelle


## Klassifikationsmetriken

Damit wir wissen wie gut unsere Klassfikationsmodelle performen benötigen wir eine sogenannte Performance Metriken, die uns sagen, wie gut das erstellte Modell tatsächlich auf den Testdaten performt.
Bei den Klassifikationen von Bewegungsprofilen nutzen wir daher die Metriken: Accuracy, Recall, Precision, F1-Score. 

### Confusion Matrix

|                     | Wahrheit: Positiv   | Wahrheit: Negativ   |
|---------------------|---------------------|---------------------|
| Vorhersage: Positiv | True Positiv (TP)   | False Positiv (FP)  |
| Vorhersage: Negativ | False Negativ (FN)  | True Negativ (TN)   |




### Accuracy

DIe Accuracy ist ein

### Recall


### Precision


### F1-Score

Der F1-Score ist der Harmonische Mittelwert von Recall und Precision.  
Wichtig bei einer Multiklass Klassifikation ist, dass wir nicht nur einen F1-Score bzw. einen Recall und Precision erhalten sondern mehrer. Aus diesem Grund gibt es verschiedene Mittelwerte die wir bei F1-Score nehmen können. F1-Score Macro, F1-Score Micro, F1-Score Average, F1-Score Weighted

#### F1-Score Average



#### F1-Score Weighted

#### F1-Score Micro

#### F1-Score Macro



### 


## Applikation

