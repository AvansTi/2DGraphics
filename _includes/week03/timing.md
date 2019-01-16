## Timing

De timer wordt standaard 60x per seconde aangeroepen, maar als de applicatie op een minder sterke PC uitgevoerd wordt, is het mogelijk dat de 60 beelden per seconde niet gehaald wordt. Dit kan ook gebeuren als er een zware berekening op de achtergrond gedaan wordt. Om er voor te zorgen dat alle objecten dan toch even snel blijven bewegen kunnen we gebruik maken van een tijdsmeting.

Door de tijd te meten tussen de huidige update- en de vorige update-aanroep, kunnen we een factor bepalen die we met alle snelheden kunnen vermenigvuldigen. We krijgen dan de volgende code:

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.geom.AffineTransform;
import java.awt.geom.Rectangle2D;

public class HelloAnimation extends JPanel implements ActionListener {
    public static void main(String[] args)
    {
        JFrame frame = new JFrame("Hello Java2D");
        frame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        frame.setMinimumSize(new Dimension(800, 600));
        frame.setExtendedState(frame.getExtendedState() | JFrame.MAXIMIZED_BOTH);
        frame.setContentPane(new HelloAnimation());
        frame.setVisible(true);
    }

    private double angle = 0;
    private long lastTime = System.currentTimeMillis();

    HelloAnimation()
    {
        Timer t = new Timer(1000/15, this);
        t.start();
    }

    public void paintComponent(Graphics g)
    {
        super.paintComponent(g);
        Graphics2D g2d = (Graphics2D)g;

        AffineTransform tx = new AffineTransform();
        tx.translate(getWidth()/2, getHeight()/2);
        tx.rotate(angle);
        tx.translate(200, 0);

        g2d.fill(tx.createTransformedShape(new Rectangle2D.Double(-50,-50,100,100)));
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        long currentTime = System.currentTimeMillis();
        double deltaTime = (currentTime - lastTime) / 1000.0;
        lastTime = currentTime;
        angle+=deltaTime;
        repaint();
    }
}

```
