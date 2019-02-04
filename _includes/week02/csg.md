## Areas en Constructive Solid Geometry

Een andere manier van 't maken van vormen is Constructive Solid Geometry. Dit is in het kort het combineren van 2 vormen om een nieuwe vorm te maken. Dit kunnen we doen met 3 operaties:

### Vereniging (add)

![add](images/week02/csg_add.png?left)

Door de vereniging te nemen van 2 vormen, krijg je een nieuwe vorm met een combinatie van beide vormen. Er komt 1 nieuwe vorm uit, en de lijnstukken die tussen de 2 vormen in zitten, vallen weg.

### Verschil (subtract)

![subtract](images/week02/csg_subtract.png?left)

Geeft de eerste vorm, waar de tweede vorm als een hap uitgenomen is. Dit kan gaten opleveren in de vorm. Let op de volgorde van de vormen, het verschil tussen vorm A en B, en B en A is anders.

### Doorsnede (intersect)

![intersect](images/week02/csg_intersect.png?left)

Geeft alleen de ruimte die overlapt in beide vormen.

### Exclusieve of (xor)

![xor](images/week02/csg_xor.png?left)

Geeft alleen de ruimte die of in de een, of in de andere vorm zit, maar niet allebei. Is gelijk aan ```Verschil(Vereniging(A, B), Doorsnede(A, B))```

### Gebruik van CSG

In java werkt CSG door middel van de [Area](https://docs.oracle.com/javase/7/docs/api/java/awt/geom/Area.html) klasse. Deze klasse is ook een Shape, en kan gemaakt worden op basis van een shape in de constructor. Door een bestaande Shape in een Area te encapsuleren kun je dus gemakkelijk CSG operaties hierop toepassen, en het resultaat kun je meteen tekenen.

```java
public void draw(FXGraphics2D g2d) {

    Area a = new Area(new Ellipse2D.Double(0,0,100,100));
    Area b = new Area(new Ellipse2D.Double(50,0,100,100));

    Area added = new Area(a);
    added.add(b);

    Area sub = new Area(a);
    sub.subtract(b);

    Area intersect = new Area(a);
    intersect.intersect(b);

    Area xor = new Area(a);
    xor.exclusiveOr(b);

    g2d.translate(25,25);

    g2d.setColor(Color.lightGray);
    g2d.fill(added);
    g2d.setColor(Color.black);
    g2d.draw(a);
    g2d.draw(b);

    g2d.translate(0,150);
    g2d.setColor(Color.lightGray);
    g2d.fill(sub);
    g2d.setColor(Color.black);
    g2d.draw(a);
    g2d.draw(b);

    g2d.translate(0,150);
    g2d.setColor(Color.lightGray);
    g2d.fill(intersect);
    g2d.setColor(Color.black);
    g2d.draw(a);
    g2d.draw(b);

    g2d.translate(0,150);
    g2d.setColor(Color.lightGray);
    g2d.fill(xor);
    g2d.setColor(Color.black);
    g2d.draw(a);
    g2d.draw(b);
}
```

Het is natuurlijk ook mogelijk om verschillende operaties achter elkaar uit te voeren op een Area, bijvoorbeeld door er een aantal keer verschillende stukjes af te hakken.

Je kunt CSG gebruiken om nieuwe vormen te maken, maar je kunt er nog meer mee doen:

- Overlap detecteren.
- Onwikkelen van grote complexe vormen (levels).

{% include week02/exercise/02-yingyang.md %}
{: .exercises }
