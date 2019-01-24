# Parametrische vergelijkingen

Een van de dingen die we met lijnen kunnen maken zijn grafieken en parametrische vergelijkingen. Een simpele grafiek zou bijvoorbeeld kunnen zijn `y = sin(x)`. Deze grafiek kunnen we tekenen door een x-variabele te laten lopen, en hierbij de y-coördinaat te berekenen. Hierna zetten we een puntje op locatie x,y. Het probleem hierbij is echter, dat de waarden voor y tussen -1 en 1 liggen. Hiervoor moeten we dus gaan schalen. Daarnaast is het mooier om de continuïteit van de grafiek te tekenen door lijnen te tekenen tussen het huidige punt en het vorige punt. Hierdoor krijgen we 1 lijn. Hiervoor kunnen we de volgende code gebruiken:

```java
public void draw(FXGraphics2D graphics) {

    graphics.translate(this.canvas.getWidth()/2, this.canvas.getHeight()/2);
    graphics.scale( 50, -50);

    graphics.setColor(Color.red);
    graphics.drawLine(0,0,1000,0);
    graphics.setColor(Color.green);
    graphics.drawLine(0,0,0,1000);
    graphics.setColor(Color.black);

    double resolution = 0.1;
    double lastY = Math.sin(-10);

    for(double x = -10; x < 10; x += resolution)
    {
        float y = (float)Math.sin(x);
        graphics.draw(new Line2D.Double(x, y, x-resolution, lastY));
        lastY = y;
    }
}
```

![probleem](images/week01/scaleproblem.png)

Deze code schaalt het scherm met een factor 50, tekent een assenstelsel, en maakt hierna de grafiek `y = sin(x)`, waarbij x van -10 tot 10 loopt. Bij het uitvoeren van deze code, zien we echter een probleem ontstaan, de lijnen zijn ook opgeschaald en erg dik geworden.  Dit is op 2 manieren op te lossen; door de lijndikte kleiner te maken tot 1/50, of door de schaling niet te doen met de scale methode maar door alleen de coördinaten te vermenigvuldigen met een schalingsfactor. De tweede manier heeft in dit geval de voorkeur. Dit levert de volgende code op:

```java
public void draw(FXGraphics2D graphics) {

    graphics.translate(getWidth()/2, getHeight()/2);
    graphics.scale( 1, -1);

    graphics.setColor(Color.red);
    graphics.drawLine(0,0,1000,0);
    graphics.setColor(Color.green);
    graphics.drawLine(0,0,0,1000);
    graphics.setColor(Color.black);

    double resolution = 0.1;
    double scale = 50.0;
    double lastY = Math.sin(-10);

    for(double x = -10; x < 10; x += resolution)
    {
        float y = (float)Math.sin(x);
        graphics.draw(new Line2D.Double(x*scale, y*scale, (x-resolution)*scale, lastY*scale));
        lastY = y;
    }
}
```

Let hierbij op dat de schaling pas bij het tekenen toegepast wordt, niet al in de berekeningen. Nu krijgen we wel het gewenste resultaat. Het is nu triviaal om de schaal aan te passen, of een andere formule te gebruiken. Let wel op de resolution variabele, deze geeft de tussenstap tussen pixels aan. Als deze te klein is, wordt het tekenen erg langzaam, te groot en de grafiek berekent niet voor iedere pixel een juiste coördinaat

{% include week01/exercise/02-graph.md %}
{% include week01/exercise/03-spiral.md %}
{: .exercises }
