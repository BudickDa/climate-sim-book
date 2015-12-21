# Fazit
Die vorliegende Simulation ist weit von der Realität entfernt. Das Klima ist viel zu komplex als dass es durch einen Laien implementiert werden kann. Das war allerdings auch nicht das Ziel. 

Das Ziel war zum einen, eine Karte zu generieren, deren Klimazonen sinnvoll sind. Zum anderen zu zeigen, wie beliebig komplexe Systeme in kleinste Bausteine zerlegt werden können, die wiederverwendbar und überprüfbar sind.

Betrachtet man das zugehörige Softwareprojekt so findet man in den Dateien `test_*.js` Unit-Tests der Funktionen. Komplexe Systeme sind schwer zu überblicken, weswegen die Korrektheit der Implementierung im gesamten schwer zu überprüfen ist.

Die funktionale Programmierung bietet aber einen Ausweg.
Zum einen kann ein Wirkungsnetz übersichtlich als Code abgebildet werden. Einzelne Elemente werden zu Funktionen, Subsysteme werden zu Funktionen die aus mehreren Funktionen bestehen. Zum anderen sind die Elemente test- und wiederverwendbar. Durch das Vermeiden von Redundanz bleibt die Codebasis übersichtlich und nachvollziehbar. Komplexität entsteht durch die korrekte Kombination von einfachen Funktionen. Fehler können, wenn die einzelnen Funktionen getestet wurden, nur noch in der Kombination derselbigen auftreten. 

Da die Kombination durch den Entwurf bestimmt wird und einfach umsetzbar ist (z. B. mit `_.compose`), ist ein Systemfehler meistens dem Entwurf geschuldet und kein Fehler in der Implementierung. Handelt es sich doch um einen Fehler in der Implementierung, ist schnell gefunden.
Ein weiterer Vorteil, ist das Cachen von Funktionen. Mit `_.memoize( )` wird ein und Ausgabe einer Funktion beim ersten Ausführen gespeichert. Dieses Vorgehen bietet bei richtiger Anwendung gewaltige Verbesserungen in der Performanz.

Eine letzte Anforderung war die Eignung für eine prozedurale Spielewelt. Jeder Teil einer prozeduralen Spielewelt soll generiert werden können, ohne das Informationen über seinen Nachbar vorhanden sind. Dies ist mit dem vorliegenden System möglich. Es wird von einem Startwert aus bis zum aktuellen Standort aus jedes Biom durchiteriert. Der begrenzte Stack schränkt die Anzahl der Iterationen allerdings ein.
Dieses Problem kann umgangen werden, da die Iteration an jedem Biom abgebrochen und mit den Werten des Biomes am Abbruch eine neue Iteration gestartet werden kann.
Angenommen es können nur maximal 500 Biome pro Durchgang verarbeitet werden. Es wird aber das Biom an Position 800 benötigt. 

Die Lösung: Es werden die ersten 500 Biome verarbeitet. Das Ergebnis (Biom 500) wird der Startwert für den zweiten Durchgang. An Position 301 wird gestoppt. Das Ergebnis sind die Daten von Biom 800.
