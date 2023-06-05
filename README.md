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

Die Verarberitung der Sensordaten ist wichtig, damit unsere Modelle auch richtig und gute vorhhersagen machen können. Damit diese besser ist, wurden die Daten getrimmt und Aggregiert.

### Trimmen 

Von Jeder Messung haben wir die ersten und letzten 5 Sekunden abgeschnitten. Denn gemäss der Vereinbaerung, wie man die Sensordaten aufnehmen sollte, sind die ersten 5 Sekunden und die letzten 5 Sekunden irreleveant für das Bewegungsprofil.
Die ersten und letzten 5 Sekunden ist die Bewegung, dass das Handy in die Hosentasche.

### Aggregation in 5 Sekunden Fenster

Damit wir mehr Features aus unseren Daten generieren, wurden die Messungen in einem 5 Sekunden Zeitfenster aggregiert. Dabei berücksichtigt wurden die Frequenzen der Messungen. Jede Messung hat mehr oder weniger eine andere Frequenz und musste somit beim aggregieren in 5 Sekunden Zeitfesnter mirberücksichtigt werden. Die Überlappung der Zeitfenster 

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

### [Multiple Logistische Regression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)

Beim Baseline Modell, unserer Multiple logsitischen Regression haben wir dafür die kompletten unverarbeiteten Rohdaten genommen. Aufgrund unserer definierten Metrik der Accuracy, afu welche wir optimieren, wurden ein undersampling vom rohdatensatz gemacht bevor das Modell trainiert wurde. Dadurch gab es von jeder Klasse die genau gleiche Anzahl an Observationen, sowohl für den Trainingsdatensatz als auch Testdatensatz. 

Beim Multiple Logistische Regression klassifizieren wir sechs Target Werte, unsere Bewegungsprofile. Dies geschieht durch unsere Multiple Logsitische Regression und dem Paramater "OvR" welches für One-vs-Rest Methode ist.
Der Trainingsprozess in der OvR-Methode besteht aus folgenden Schritten:

1) Für jede Klasse wird ein separates binäres Modell erstellt.
2) Im ersten Schritt wird ein Modell trainiert, um die erste Klasse von den restlichen Klassen zu unterscheiden. Dazu werden alle Beispiele der ersten Klasse als positive Beispiele und alle Beispiele der anderen Klassen als negative Beispiele verwendet.
3) Im zweiten Schritt wird ein Modell trainiert, um die zweite Klasse von den restlichen Klassen zu unterscheiden. Diesmal werden alle Beispiele der zweiten Klasse als positive Beispiele und alle Beispiele der anderen Klassen als negative Beispiele verwendet.
4) Dieser Prozess wird für jede Klasse wiederholt, bis ein separates binäres Modell für jede Klasse erstellt wurde.

Beim Vorhersageprozess wird dann jedes Modell angewendet, um die Wahrscheinlichkeit zu berechnen, dass eine Eingabe zu dieser spezifischen Klasse gehört. Die Klasse mit der höchsten Wahrscheinlichkeit wird schliesslich als Vorhersage ausgewählt.

### [Decision Tree Classifier](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html)
Der Name Decision Tree leitete sich aus dem Erscheinungsbild ab, welches einem Baum entspricht. Ein Decision Tree besteht aus Wurzeln, Ästen und Blätter, dabei wird der Decision Tree immer von oben nach unten betrachtet. Der Decision Tree ist also hierarchisch aufgebaut. Als Start dient uns ein Wurzelknoten, wird auch Root Node oder Root genannt, diese beinhaltete eine binaere Entscheidung (True oder False) die getroffen wird. Je nachdem, wie die Entscheidung fiel, wandert man einem Pfad bzw. Ast entlang zum naechsten Knotenpunkt, diese wird auch Branches oder Internal Nodes genannt, beim naechsten Knotenpunkt wird wieder eine binaere Entscheidung gefaellt, um einen weiteren Pfad zu nehmen. Dies geschieht solange bis man an das Ende angekommen ist. Das Ende eines Decision Tree nennt man auch Blatt, Leaf Nodes oder Leaf. Haeufig werden Decision Tree verwendet, um Klassifikations Aufgaben zu loesen. Am Ende vom Decision Tree, kann man somit Aussagen treffen, wie bsp. um welches Bewegungsprofil es sich handelt.

