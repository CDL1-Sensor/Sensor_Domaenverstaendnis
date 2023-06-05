# Domänenverständnis

Hier in diesem Repository teilen wir das Domänenverständnis im Team und bereiten uns auf die mündlichen Abschlussprüfungen vor. 

## Sensoren
Ein Sensor ist ein Gerät, das physikalische oder chemische Veränderungen in der Umgebung misst oder erkennt und sie in ein elektrisches oder digitales Signal umwandelt. Einige gängige Arten von Sensoren sind Beschleunigungsmesser, Gyroskope und Magnetometer. Diese Sensoren werden oft in Verbindung miteinander verwendet, um genauere und umfassendere Daten zu erhalten.

### Unkalibrierte Messungen
Sensor Logger bietet uns die Möglichkeit, unkalibrierte Rohdaten von Beschleunigungsmesser, Gyroskop und Magnetometer aufzuzeichnen. Ebenfalls werden
zu den unkalibrierten Rohdaten die "normalen" Daten ebenfalls mit aufgenommen. Sensor Logger selbst gibt uns an, die unkalibrierten Rohdaten nicht zu verwenden.  
[Sensor Logger auf GitHub](https://github.com/tszheichoi/awesome-sensor-logger/)

### Beschleunigungsmesser
Die Beschleunigung und Neigung kann mit einem kleinen elektronischen Gerät, einem so genannten Beschleunigungsmesser, gemessen werden. Der Beschleunigungsmesser im mobilen Gerät liefert die XYZ-Koordinatenwerte, die zur Messung der Position und der Beschleunigung des Geräts verwendet werden. Die XYZ-Koordinate gibt die Richtung und Position des Geräts an, bei der die Beschleunigung aufgetreten ist. Die X-Achse (links/rechts), die Y-Achse (oben/unten) und die Z-Achse (vorn/hinten)

### Schwerkraft
Ein Smartphone mit einem Schwerkraftsensor kann den Winkel, die Höhe und die Neigung der aktuellen Position bestimmen. Ein mobiles Gerät muss über ein Gyroskop und einen Beschleunigungsmesser verfügen, um die Schwerkraft richtig zu erkennen. Der Schwerkraftsensor kann kein Magnetometer als Input verwenden.

### Gyroskop
Gyroskop sind wesentliche Komponenten zur Messung von Orientierung und Bewegung. Gyroskop sind besonders nützlich bei der Erkennung von Rotationsbewegungen und Änderungen der Ausrichtung. So können sie beispielsweise erkennen, wenn ein Smartphone gekippt oder gedreht wird, was eine Bildschirmdrehung und gestenbasierte Steuerung ermöglicht. 

### Magnetometer
Das Magnetometer ist ein digitaler Kompass, der wie ein analoger Kompass arbeitet und genutzt werden kann. Das Magnetometer nutzt das Megnetfeld  der Erde, um die Nordrichtung zu ermitteln. Sie messen also die Stärke und Richtung von Magnetfeldern und ermöglichen es dem Smartphone, sich im Verhältnis zum Magnetfeld der Erde zu orientieren.

### Orientierung
Die Orientierungssensoren verwenden Daten von den Beschleunigungsmessern, um die Richtung der Schwerkraft und Änderungen der linearen Beschleunigung zu bestimmen. Die Gyroskope liefern Informationen über Winkelgeschwindigkeit und Drehung, während Magnetometer die Richtung des Telefons relativ zum Erdmagnetfeld bestimmen.

## Verarbeitung von Signaldaten

### Trimmen 
die ersten 5 sec schneiden

### Aggregation in 5 Sekunden Fenster
min, max, mean, median


## Machine Learning Modellen
Im Bereich des Machine Learning definieren wir eine Zielvariable, die in unserem Fall unsere Bewegungsprofile darstellt. Diese dienen als Zielvariable. Die Eingangsvariablen, also unsere Features, sind die aggregierten Sensordaten.
Mit Hilfe des Sklearn-Frameworks haben wir verschiedene Machine Learning-Modelle erstellt und unsere Daten darauf trainiert und validiert, um Bewegungsprofile zu generieren.

### Hyperparameter Tuning mit Weights & Bias
Da unsere Modelle unterschiedliche Parameter haben können und diese einen grossen Einfluss auf unsere Accuracy hatte, haben wir mittels Weights & Bias Hyperparameter Tuning betrieben. Der Vorteil bei Weights & Bias war, dass wir somit unsere Hyperparameter Tuning live mitverfolgen konnten und somit diverse Hunderte Modelle austesten konnten und deren Metriken berechnen und übersichtlich darstellen. 
Die Weights & Bias Hyperparameter Tuning sind unter dem folgenden Link zu finden: 

### Cross Validation
Die Cross Validation ist ein Verfahren die uns die Fehlerabschätzung unserer Zielmetrik berechnet. Da wir unseren Datensatz aufgrund vom File Namen splitten, um Data Leakage zu verhindern ist, hat der Train - Validation Split einen grossen Einfluss auf unsere Metrik. Der Grund hierfür ist auch, dass ein File unterschiedlich lange sein kann. 

Das Bild verdeutlich das prinzip der Cross Validierung.   
Bemerkung: Achtung, in unserem Fall sind die Train und Test grössen bei jedem Split unterschiedlich gross.

![image](https://github.com/CDL1-Sensor/Sensor_Domaenverstaendnis/assets/66916399/049467f8-653e-4bf0-9962-a3cc2939fc16)

Auch hier haben wir die Cross Validierung mittels Weights and Bias verfolgt, da wir vom besten Hyperparameter Tuning Modell, mehrere Runs mit unterschiedlichen Split Seeds und Model Seeds verwendet haben, aber die Hyperparameter fixierd haben. Somit konnten wir von unserem besten Modell die Fehler der Metriken, sprich den Mittelwert und die Standardabweichung berechnen und visualisieren. 

### Multiple Logistische Regression



### Decision Tree Classifier

### Random Forest Classifier

### Stochastic Gradient Descent Classifier

## Deep Learning Modelle

Der Hauptunterschied zwischen Deep Learning und Machine Learning liegt in der Art und Weise, wie diese Ansätze Daten verarbeiten.   
Während traditionelle Machine-Learning-Methoden manuell entwickelte Merkmale (Features) aus den Daten extrahieren (Aggregation von unseren Sensordaten), sind Deep Learning Modelle in der Lage, automatisch abstrakte Merkmale aus den Rohdaten zu lernen.   
Dies ermöglicht Deep Learning-Modellen, komplexere Muster und Strukturen in den Daten zu erkennen.  

![image](https://github.com/CDL1-Sensor/Sensor_Domaenverstaendnis/assets/66916399/30bb163a-6e65-48fa-8e64-54fd3e8c9d63)

In unserer Challenge haben wir hauptsächlich nur mit dem Tensorflow Deep Learning Framework auseinandergesetzt.

### Tensoren

Tensoren sind mathematische Objekte, die mittels der Grundlagen der linearen Algebra verwendet werden, um mehrere Vektoren oder Matrizen gleichzeitig abzubilden. Ein Tensor kann als multidemensionale erweiterung eines Skalars oder Vektors betrachtet werden. Numpy arrays in Python sind jeweils direkt kompatible Tensor Tensorflow objekte. In Tensorflow werden Tensoren als zentrale Datenstruktur verwendet, um sowohl Eingangsdaten als auch Modellparameter zu speichern. Durch die Verwendung von Tensoren können Deep Learning-Modelle effizient auf GPUs und TPUs ausgeführt werden, um schnelle Trainings- und Vorhersagezeiten zu ermöglichen. Wärend Matrizen nur den 2. Dimensionalen Raum abdecken. Sind Tensoren multidimensional. Auf Tensoren gelten nicht Matrizen Operationen, sondern eigene. (siehe Tensorproduct, Kontraktion und Tensorzerlegung) 

### Convolutional Neural Network (CNN)

### Recurrent Neural Network (RNN)

### Long short-term memory (LSTM) 
LSTM ist eine Erweiterung von einem RNN 

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

#### F1-Score Weighted



### 


## Applikation

