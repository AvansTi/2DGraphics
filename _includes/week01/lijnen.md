# Lijnen

![line](images/week01/line.png)

Java2D werkt met een [Carthesisch Coördinatenstelsel](https://nl.wikipedia.org/wiki/Cartesisch_coördinatenstelsel). In het kort betekent dit dat er gebruik wordt gemaakt van een X- en een Y-as. De oorsprong van het coördinatenstelsel ligt standaard linksboven in het venster, waarbij de Y-as naar beneden loopt. Dit is dus gespiegeld ten opzichte van het wiskundige assenstelsel dat normaal gebruikt wordt om bijvoorbeeld grafieken te tekenen. Standaard is de eenheid een pixel, dit betekent dus dat punt (200,100) 200 pixels naar rechts, en 100 pixels naar beneden ligt ten opzichte van de linkerbovenhoek. Dit is een standaard die in veel grafische APIs gebruikt wordt.

Om een lijn te tekenen kan de ```draw()``` methode in het Graphics2D object gebruikt worden. Deze methode wil een Shape als parameter, een [Line2D](https://docs.oracle.com/javase/7/docs/api/java/awt/geom/Line2D.html) is een voorbeeld van een Shape. De Line2D klasse heeft geen public constructor, we zullen gebruik moeten maken van een van de subklassen van Line2D, zoals [Line2D.Double](https://docs.oracle.com/javase/7/docs/api/java/awt/geom/Line2D.Double.html). Deze kunnen we direct aan de draw methode meegeven, voor de volgende code.

```java
public class HelloLine extends JPanel
{
    public static void main(String[] args)
    {
        JFrame frame = new JFrame("Java2D");
        frame.setSize(800, 600);
        frame.setContentPane(new HelloLine());
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }

    Line2DDemo()
    {
    }

    public void paintComponent(Graphics g)
    {
        super.paintComponent(g);
        Graphics2D g2d = (Graphics2D)g;
        g2d.draw(new Line2D.Double(200, 100,    500, 200));
    }
}
```

Deze code zal een lijn tekenen van de coördinaat (200,100) naar (500,200).


{% include week01/exercise/01-house.md %}
{: .exercises }