Der Decision Tree von Sklearn hat dabei unterschiedliche Parameter, hier werden wir kurz einige beschreiben. 

1) criterion: Das Kriterium zur Bewertung der Qualität einer Aufteilung. "gini" verwendet den Gini-Index, "entropy" verwendet den Informationsgewinn.   
2) max_depth: Die maximale Tiefe des Entscheidungsbaums. Es begrenzt die Anzahl der Entscheidungsknoten im Baum.   
3) min_samples_split: Die minimale Anzahl von Datenpunkten, die erforderlich sind, um eine Aufteilung in einen internen Knoten durchzuführen.   
4) min_samples_leaf: Die minimale Anzahl von Datenpunkten, die erforderlich sind, um einen Blattknoten zu bilden.   
5) max_features: Die maximale Anzahl der Funktionen, die bei der Suche nach der besten Aufteilung berücksichtigt werden.   
6) random_state: Der Startwert für die Zufallsgeneratoren zur Wiederholbarkeit der Ergebnisse.   

Overfitting kann entstehen, wenn man zu viel Branches erstellt und die Daten nicht mehr generalisierbar auf neue Daten sind, um das Overfitting zu vermeiden.   

### [Random Forest Classifier]()
Ähnlich wie beim Decision Tree besteht auch der Random Forest Classifier aus einer Hierarchie von Wurzeln, Ästen und Blättern, die wie ein Baum strukturiert sind. Jeder Baum im Random Forest wird unabhängig voneinander trainiert, wobei verschiedene Teilmengen der Trainingsdaten zufällig ausgewählt werden.

Um Vorhersagen zu treffen, werden die Testdaten durch jeden Baum im Random Forest geleitet. Jeder Baum trifft Entscheidungen basierend auf den Merkmalen der Daten und gibt eine Vorhersage aus. Im Fall einer Klassifikationsaufgabe könnte die Vorhersage beispielsweise eine Klasse oder ein Label sein.

Nachdem alle Bäume ihre Vorhersagen gemacht haben, wird eine "Mehrheitsabstimmung" durchgeführt, um die endgültige Vorhersage des Random Forest Classifiers zu ermitteln. Die Klasse, die von den meisten Bäumen vorhergesagt wird, wird als das endgültige Ergebnis ausgewählt.

Der Random Forest Classifier hat verschiedene Parameter, die seine Leistung beeinflussen können:

1) n_estimators: Die Anzahl der Bäume im Random Forest. Eine grössere Anzahl von Bäumen kann zu einer besseren Leistung führen, aber auch zu höheren Rechenkosten.
2) max_features: Die maximale Anzahl von Merkmalen, die bei der Suche nach der besten Aufteilung in jedem Baum berücksichtigt werden. Durch die Begrenzung der Anzahl von Merkmalen kann die Korrelation zwischen den Bäumen verringert und die Vielfalt im Ensemble erhöht werden.
3) max_depth: Die maximale Tiefe jedes einzelnen Baums im Random Forest. Eine grössere Tiefe ermöglicht es den Bäumen, komplexere Muster in den Daten zu lernen, erhöht jedoch auch das Risiko von Overfitting.
4) min_samples_split: Die minimale Anzahl von Datenpunkten, die erforderlich sind, um eine Aufteilung in einen internen Knoten durchzuführen. Dieser Parameter hilft, Overfitting zu reduzieren, ähnlich wie beim Decision Tree.

