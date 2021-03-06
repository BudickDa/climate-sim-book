# Das System

Im Folgenden soll das Klima aus systemtheoretischer Sicht betrachtet werden. Dazu müssen vorher einige Begrifflichkeiten geklärt werden:
* **Knoten:** Jedes System besteht aus Knoten, welche eigenständige Elemente sind, und aus Verbindungen zwischen den Knoten. Das vorliegende System besteht nur aus Subsystemen und Elementen.
* **Element:** Hat Ein- und Ausgänge und interne Logik und Eigenschaften. Im vorliegenden System sind die Höhenlevel die Elemente. Sie interagieren mit der Umwelt und haben eine interne Logik. Man kann hierbei auch von Agenten sprechen.
* **Subsystem:** Ein Subsystem kann entweder eine Anordnung von Systemen sein (z. B.: Ein Biom (Subsystem) besteht aus drei Leveln (Subsystem)) oder ein System bestehend aus einzelnen Elementen.
* **Gesamtsystem:** Das Gesamtsystem ist die Summe aller Subsysteme. In diesem Fall alle Biome.


## Das Biom
Ein Biom ist ein virtuelles Gebiet mit einer bestimmten Fläche. Jedes Biom wurde in drei Höhenlevel unterteilt: 
- Level 1: Der Boden.
- Level 2: Untere Atmosphäre (ca. 3000 m)
- Level 3: Obere Atmosphäre (ca. 7000 m)

Jedes Level hat eigene klimatische Bedingungen, die sich auf die unteren Level auswirken können:
- Bewölkung: Dämpft das Sonnenlicht
- Regen: Senkt die Luftfeuchtigkeit

Die Level interagieren mit den Leveln des anschließenden Bioms, sofern Wind weht. Diese Interaktion findet immer auf gleicher Höhe statt: z. B. Level 1 => Level 1, Level 2 => Level 2 etc.

Somit werden z. B. Wolken von einem Biom in das nächste geweht.

<div style="page-break-after: always;"></div>


## Das Gesamtsystem
Das Gesamtsystem hat mehrere Ebenen. In der obersten Ebene wird die Interaktion der Biome beschrieben. Zur Vereinfachung sind die Biome nur eindimensional angeordnet.
Die eintreffende Strahlungsenergie der Sonne ist abhängig von Position und Zeit. Zur Vereinfachung wird angenommen, dass sich alle Biome auf demselben Breiten und Längengrad befinden.

Eine weitere Vereinfachung ist, dass die Interaktion der Biome nur von Westen nach Osten erfolgen kann (der Wind weht nur von Westen nach Osten).
Das Resultierende System kann wie folgt abgebildet werden:

![Das System abgebildet](system.jpg)

Am Anfang steht ein sogenanntes Seed-Biom. Die Eigenschaften dieses Biomes werden am Anfang gesetzt. 

Die Biome selbst haben zwei Eingänge und einen Ausgang. Der erste Eingang ist für die Aufnahme von Strahlungsenergie (Sonnenschein) zuständig. Der andere nimmt die durch den Wind herangetragenen Eigenschaften des vorherigen Biomes an. Der Ausgang gibt sie an das nächste Biom weiter.

Die Level jedes Biomes interagieren über den Wind mit dem der Höhe entsprechenden nächsten Biom. Wenn auf der entsprechenden Höhe zwischen zwei Biomen Wind weht, beeinflussen die Eigenschaften des vorherigen Biomes die des nächsten.

Aus den herangetragenen Werten wird mit Hilfe der internen Logik der momentane Ist-Zustand ermittelt. Anschließend werden dem Ist-Zustand entsprechend die Werte der Ausgänge gesetzt.
Jedes Element kann auf die Werte der benachbarten Elemente zugreifen und entscheidet nach festgelegten Regeln ob es die Werte aufnimmt:
z. B.:

| Biom 1 - Level 1 | Biom 2 - Level 1 |
| -- | -- |
| Luftdruck: 1200 | Luftdruck: 1000 |
| Temperatur: 28 | Temperatur: 25  ||

Biom 2 ermittelt:<br/>
$$Luftdruck_{B1L1}>Luftdruck_{B2L1} => v_{wind}>0$$<br/>
Da der Luftdruck in Biom 1 höher ist als in Biom 2, weht Wind. 
Daraus folgt, dass die Temperatur aus Biom 1 die Temperatur in Biom 2 beeinflusst (in diesem Fall erhöht).

<div style="page-break-after: always;"></div>
## Abhängigkeiten und Reihenfolge
Wie im Kapitel [Die Erde](die_erde.md) bereits erörtert wurde, hängen die diversen klimatischen Bedingungen zusammen. 
Die Bewölkung ist zum Beispiel abhängig von Luftfeuchtigkeit und Temperatur in einer bestimmten Luftschicht. Daraus folgt, dass bevor die Bewölkung ermittelt werden kann, Temperatur und Luftdruck festgelegt werden müssen. 
![](setClouds.PNG)

Die Reihenfolge ist in diesem System allerdings nicht von Bedeutung. 
Da die Simulation in einer Dauerschleife erfolgt, ist es irrelevant, ob z. B. zuerst die Bewölkung und dann der Regen berechnet wird, da im nächsten Durchgang die Berechnung der Bewölkung auf die Berechnung des Regens erfolgt und vice versa.

Die Abhängigkeit ist allerdings von Bedeutung, da es einen ersten Durchgang gibt, in dem nur das Seed-Biom Daten besitzt. Die Abhängigkeiten in diesem System sind Temperatur und Luftfeuchtigkeit. Die Temperatur hängt wiederum von der Bewölkung und der Sonneneinstrahlung ab. Die Luftfeuchtigkeit davon, ob es regnet und der Temperatur. Die Sonneneinstrahlung ist nur von Ort und Zeit abhängig und dadurch immer gegeben. Bleibt also nur die Bewölkung als ursprüngliche Abhängigkeit übrig.

Damit wäre die Bewölkung abhängig von der Temperatur und die Temperatur wiederum von der Bewölkung. Dieses Problem wird dadurch gelöst, dass im Modell die folgende Annahme gilt:

**Wenn die Bewölkung nicht definiert ist, wird die Abwesenheit von Wolken angenommen. Der Himmel ist also wolkenfrei.**


