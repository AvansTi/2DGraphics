## Timing

Niet elke computer kan meer dan 30 frames per seconden. Dit kan ook gebeuren als er een zware berekening op de achtergrond gedaan wordt. Om er voor te zorgen dat alle objecten dan toch even snel blijven bewegen kunnen we gebruik maken een deltatime parameter in de `update` methode.

Door gebruik te maken van een deltatime, die genormaliseerd is om basis van 1 seconden, voorkom je dit probleem. Als de computer waarop het programma afspeelt maar 5 FPS aan kan is de deltatime een stuk groter (0.2) dan wanneer de computer 60 FPS aankan.

```java
public class HelloAnimation extends Application {
    private double angle = 0;
    private Stage stage;

    @Override
    public void start(Stage stage) throws Exception {
        this.stage = stage;
        javafx.scene.canvas.Canvas canvas = new Canvas(1920, 1080);
        FXGraphics2D g2d = new FXGraphics2D(canvas.getGraphicsContext2D());
        draw(g2d);
        stage.setScene(new Scene(new Group(canvas)));
        stage.setTitle("Hello Animation");
        stage.show();

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

    @Override
    private void update(double deltatime) {
        long currentTime = System.currentTimeMillis();
        double deltaTime = (currentTime - lastTime) / 1000.0;
        lastTime = currentTime;
        angle+=deltaTime;
        repaint();
    }
}

```
