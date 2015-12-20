# Funktionale Programmierung

Wenn man das vorliegende System in seine kleinsten Bestandteile zerlegt, kommt man zu dem Ergebnis, dass es sich um eine komplexe Kombination von mathematischen Funktionen handelt.

Diese lassen sich in zwei Gruppen unterteilen:

##Funktionen, die in der Reihe aufgerufen werden:

mathematische Darstellung:

$$ f_{gesamt}(x) = 9 * (x+5)$$<br/>
kann unterteilt werden in zwei Funktionen:<br/>
$$f_1(x) = x + 5$$<br/>
und<br/>
$$f_2(x) = 9*x$$<br/>
$$ f_{gesamt}(x) = f_2(f_1(x))$$

Als System betrachtet:
![](gesamtsystem.PNG)

Komplexe Systeme können auf diese Weise in einfachste Blöcke zerlegt und aneinandergereiht werden. Man könnte diesen Vorgang auch in JavaScript implementieren:

    function one(x){
      return x + 5;
    }
    function two(x){
        return 9 * x;
    }
    
    function gesamt(x){
        return two(one(x));
    }
    
    //oder eleganter:
    var gesamt = _.compose(one, two);

Man nehme ein Beispiel aus dem Modell:

Um zu ermitteln ob es bewölkt ist, wird die aktuelle Temperatur und Luftfeuchtigkeit benötigt

    function getTemperature(data){
      var e_sun = getSun(); //Sonne ist überall gleich im Modell
      data.temperature = e_sun *  
      return 
      
    }
    function getHumidity(data){
      
    }
    function getClouds(data){
    }