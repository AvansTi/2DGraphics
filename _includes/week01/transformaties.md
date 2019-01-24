## Transformaties

Het standaard coördinatenstelsel in java2D heeft de oorsprong in de linkerbovenhoek van het scherm zitten, waarbij de Y-as naar beneden gaat. Soms is dit echter onhandig met het tekenen, en is het bijvoorbeeld handiger om dit assenstelsel aan te kunnen passen. Dit kan bij computer graphics met 3 verschillende acties.

- **Transleren**

  Transleren ofwel verplaatsen, verplaatst de oorsprong van het coördinatenstelsel. Dit kun je dus bijvoorbeeld gebruiken om de oorsprong op het centrum van het venster te leggen. We kunnen dit doen met de `translate(double x, double y)` methode in het Graphics2D object. Door `g2d.translate(100,100);` uit te voeren, verplaatsen we de oorsprong naar de pixel-coördinaat (100,100) in het venster. Met `g2d.translate(this.canvas.getWidth()/2, this.canvas.getHeight()/2);` kunnen we de hoogte en breedte van het paneel opvragen, en komt de oorsprong in het midden van het venster te liggen.

- **Roteren**

  Rotatie draait het coördinatenstelsel rond de oorsprong, of een ander punt. Dit doen we met de `rotate(double hoek)` methode (deze draait om de oorsprong) of de `rotate(double hoek, double x, double y)` methode (deze draait om een punt). Het is voor deze methoden dus erg belangrijk waar de oorsprong van het coördinatenstelsel ligt.
- **Schalen**

  Schalen vergroot of verkleint het coordinatenstelsel vanuit de oorsprong. Dit doen we met de [`scale(double x, double y)`](https://docs.oracle.com/javase/8/docs/api/java/awt/Graphics2D.html#scale(double,%20double)) methode. De x en y parameters zijn hierbij vermenigvuldigings-schaalfactoren. Een factor 1 zal de coördinaten hetzelfde houden en een factor 2 maakt de wereld 2× zo groot. Een schalingsfactor van 0 zal deze as compleet 'uitzetten' en een factor van -1 zal de as spiegelen.

### Combineren van transformaties

Door verschillende transformaties achter elkaar uit te voeren kunnen we deze transformaties combineren. Hierbij is de volgorde van groot belang. Het is bijvoorbeeld belangrijk om eerst de oorsprong goed te zetten, voordat om de oorsprong gedraaid wordt. Door de wiskunde achter het combineren van deze transformaties (Zie volgende week), staan deze transformaties in de omgedraaide volgorde. Je moet de regels code dus van onder lezen. Om bijvoorbeeld de oorsprong van het coördinatenstelsel in het midden van het venster te zetten en de Y-as om te draaien zodat Y positief omhoog gaat, kunnen we de volgende code gebruiken:

```java
graphics.translate(this.canvas.getWidth()/2, this.canvas.getHeight()/2);
graphics.scale(1,-1);
```
