## Muisinteractie

De muis werkt in Java event-driven, op basis van de MouseListener, MouseMotionListener en MouseWheelListener interfaces. Deze interfaces bevatten methoden die aangeroepen worden op 't moment dat er iets gebeurt met de muis. Deze listener kan hierna met de ```addMouseListener()```, ```addMouseMotionListener()``` of ```addMouseWheelListener()``` methoden van het JPanel toegevoegd worden. Het is ook mogelijk om meerdere mouselisteners te hebben op een paneel, maar dit is af te raden als je een enkele applicatie hebt, omdat er dan ongewenst dingen dubbel kunnen gebeuren met de muis, de communicatie tussen verschillende mouselisteners is namelijk lastig. Een voorbeeld:

```java
public class HelloMouse extends JPanel implements MouseListener, MouseMotionListener {
    public static void main(String[] args)
    {
        JFrame frame = new JFrame("Hello Java2D");
        frame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        frame.setMinimumSize(new Dimension(800, 600));
        frame.setExtendedState(frame.getExtendedState() | JFrame.MAXIMIZED_BOTH);
        frame.setContentPane(new HelloMouse());
        frame.setVisible(true);
    }

    HelloMouse()
    {
        addMouseListener(this);
        addMouseMotionListener(this);
    }

    public Point2D position = new Point2D.Double(100,100);

    public void paintComponent(Graphics g)
    {
        super.paintComponent(g);
        Graphics2D g2d = (Graphics2D)g;
        g2d.setStroke(new BasicStroke(20));
        g2d.draw(new Rectangle2D.Double(position.getX()-50, position.getY()-50, 100, 100));
    }

    public void mouseClicked(MouseEvent e) {}
    public void mousePressed(MouseEvent e) {}
    public void mouseReleased(MouseEvent e) {}
    public void mouseEntered(MouseEvent e) {}
    public void mouseExited(MouseEvent e) {}

    public void mouseDragged(MouseEvent e) {
        position = e.getPoint();
        repaint();
    }

    public void mouseMoved(MouseEvent e) {}
}
```

Deze code zal een paneel aanmaken met een MouseListener en MouseMotionlistener erop, en zodra gesleept wordt, wordt de positie van een rectangle aangepast. De mouseDragged methode wordt automatisch aangeroepen zodra de muis gesleept wordt (met een muisknop ingedrukt).

Van het MouseEvent kunnen een aantal eigenschappen opgevraagd worden. Zo kun je met de ```getPoint()``` opvragen waar de muiscursor is, met ```getClickCount()``` hoevaak er is geklikt (dus om dubbelkliks te detecteren). Met de ```getButton()``` methode kun je opvragen welke knop is ingedrukt. Deze waarde kun je vergelijken met ```MouseEvent.BUTTON1```, ```MouseEvent.BUTTON2``` of ```MouseEvent.BUTTON3```. Dit gaat echter alleen bij de mouseClicked, mousePressed en mouseReleased methoden. Een methode die wel voor alle MouseEvents werkt, zijn de ```SwingUtilities.isLeftMouseButton(MouseEvent event)```, ```SwingUtilities.isMiddleMouseButton(MouseEvent event)``` en ```SwingUtilities.isRightMouseButton(MouseEvent event)``` methoden. Deze statische methoden in de SwingUtilities klasse houden ook rekening met het slepen en andere modifiers.