Der Random Forest Classifier bietet mehrere Vorteile, darunter die Fähigkeit, mit hoher Genauigkeit komplexe Entscheidungsgrenzen zu erlernen, die Robustheit gegenüber Ausreissern und fehlenden Daten und die Fähigkeit, die Bedeutung der Merkmale zu bewerten. Durch den Einsatz von zufälligen Teilmengen der Daten und Merkmale hilft der Random Forest auch, Overfitting zu reduzieren und eine bessere Generalisierung auf neuen Daten zu erzielen

### [Stochastic Gradient Descent Classifier](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.SGDClassifier.html#sklearn.linear_model.SGDClassifier)
Der SGD Classifier verwendet eine lineare Entscheidungsgrenze, um zwischen verschiedenen Klassen zu unterscheiden. Es handelt sich um einen iterativen Algorithmus, der die Gewichte des linearen Modells schrittweise anpasst, um den Fehler zu minimieren. Der Name "stochastischer Gradientenabstieg" bezieht sich auf die Verwendung von zufällig ausgewählten Teilgruppen von Trainingsdaten, um die Gewichtsaktualisierungen durchzuführen.

Der Algorithmus beginnt mit zufällig initialisierten Gewichten und durchläuft die Trainingsdaten in Iterationen. In jeder Iteration wird eine zufällig ausgewählte Teilmenge der Trainingsdaten verwendet, um die Gewichte zu aktualisieren. Dieser Schritt wird als stochastischer Gradientenabstieg bezeichnet, da die Gewichtsaktualisierungen aufgrund der zufälligen Teilgruppen von Daten stattfinden.

Der SGD Classifier hat verschiedene Parameter, die angepasst werden können, um die Leistung des Modells zu optimieren:
1) loss: Die Verlustfunktion, die minimiert werden soll. Für Klassifikationsaufgaben kann dies beispielsweise die logistische Verlustfunktion (log loss) oder die hinge-Verlustfunktion sein.
2) alpha: Der Regularisierungsparameter, der die Stärke der Regularisierung steuert. Die Regularisierung hilft, Overfitting zu reduzieren, indem sie die Grösse der Gewichte begrenzt.
Der SGD Classifier bietet mehrere Vorteile, darunter seine Fähigkeit zur effizienten Verarbeitung grosser Datensätze und die Anpassungsfähigkeit an Online-Lernszenarien, bei denen neue Daten schrittweise eingeführt werden. Es kann auch mit sparse Daten umgehen, bei denen viele Merkmale den Wert Null haben. Der SGD Classifier ist jedoch anfällig für das Einstranden in lokale Minima und kann empfindlich auf die Wahl der Hyperparameter reagieren.

Insgesamt ist der SGD Classifier ein flexibler und effizienter Algorithmus für lineare Klassifikationsaufgaben, der in vielen Anwendungen erfolgreich eingesetzt werden kann.

## Deep Learning Modelle
Der Hauptunterschied zwischen Deep Learning und Machine Learning liegt in der Art und Weise, wie diese Ansätze Daten verarbeiten.   
Während traditionelle Machine-Learning-Methoden manuell entwickelte Merkmale (Features) aus den Daten extrahieren (Aggregation von unseren Sensordaten), sind Deep Learning Modelle in der Lage, automatisch abstrakte Merkmale aus den Rohdaten zu lernen.   
Dies ermöglicht Deep Learning-Modellen, komplexere Muster und Strukturen in den Daten zu erkennen.  

