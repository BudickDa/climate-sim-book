# Die Idee

Prozedurale Generierung ermöglicht es, gigantische Welten abzubilden, die weder von einem Menschen designt noch auf einem Datenträger gespeichert worden sind. Das im nächsten Jahr veröffentlichte Videospiel *No Man's Sky* findet in einem Universum statt, welches komplett von einem Algorithmus generiert wird. Anhand der Position und Blickrichtung des Spielers, wird die direkte Umwelt in drei Ebenen (level of detail) gerendert. Einmal die direkte Umgebung, dann die Fernsicht auf dem jeweiligen Planeten und in der dritten Ebene Planeten und Sternsysteme in der Nähe [1].

Jeder Stern, den der Spieler sieht, kann auch besucht werden. Fast jeder Stern ist Teil eines Sonnensystems mit Planeten und Monden. Insgesamt wird die Anzahl der Planeten mit $$ 2 ^{64} = 18,446,744,073,709,551,616$$ geschätzt, da diese Zahl die Länge des Seeds ist. [2]

Jeder Planet wird in Abhängigkeit seiner Position generiert, so bestimmt z. B. die Entfernung zur Sonne, ob flüssiges Wasser auf der Planetenoberfläche existieren kann, was wiederum bestimmt, ob es auf dem Planeten Meere und Flüsse gibt. 
Abstrakt betrachtet ist die gesamte Umgebung das Ergebnis einer Funktion, die lediglich die aktuelle Position im Universum als Parameter hatte.
Verdeutlichen kann man das mit dem folgenden Code-Beispiel:

    var globalSeed = 12684842;
    function generateScene(position){
      /**
       * erstellt aus der Position und dem globalenSeed einen lokalen Seed
       **/
	  var pseudoRandom = new Chance(globalSeed + position), 
	  scene = {};
	  /**
	   * gibt true zurück wenn nächste Zufallszahl ist gerade  
	   **/
	  scene.rainy = pseudoRandom.next()%2 == 0; 
    }

In diesem Fall werden Entscheidungen mit Hilfe einer Zahl aus einem Zufallsgenerator getroffen, welcher mit Hilfe der Position und dem globalen Seed geseedet wurde. Da die Funktion `next()` mit Hilfe eines deterministischen Algorithmus die nächste Pseudozufallszahl ermittelt, werden zwei Szenen mit derselben Position immer genau gleich sein.

Mit Hilfe dieses Verfahrens kann man bereits ganze Welten erstellen. Diese können jedoch sehr unnatürlich sein. 
Folgendes Beispiel: Jede generierte Szene hat ein Biom. 

Es gibt verschiedene Biome:

-	Meer
-	Wüste (hohe Temperatur)
-	Wiese
-	Sumpf
-	Schneelandschaft (Minusgrade)
	


    var globalSeed = 12684842;
    var bioms = ['Meer', 'Wüste', 'Wiese', 'Sumpf', 'Schneelandschaft'];
    
    function generateScene(position){
	  var pseudoRandom = new Chance(globalSeed + position), 
	  scene = {},
	  biomIndex = pseudoRandom.next()%4;
	  scene.biom = bioms[biomIndex];
    }
    
Würde man die Auswahl des Biomes dem Pseudozufall überlassen, hätte man am Ende sehr unnatürliche Biom-Kombinationen: Eine Wüste könnte direkt an eine Schneelandschaft grenzen, die wiederum an eine weitere Wüste und diese an einen Sumpf anschließt. In der Realität undenkbar.
Der Pseudozufall muss also durch ein System ersetzt werden, welches das Klima annähernd natürlich simuliert.

