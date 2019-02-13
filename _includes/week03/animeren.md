## Animeren met timers

Animatie in computer graphics wordt gedaan door het scherm steeds opnieuw te tekenen, waarbij objecten steeds een klein beetje veranderen. Door de X-coordinaat van een object op te hogen krijg je een beweging naar rechts. We kunnen dit proces opdelen in twee, van elkaar losstaande delen code; het updaten en het tekenen. Door nu intern variabelen op te slaan met de state van de applicatie, deze aan te passen in de update, en te gebruiken in de draw kunnen we nu animeren. Voor het steeds opnieuw aanroepen van code gebruiken we de [`AnimationTimer`](https://docs.oracle.com/javafx/2/api/javafx/animation/AnimationTimer.html) klasse. Deze kunnen we via de volgende constructie aanmaken:

```java
public class HelloAnimation extends Application {

    private Stage stage;
    private double angle = 0.0;


    @Override
    public void start(Stage stage) throws Exception {
        this.stage = stage;
        javafx.scene.canvas.Canvas canvas = new Canvas(1920, 1080);
        FXGraphics2D g2d = new FXGraphics2D(canvas.getGraphicsContext2D());
        draw(g2d);
        stage.setScene(new Scene(new Group(canvas)));
        stage.setTitle("Hello Animation");
        primaryStage.show();

        new AnimationTimer() {
            long last = -1;
            @Override
            public void handle(long now) {
                if(last == -1)
                    last = now;
                update((now - last) / 1000000000.0);
                last = now;
                draw(g2d);
            }
        }.start();
    }

    private void update(double deltaTime) {
        angle+=0.1;
    }

    public void draw(FXGraphics2D g2d) {
        g2d.setBackground(Color.white);
        g2d.clearRect(0,0,1920,1080);
        AffineTransform tx = new AffineTransform();
        tx.translate(1920/2, 1080/2);
        tx.rotate(angle);
        tx.translate(200, 0);
        g2d.fill(tx.createTransformedShape(new Rectangle2D.Double(-50,-50,100,100)));
    }
}
```

De `AnimationTimer` kan aangemaakt worden in de `start` methode. De implementatie van deze methode bevat alles wat nodig is om alle objecten te laten bewegen en animeren. De timer zal dus steeds twee methodes aanroepen, namelijk de `update` en `draw` methode. De `draw` method wordt ook aangeroepen wanneer je bijvoorbeeld het scherm schaalt. De `update` methode zorgt ervoor dat de state van alle objecten word aangepast, afhankelijk van de update snelheid. De `draw` methode is alleen verantwoordelijk voor het tekenen van alle objecten. Het is belangrijk dat de `update` methode niet te lang duurt!

**Let op: de volgende code gaat dus niet werken:**

```java
public class HelloAnimation extends Application {

    private Stage stage;
    private double angle = 0;
    @Override
    public void start(Stage primaryStage) throws Exception {
        stage = primaryStage;
        Canvas canvas = new Canvas(1920, 1080);
        FXGraphics2D g2d = new FXGraphics2D(canvas.getGraphicsContext2D());
        draw(g2d);
        primaryStage.setScene(new Scene(new Group(canvas)));
        primaryStage.setTitle("Hello Animation");
        primaryStage.show();

        new AnimationTimer() {
            long last = -1;
            @Override
            public void handle(long now) {
                if(last == -1)
                    last = now;
                update((now - last) / 1000000000.0);
                last = now;
                draw(g2d);
            }
        }.start();
    }

    public void draw(FXGraphics2D g2d) {
        AffineTransform tx = new AffineTransform();
        tx.translate(getWidth()/2, getHeight()/2);
        tx.rotate(angle);
        tx.translate(200, 0);

        g2d.fill(tx.createTransformedShape(new Rectangle2D.Double(-50,-50,100,100)));
    }

    private void update(double deltaTime) {
        while(true) {
            angle+=0.1;
        }
    }
}
```

We hebben nu dus 2 losse methoden om te implementeren, een `draw` en een `update` methode. Om je programma overzichtelijk te houden, is het belangrijk om deze 2 methoden hun eigen doel te geven. De `draw` methode tekent alleen, en past **geen** variabelen aan. De `update` methode tekent niets op 't scherm, maar veranderd alleen variabelen. Om tussen deze methoden te communiceren, zul je dus gebruik moeten maken van attributen om te communiceren tussen deze 2 methoden, en om de *state* van je applicatie op te slaan. Het is verstandig deze state op te splitsen in klassen, indien nodig. Stel dat je een applicatie wilt maken met een bewegende bal. Je kunt hiervoor een bal-klasse introduceren, waar ook de teken en update code gesplitst zijn

```java
public class Ball
{
    private Point2D position;
    private Point2D speed;

    public Ball(Point2D position)
    {
        this.position = position;
        this.speed = new Point2D.Double(Math.random()*10-5, Math.random()*10-5);
    }

    public void update()
    {
        this.position = new Point2D.Double(this.position.getX() + this.speed.getX(), this.position.getY() + this.speed.getY());
    }

    public void draw(FXGraphics2D graphics)
    {
        graphics.draw(new Ellipse2D.Double(this.position.getX()-5, this.position.getY()-5, 10, 10));
    }
}
```

Hierna kunnen we deze bal gebruiken:
```java

public class HelloAnimation extends Application {
    private Ball ball;

    @Override
    public void start(Stage stage) throws Exception {
        init();
        javafx.scene.canvas.Canvas canvas = new Canvas(1920, 1080);
        FXGraphics2D g2d = new FXGraphics2D(canvas.getGraphicsContext2D());
        stage.setScene(new Scene(new Group(canvas)));
        stage.setTitle("Hello Animation");
        primaryStage.show();

        new AnimationTimer() {
            long last = -1;
            @Override
            public void handle(long now) {
                if(last == -1)
                    last = now;
                update((now - last) / 1000000000.0);
                last = now;
                draw(g2d);
            }
        }.start();
    }
    private void init()
    {
        ball = new Ball(new Point2D.Double(100,100));
    }

    private void update(double deltaTime) {
        ball.update();
    }

    public void draw(FXGraphics2D g2d) {
        g2d.setBackground(Color.white);
        g2d.clearRect(0,0,1920,1080);
        ball.draw(g2d);
    }
}
```

Deze bal klasse kunnen we ook herbruiken, door ze bijvoorbeeld in een ArrayList op te slaan. Daarnaast zouden we hier ook een generiek gameobject van kunnen maken, waarbij verschillende objecten in een game deze klasse extenden om eenzelfde gedrag te vertonen