![image](https://github.com/CDL1-Sensor/Sensor_Domaenverstaendnis/assets/66916399/30bb163a-6e65-48fa-8e64-54fd3e8c9d63)

In unserer Challenge haben wir hauptsächlich nur mit dem Tensorflow Deep Learning Framework auseinandergesetzt.

### Tensoren

Tensoren sind mathematische Objekte, die mittels der Grundlagen der linearen Algebra verwendet werden, um mehrere Vektoren oder Matrizen gleichzeitig abzubilden. Ein Tensor kann als multidemensionale erweiterung eines Skalars oder Vektors betrachtet werden. Numpy arrays in Python sind jeweils direkt kompatible Tensor Tensorflow objekte. In Tensorflow werden Tensoren als zentrale Datenstruktur verwendet, um sowohl Eingangsdaten als auch Modellparameter zu speichern. Durch die Verwendung von Tensoren können Deep Learning-Modelle effizient auf GPUs und TPUs ausgeführt werden, um schnelle Trainings- und Vorhersagezeiten zu ermöglichen. Wärend Matrizen nur den 2. Dimensionalen Raum abdecken. Sind Tensoren multidimensional. Auf Tensoren gelten nicht Matrizen Operationen, sondern eigene. (siehe Tensorproduct, Kontraktion und Tensorzerlegung) 

### Convolutional Neural Network (CNN)

Das Convlolutional Neural Network kann man sich wie ein Filter vorstellen, der durch die Daten bzw. Vektoren geht und jeweils den nur einen Teilbereich aus dem Vektor sich betrachtet und diese mit dem Filter multipliziert. 

### Recurrent Neural Network (RNN)

### Long short-term memory (LSTM) 
LSTM ist eine Erweiterung von einem RNN 

## Klassifikationsmetriken

Damit wir wissen wie gut unsere Klassfikationsmodelle performen benötigen wir eine sogenannte Performance Metriken, die uns sagen, wie gut das erstellte Modell tatsächlich auf den Testdaten performt.
Bei den Klassifikationen von Bewegungsprofilen nutzen wir daher die Metriken: Accuracy, Recall, Precision, F1-Score und loggen jeweils die Trainings und Test Werte ins Weight and Bias mit. 

### Confusion Matrix

![image](https://github.com/CDL1-Sensor/Sensor_Domaenverstaendnis/assets/66916399/bf621036-9337-4c70-81ad-9fa7131f6828)

### Accuracy
Wenn man ein Modell entwickelt hat, das Bewegungsprofile von Personen in verschiedene Aktivitäten wie Gehen, Laufen und Radfahren klassifiziert, ist die Accuracy eine geeignete Metrik, um die Gesamtleistung des Modells zu bewerten. Man kann die Accuracy verwenden, um zu messen, wie gut das Modell insgesamt in der Lage ist, die Aktivitäten korrekt zu identifizieren.

### Recall
Möchte man sicherstellen, dass alle Fälle einer bestimmten Aktivität richtig erkannt werden, könnte der Recall eine wichtige Metrik sein. Zum Beispiel, wenn es darum geht, Stürze bei älteren Menschen zu erkennen, ist es entscheidend, dass das Modell alle Sturzereignisse richtig identifiziert, um rechtzeitig Hilfe zu leisten. In diesem Fall wäre der Recall eine relevante Metrik, um die Erkennungsrate von Stürzen zu bewerten.

### Precision
Die Präzision gibt an, wie gut ein Modell darin ist, wahre positive Ergebnisse von falsch positiven Ergebnissen zu unterscheiden. Ein hohes Präzisionsniveau bedeutet, dass das Modell eine geringe Anzahl von falsch positiven Vorhersagen hat, während ein niedriges Präzisionsniveau darauf hinweist, dass das Modell viele falsch positive Vorhersagen macht.

### F1-Score
Der F1-Score ist eine geeignete Metrik, wenn man eine ausgewogene Bewertung der Leistung des Modells benötigt, die sowohl Precision als auch Recall berücksichtigt. Wenn man beispielsweise Bewegungsprofile von Personen in Aktivitäten wie Gehen, Laufen und Treppensteigen klassifiziert, möchte man sowohl eine hohe Erkennungsrate der Aktivitäten als auch eine genaue Klassifizierung sicherstellen, um Verletzungen zu vermeiden. Der F1-Score gibt eine ausgewogene Einschätzung der Gesamtleistung des Modells in Bezug auf Precision und Recall.

## Applikation

