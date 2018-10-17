# Java2D

Java2D is een verzameling van klassen om binnen java met 2D graphics te werken. Deze API bestaat uit een aantal klassen in de java.awt.graphics namespace, en veel functionaliteiten zijn gemakkelijk te benaderen via de [Graphics2D](https://docs.oracle.com/javase/7/docs/api/java/awt/Graphics2D.html) klasse. Een Graphics2D object slaat intern een aantal attributen op die bepalen hoe getekend gaat worden, zoals welke kleur gebruikt gaat worden. Daarnaast is er een uitgebreide [Shape](https://docs.oracle.com/javase/7/docs/api/java/awt/Shape.html)-library die gebruikt kan worden om verschillende vormen te combineren. Deze lessen gaan dieper in op het gebruik van Java2D, maar er is online natuurlijk [ook veel te vinden](https://docs.oracle.com/javase/tutorial/2d/TOC.html). 

Er wordt gebruik gemaakt van Java2D in combinatie met Swing, maar de concepten die behandeld worden zijn ook gemakkelijk toe te passen binnen JavaFX. Daarnaast zijn deze concepten ook toepasbaar binnen andere omgevingen, zoals de SurfaceView binnen android, of het canvas binnen C#.net

Alle code voor deze week kun je vinden op [github](https://github.com/Borf/2DGraphics_demo/tree/master/Java2D_week1), in het Java2D_week1 project.

# Makkelijk gebruiken

Java2D is te gebruiken 	via een [Graphics2D](https://docs.oracle.com/javase/7/docs/api/java/awt/Graphics2D.html) object. Dit object komt intern uit java en Swing, en kan gebruikt worden om op verschillende dingen te tekenen, zoals een JPanel. Om op een JPanel te tekenen kunnen we de volgende code gebruiken:

```java
public class Java2DDemo extends JPanel
{
    public static void main(String[] args)
    {
        JFrame frame = new JFrame("Java2D");
        frame.setSize(800, 600);
        frame.setContentPane(new Java2DDemo());
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }

    Java2DDemo()
    {
//init
    }

    public void paintComponent(Graphics g)
    {
        super.paintComponent(g);
        Graphics2D g2d = (Graphics2D)g;
//teken
    }
}
```

![helloworld](images/week01/hellojava.png)

Deze code maakt een JFrame aan met een aantal standaard opties en zet hier een nieuw contentpaneel in. Dit contentpaneel is van het type Java2DDemo. Deze klasse override de paintComponent methode in deze methode kan code gezet worden om te tekenen. Door de super.paintComponent aan te roepen wordt de originele tekencode uitgevoerd voor het tekenen van andere componenten en wordt 't scherm leeggemaakt. Na deze methode aanroep kan code toegevoegd worden om eigen vormen te tekenen.
