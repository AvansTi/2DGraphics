## Paints

De `Graphics2D.fill()` methode kan een vorm invullen. Standaard is dit met een enkele kleur, maar dit kun je instellen met de `Graphics2D.setPaint(Paint paint)` methode. Hier kun je een paint object meegeven, dat bepaalt hoe de vorm gevuld wordt.

### Color

De color klasse implementeerd ook het Paint interface en kun je gebruiken om een Shape in een kleur in te kleuren. De kleur kun je aanmaken met alle constructoren van Color, op dezelfde manier als [setColor](week1#Kleuren).

### GradientPaint

![Gradientpaint](images/week02/gradientpaint.png)

Een GradientPaint maak je aan met twee punten en twee kleuren. Java zal dan lineair interpoleren over een lijn die tussen deze twee punten loopt. Je kunt in de constructor ook aangeven of deze gradient cyclisch of asyclisch is. Een cyclische gradient zal zichzelf blijven herhalen na de twee punten en een acyclische gradient blijft dezelfde kleur na deze twee punten.

### LinearGradientPaint

![LinearGradientPaint](images/week02/lineargradientpaint.png)

Een [LinearGradientPaint](https://docs.oracle.com/javase/8/docs/api/java/awt/LinearGradientPaint.html) heeft twee punten en meerdere kleuren. Daarnaast kun je aangeven hoeveel een bepaalde kleur in verhouding gebruikt moet worden. Je kunt hier dus hetzelfde mee als met eenGradientpaint, maar ook meer, door meerdere kleuren toe te voegen. De standaard constructor `LinearGradientPaint(float startX, float startY, float endX, float endY, float[] fractions, Color[] colors)` zal een acyclische gradientpaint maken die van het startpunt tot het eindpunt de kleuren lineair interpoleert, en daarna een constante kleur blijft. De fractions zijn hierbij een lijst met floating point waarden tussen 0 en 1, in oplopende volgorde, die aangeven waar in de gradient de kleur zich bevind. 0 is (startX,startY), 1 is (endX,endY), 0.5 is precies halverwege.

### RadialGradientPaint

![RadialGradientPaint](images/week02/radialgradientpaint.png)

Een RadialGradientPaint is een gradientpaint die in een cirkel vanuit een punt van kleur verloopt. Hierbij kan nog een tweede focuspunt aangegeven worden om het middelpunt te verschuiven. Ook wordt hier een array aan kleuren meegegeven zoals bij een LinearGradientPaint.
Om een RadialGradientPaint te gebruiken kun je de `RadialGradientPaint(Point2D center, float radius, Point2D focus, float[] fractions, Color[] colors, MultipleGradientPaint.CycleMethod cycleMethod)` constructor aanroepen, waar je een centrum, straal en focuspunt kan opgeven, en daarnaast de lijst met kleuren en fractions om de kleuren aan te geven. Ook kun je een cycleMethod opgeven waarmee aangegeven wordt hoe het patroon herhaald wordt.

### TexturePaint

Een TexturePaint maakt gebruik van een afbeelding om een shape op te vullen. Deze afbeelding is in de vorm van een BufferedImage, en wordt herhaald. In de constructor van de TexturePaint moet dus een BufferedImage meegeven worden en ook een Rectangle die aangeeft waar de afbeelding geplaatst moet worden. Om een afbeelding in te laden, kunnen we de ImageIO klasse gebruiken. Let erop dat je deze afbeelding maar 1x inlaad, dus in de constructor van je klasse, en niet bij het tekenen.

```java
Stage stage;
@Override
public void start(Stage primaryStage) throws Exception {
    stage = primaryStage;
    javafx.scene.canvas.Canvas canvas = new Canvas(1920, 1080);
    draw(new FXGraphics2D(canvas.getGraphicsContext2D()));
    primaryStage.setScene(new Scene(new Group(canvas)));
    primaryStage.setTitle("Hello Paths");
    primaryStage.show();
}

public void draw(FXGraphics2D g2d) {
    BufferedImage texture;
    try {
        texture = ImageIO.read(getClass().getResource("/images/texture.jpg"));
    } catch (IOException | IllegalArgumentException e) {
        e.printStackTrace();
    }
    g2d.setPaint(new TexturePaint(texture, new Rectangle2D.Double(0,0,400,400)));
    g2d.fill(new Rectangle2D.Double(0,0,1920, 1080));
}
```

#### Textures inladen in IntelliJ

Deze afbeeldingen kunnen in IntelliJ gezet worden. In IntelliJ kunnen meerdere mappen gemarkeerd worden als resource. Deze mappen worden hierna in het buildproces meegenomen, en worden ook in de .jar files gezet. Het aanmaken van een resource map bestaat uit 2 stappen. Eerst moet een map aangemaakt worden (met de afbeelding erin), en deze kan hierna gemarkeerd worden als resources root.

![IntelliJ](images/week02/intellij_1.png)
![IntelliJ](images/week02/intellij_2.png)

In dit voorbeeld is een map 'resources', met hierin een map 'images'. Door nu de resources map als root te markeren, kunnen we in code alle subfolders openen, relatief ten opzichte van het project. De bovenstaande texture is dus te openen met `ImageIO.read(getClass().getResource("/images/texture.jpg"))`.


{% include week02/exercise/03-kleuren.md %}
{% include week02/exercise/04-gradientpaint.md %}
{: .exercises }

