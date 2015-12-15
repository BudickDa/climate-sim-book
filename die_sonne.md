# Die Sonne

Das Wetter eines jeden Planeten ist abhängig vom Zentralgestirn, welches er Umkreist. Im Falle der Erde ist das die Sonne. Die Erde umkreist die Sonne annähernd Kreisförmig. An der entferntesten Stell, dem sogenannten Aphel sind das $$152 * 10^9 m$$. Am Perihel, die Position an der die Sonne der Erde am nächsten ist, sind es $$147 * 10^9 m$$.
Die durchschnittlich wirkende Leistung in Form von Strahlung ist von der Entfernung unabhängig. Misst man von einem Satelliten die eintreffende Strahlung erhält man den Durchschnittswert von $$1367 \frac{W}{m^2}$$ (3). 
Die unterschiedlichen Klimazonen sowie das Wechsel der Jahreszeiten liegt an der Neigung der Äquatorebne zur Bahnebene des Orbits. Diese beträgt etwa $$23.4 ^\circ$$. Man spricht hierbei von der Ekliptik.

![Ekiptik: Der Winkel zwischen Äquator und Orbitalebene](Ekliptik.png)

Das Resultat der Ekliptik ist, dass die Sonnenstrahlen schief auf die Erde auftreffen, da vom Boden aus betrachtet die Sonne in Abhängigkeit von Breitengrad und Jahreszeit unterschiedlich hoch am Himmel steht.
Dadurch, dass die Sonnenstrahlen schief auftreffen, wird die Energie aus $$1m^2$$ Sonnenstrahl auf eine größere Fläche am Boden verteilt. Je niedriger die Sonne am Horizon steht, desto geringer ist die Energie pro $$m^2$$.

![Der Höhenwinkel Beta der Sonne beträgt in diesem Beispiel 30 Grad.](Fläche.png)

Im vorliegenden Beispiel beträgt der Winkel der Sonne am Horizont (Höhenwinkel $$\beta$$) 30°.
Mit Hilfe des Sinus kann man die Strahlung pro Quadratmeter am Boden berechnen:

$$ E_{Boden} = E_0 * \sin(\beta)$$<br/>
$$ E_{Boden} = 1367 \frac{W}{m^2}* \sin(30 ^\circ)$$<br/>
$$ E_{Boden} = 683.5\frac{W}{m^2}$$<br/>


## Ekliptik $$\epsilon$$ und die Jahreszeiten

Der Höhenwinkel der Sonne ändert sich über das Jahr. Grund dafür ist, dass während die Erde ihre Bahn um die Sonne dreht sich der Ausrichtung der Erdachse gegenüber der Sonne ändert.

![Die Ausrichtung der Erdachse zur Sonne ändert sich mit jeder Jahreszeit um 45 Grad](Jahreszeit.png)


Man kann die Ekliptik mit einer Formel vom letzten Standardäquinoktium (J2000.0) berechnen: 

$$\epsilon = 23.439° - 0.0000004° * n$$

$$n$$ ist die Anzahl der Tage seit dem letzten Standardäquinoktium.

In JavaScript kann man $$n$$ folgendermaßen berechnen:

    function n(){
      var san = 946728000,//Timestamp des Standardäquinoktikums: 946728000
          secondsOfDay = 86400; //Tag in Sekunden: 60 * 60 *24 = 86400
      return (new Date().getTime() - san) / secondsOfDay;
    }

Neben der Ekliptik ist der Höhenwinkel außerdem abhängig vom Breitengrade $$\Phi$$.

Zusammenfassen lässt sich diese Abhängigkeit mathematisch:

$$\beta = arctan{\frac{cos(\epsilon)*sin(\Phi)}{cos(\Phi)}}$$

Fasst man die bisherigen Erkentnisse zusammen erhält man die folgende Gleichung:

$$E_{Boden} = 1367\frac{W}{m^2}*sin(arctan(\frac{cos((23.439^\circ-0.0000004^\circ)*\frac{t-946728000}{86400})*sin(\Phi)}{cos(\Phi)})$$

Implementiert man die folgende Gleichung in JavaScript ist zu beachten, dass die Winkel in Radian konvertiert werden.

