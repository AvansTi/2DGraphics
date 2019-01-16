## Animeren met timers

Animatie in computer graphics wordt gedaan door het scherm steeds opnieuw te tekenen, waarbij objecten steeds een klein beetje veranderen. Door de X-coordinaat van een object op te hogen krijg je een beweging naar rechts. We kunnen dit proces opdelen in twee, van elkaar losstaande delen code; het updaten en het tekenen. Door nu intern variabelen op te slaan met de state van de applicatie, deze aan te passen in de update, en te gebruiken in de paintComponent kunnen we nu animeren. Voor het steeds opnieuw aanroepen van code gebruiken we de ```javax.swing.Timer``` klasse. Deze kunnen we via de volgende constructie aanmaken:

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

    public HelloAnimation()
    {
        Timer t = new Timer(1000/60, this);
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
        angle+=0.1;
        repaint();
    }
}
```

In de constructor van de timer geven we aan dat de actionPerformed methode 60x per seconde wordt aangeroepen. De actionPerformed methode bevat dan de code die uitgevoerd moet worden om alle objecten te bewegen en te animeren, waarna de repaint() aangeroepen wordt. De ```repaint()``` stuurt intern in Java een verzoek om het venster opnieuw te tekenen. Java2D zal dan zelf schedulen wanneer de paintComponent aangeroepen gaat worden. Je kunt meerdere keren repaint() aanroepen, maar dit betekent dus niet dat er ook meerdere keren opnieuw getekent wordt. Zorg er daarom dus voor dat de actionPerformed niet te veel zware code bevat, omdat er pas opnieuw getekend wordt zodra de actionPerformed afgerond is.

**Let op: de volgende code gaat dus niet werken:**

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

    public HelloAnimation()
    {
        Timer t = new Timer(1000/60, this);
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
        while(true)
        {
            angle+=0.1;
            repaint();
        }
    }
}
```