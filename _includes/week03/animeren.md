## Animeren met timers

Animatie in computer graphics wordt gedaan door het scherm steeds opnieuw te tekenen, waarbij objecten steeds een klein beetje veranderen. Door de X-coordinaat van een object op te hogen krijg je een beweging naar rechts. We kunnen dit proces opdelen in twee, van elkaar losstaande delen code; het updaten en het tekenen. Door nu intern variabelen op te slaan met de state van de applicatie, deze aan te passen in de update, en te gebruiken in de paint kunnen we nu animeren. Voor het steeds opnieuw aanroepen van code gebruiken we de [`AnimationTimer`](https://docs.oracle.com/javafx/2/api/javafx/animation/AnimationTimer.html) klasse. Deze kunnen we via de volgende constructie aanmaken:

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

PSM: GOOSSENS: TODO!
In de constructor van de timer geven we aan dat de actionPerformed methode 60x per seconde wordt aangeroepen. De actionPerformed methode bevat dan de code die uitgevoerd moet worden om alle objecten te bewegen en te animeren, waarna de repaint() aangeroepen wordt. De `paint()` stuurt intern in Java een verzoek om het venster opnieuw te tekenen. Java2D zal dan zelf schedulen wanneer de paintComponent aangeroepen gaat worden. Je kunt meerdere keren repaint() aanroepen, maar dit betekent dus niet dat er ook meerdere keren opnieuw getekent wordt. Zorg er daarom dus voor dat de actionPerformed niet te veel zware code bevat, omdat er pas opnieuw getekend wordt zodra de actionPerformed afgerond is.

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