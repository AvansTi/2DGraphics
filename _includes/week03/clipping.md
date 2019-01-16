## Clipping

[![Clipping](images/week03/clip.gif?thumbright)](images/week03/clipping.png) Het is ook mogelijk om het tekenen op bepaalde gebieden van het scherm uit te zetten, zodat er niet getekent wordt. Dit noemen we clipping. De Graphics2D klasse heeft een ```setClip(Shape shape)``` methode, die een clipping-shape instelt. Als je ```null``` meegeeft als parameter, wordt de clipping uitgezet, en anders kan er alleen binnen de vorm getekend worden die je meegeeft. Dit kun je gebruiken om bijvoorbeeld een spotlight-effect te maken, of een vorm opvullen met andere shapes. Alles dat buiten deze vorm valt zal dus niet getekend worden.

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.MouseEvent;
import java.awt.event.MouseMotionAdapter;
import java.awt.geom.Ellipse2D;
import java.awt.geom.GeneralPath;
import java.awt.geom.Point2D;
import java.util.Random;

public class HelloClip extends JPanel {
    public static void main(String[] args)
    {
        JFrame frame = new JFrame("Hello Java2D");
        frame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        frame.setMinimumSize(new Dimension(800, 600));
        frame.setExtendedState(frame.getExtendedState() | JFrame.MAXIMIZED_BOTH);
        frame.setContentPane(new HelloClip());
        frame.setVisible(true);
    }

    public void paintComponent(Graphics g)
    {
        super.paintComponent(g);
        Graphics2D g2d = (Graphics2D)g;


        Shape shape = new Ellipse2D.Double(getWidth()/2-100, getHeight()/2-100, 200, 200);
        g2d.draw(shape);
        g2d.clip(shape);

        Random r = new Random();
        for(int i = 0; i < 1000; i++) {
            g2d.setPaint(Color.getHSBColor(r.nextFloat(),1,1));
            g2d.drawLine(r.nextInt() % getWidth(), r.nextInt() % getHeight(), r.nextInt() % getWidth(), r.nextInt() % getHeight());
        }

    }
}
```