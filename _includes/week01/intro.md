## Java2D

Java2D is een verzameling van klassen om binnen java met 2D graphics te werken. Deze API bestaat uit een aantal klassen in de java.awt.graphics namespace, en veel functionaliteiten zijn gemakkelijk te benaderen via de [Graphics2D](https://docs.oracle.com/javase/7/docs/api/java/awt/Graphics2D.html) klasse. Een Graphics2D object slaat intern een aantal attributen op die bepalen hoe getekend gaat worden, zoals welke kleur gebruikt gaat worden. Daarnaast is er een uitgebreide [Shape](https://docs.oracle.com/javase/7/docs/api/java/awt/Shape.html)-library die gebruikt kan worden om verschillende vormen te combineren. Deze lessen gaan dieper in op het gebruik van Java2D, maar er is online natuurlijk [ook veel te vinden](https://docs.oracle.com/javase/tutorial/2d/TOC.html).

Er wordt gebruik gemaakt van Java2D in combinatie met JavaFX, maar de concepten die behandeld worden zijn ook gemakkelijk toe te passen binnen JavaFX. Daarnaast zijn deze concepten ook toepasbaar binnen andere omgevingen, zoals de SurfaceView binnen android, of het canvas binnen C#.net

Alle code voor deze week kun je vinden op [github](https://github.com/Borf/2DGraphics_demo/tree/master/Java2D_week1), in het Java2D_week1 project.

## Makkelijk gebruiken

Java2D is te gebruiken via een [Graphics2D](https://docs.oracle.com/javase/7/docs/api/java/awt/Graphics2D.html) object. Dit object komt intern uit java en JavaFX, en kan gebruikt worden om op verschillende dingen te tekenen, zoals een Canvas. Om op een Canvas te tekenen kunnen we de volgende code gebruiken:

```java
public class HelloJava2D extends Application {

    private Canvas canvas;
    @Override
    public void start(Stage primaryStage) throws Exception {
        this.canvas = new Canvas(640, 480);
        draw(new FXGraphics2D(canvas.getGraphicsContext2D()));
        primaryStage.setScene(new Scene(new Group(canvas)));
        primaryStage.setTitle("Hello Java 2D");
        primaryStage.show();
    }

    public void draw(FXGraphics2D graphics) {
        // teken
    }

    public static void main(String[] args) {
        launch(HelloJava2D.class);
    }
}
```

![helloworld](images/week01/hellojava.png)

De bovenstaande code maakt gebruik een standaard JavaFX applicatie implementatie. In plaats van het aanmaken van een component dat we al kennen uit OGP1 zoals `Button`, maken we nu gebruik van een andere soort JavaFX component, namelijk [Canvas](https://docs.oracle.com/javase/8/javafx/api/javafx/scene/canvas/Canvas.html). Voor het omzetten van JavaFX code naar 2D Graphics, wordt er gebruik gemaakt van een externe library namelijk [FXGraphics2D](http://www.jfree.org/fxgraphics2d/). Deze library moet je toevoegen als library in IntelliJ.
De methode draw wordt aangeroepen als de applicatie opstart. In deze methode kunnen alle graphics berekeningen uitgevoerd worden. 
