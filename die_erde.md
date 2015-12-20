# Die Erde

Nachdem nun eine Möglichkeit besteht die Sonneneinstrahlung in Abhängigkeit von Zeit und Ort zu ermitteln, sollen im Folgenden die Klimamechanismen auf der Erde ermittelt werden.

Parameter des Systems sollen sein: 
- Temperatur in Celsius
- Luftfeuchtigkeit in %
- Bewölkung ($$true/false$$)
- Regen ($$true/false$$)
- Luftdruck in $$Pa$$
- Windgeschwindigkeit ($$\frac{m}{s}$$)

## Temperatur
Die vorherrschende Temperatur ist von der Sonneneinstrahlung abhängig. Die Strahlungsenergie wird allerdings neben dem Höhenwinkel der Sonne (siehe [Die Sonne](die_sonne.md)) auch von der Bewölkung abhängig.
Trifft ein Sonnenstrahl auf ein Wolke von Wassermolekül gibt es, vereinfacht betrachtet, drei Möglichkeiten
1. Absorption: Der Sonnenstrahl wird komplett absorbiert, seine Energie regt das Molekül zum schwingen an, es wird wärmer (Strahlungsenergie => Wärmeenergie)

2. Reflektion: Der Sonnenstrahl wird reflektiert, er verliert einen Teil seiner Energie (Frequenz ändert sich), das es wird ein wenig wärmer und der Sonnenstrahl wird in eine andere Richtung abgelenkt

3. Verfehlung: Der Sonnenstrahl verfehlt die Moleküle und setzt seinen Weg unverändert fort

Für das Modell bedeutet das folgendes: Wolken reduzieren die Strahlungsenergie der Sonne, heizen sich dabei allerdings auf.
Da es nicht zielführend war einzelne Sonnenstrahlen und Wassermoleküle zu simulieren, wurde hier ein qualitativer Ansatz gewählt. Es wird nur beachtet, ob Wolken vorhanden sind oder nicht. Sind Wolken vorhanden gibt des zwei Parameter: Absorption und Reflektion. Trifft das Sonnenlicht auf eine Wolkenschicht, so wird der Anteil der Absorption und Reflektion abgezogen. Die übriggebliebene Energie wandert weiter nach unten wo sie entweder auf weitere Wolken oder den Boden trifft. Der Anteil der Absorption wird in Wärmeenergie umgerechnet, resultiert also in einem Temperaturanstieg.
Dieser Temperaturanstieg $$\Delta T$$ wird aus einem festgelegtem Parameter $$\_e2t$$ ermittelt, da das Volumen der Wolken nicht bekannt ist. Der reflektierte Anteil wird ignoriert. Er gehört zu jener Energie, die ins Weltall abgestrahlt wird und damit das System verlässt.

Beispiel:
Sei Absorption $$a$$ und Reflektion $$r$$<br/>

$$\Delta T = (E_{Sonne} * a) * \_e2t$$

Die Energie, die im System verbleibt ($$E_{Sonne}^*$$):<br/>
$$E_{Sonne}^* = E_{Sonne} * r$$