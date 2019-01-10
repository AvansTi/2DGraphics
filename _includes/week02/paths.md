## Paths

Een speciale shape is een Path2D. Een Path is een combinatie van lijnen die gebruikt kunnen worden veel verschillende vormen te maken. De Path klasse wordt geïmplementeerd door de GeneralPath klasse, dus deze kunnen we gebruiken. Een generalpath werkt als een soort pen. Je kunt de pen over het canvas bewegen om zo een vorm te tekenen.

![GeneralPath](images/week02/generalpath.png?right)

```java
public void paintComponent(Graphics g)
{
    super.paintComponent(g);
    Graphics2D g2d = (Graphics2D)g;

    GeneralPath path = new GeneralPath();
    path.moveTo(100, 100);
    path.lineTo(200,100);
    path.lineTo(100,200);
    path.closePath();

    g2d.setColor(Color.green);
    g2d.fill(path);
    g2d.setColor(Color.black);
    g2d.draw(path);
}
```
De GeneralPath klasse heeft de volgende methoden:

- ```moveTo(double x, double y)``` Beweegt de cursor naar positie (x,y) zonder een lijn te tekenen.
- ```lineTo(double x, double y)``` Tekent een lijn van de huidige locatie naar locatie (x,y).
- ```quadTo(double x1, double y1, double x2, double y2)``` Tekent een bezier curve naar (x2,y2) met steunpunt (x1,y1).
- ```curveTo(double x1, double y1, double x2, double y2, double x3, double y3)``` Tekent een bezier curve naar (x3,y3) met steunpunten (x1,y1) en (x2,y2).
- ```closePath()``` Sluit het pad met een rechte lijn naar het beginpunt.

Om een vorm te vullen, moet je deze altijd afsluiten met closePath, anders kan de inkt weglekken en zou het hele scherm gevuld worden.

Het is niet altijd voordehandliggend welk gedeelte van de shape gevuld wordt, zeker als de lijnen van het pad elkaar kruisen. Bekijk de volgende voorbeeldcode met de lijnen die hieruit komen:

![myShape](images/week02/weirdshape.png?right)

```java
myShape = new GeneralPath();
myShape.moveTo(-2f, 0f);
myShape.quadTo(0f, 2f, 2f, 0f);
myShape.quadTo(0f, -2f, -2f, 0f);
myShape.moveTo(-1f, 0.5f);
myShape.lineTo(-1f, -0.5f);
myShape.lineTo(1f, 0.5f);
myShape.lineTo(1f, -0.5f);
myShape.closePath();
```

Als we deze vorm gaan opvullen, krijgen we een probleem, welke onderdelen worden er nu gevuld? In java kunnen we kiezen uit 2 verschillende manieren van vullen:

- even-odd rule

  ![even-odd](images/week02/even-odd.png)

  We trekken een virtuele lijn door de vorm heen, en verhogen een teller op iedere plek waar de lijn door de shape heengaat. Buiten de shape staat de teller op 0. De plaatsen waar de teller even is zijn 'buiten' de vorm, de plaatsen waar de teller oneven is zit 'binnen' de vorm.
- nonzero rule

  ![nonzero](images/week02/nonzero.png)

  We trekken weer een virtuele lijn door de vorm heen. Daarnaast geven we alle lijnen een richting (de richting waarin ze zijn getekent). Als we nu onze virtuele lijn volgen en de rand van de shape kruist van rechts, halen we 1 van de teller af, van links tellen we 1 bij de teller op. De plaatsen waar de teller 0 is zijn buiten de shape, op plaatsen waar de teller iets anders dan 0 is, is binnen de shape.

{% include week02/exercise/01-moon.md %}
{: .exercises }
