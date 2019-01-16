## Afbeeldingen

De [Image](https://docs.oracle.com/javase/7/docs/api/java/awt/Image.html) klasse, is een abstracte klasse om met afbeeldingen te werken. Deze kun je echter niet zomaar aanmaken, omdat deze abstract is. Je kunt een afbeelding op 2 manieren aanmaken, uit een bestand inladen of een nieuwe lege afbeelding maken. Om een afbeelding in te laden vanuit een bestand en te tekenen, kunnen we de volgende code gebruiken:

```java
class HelloImage extends JPanel
{
    private BufferedImage image;
    public HelloImage()
    {
        try {
            image = ImageIO.read(getClass().getResource("/images/test.png"));
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public void paintComponent(Graphics g)
    {
        super.paintComponent(g);
        Graphics2D g2d = (Graphics2D)g;

        AffineTransform tx = new AffineTransform();
        tx.translate(400,400);
        tx.rotate(Math.toRadians(45.0f), image.getWidth()/2, image.getHeight()/2);
        tx.scale(0.75f, 0.75f);
        g2d.drawImage(image, tx, null);
    }
}
```

Op deze manier wordt een afbeelding maar 1x ingeladen (in de constructor), en steeds herbruikt met het tekenen. Let er wederom op dat de directory waar de afbeelding in staat gemarkeerd is als resource root, zoals in les2 is besproken

### SpriteSheets

![SpriteSheet](images/week03/spritesheet.png?right) In games worden veel spritesheets gebruikt om animaties of meerdere gelijksoortige afbeeldingen op te slaan. Dit zijn afbeeldingen met meerdere kleine afbeeldingen erop. Een voordeel is dat je dan gemakkelijk door de afbeeldingen heen kunt lopen met een nummer door ze in een array te zetten. Daarnaast is het met veel graphics APIs sneller om stukjes van afbeeldingen te laten zien dan het tekenen van verschillende afbeeldingen.

Deze afbeeldingen kun je gemakkelijk opknippen in code, doordat alle afbeeldingen even groot zijn. Dit zou je kunnen doen met de volgende code:

```java
private BufferedImage[] tiles;
public HelloImage()
{
    try {
        BufferedImage image = ImageIO.read(getClass().getResource("/images/spritesheet.png"));
        tiles = new BufferedImage[24];
        //knip de afbeelding op in 24 stukjes van 32x32 pixels.
        for(int i = 0; i < 24; i++)
            tiles[i] = image.getSubImage(32 * (i%6), 32 * (i/6), 32, 32);
    } catch (Exception e) {
        e.printStackTrace();
    }

}
```

Sommige spritesheets hebben sprites die niet allemaal even groot zijn en niet op opvolgende plaasten staan. Hier zit dan altijd een extra bestand bij dat geparsed moet worden om de locatie van de sprites te vinden en uit te knippen.
