## Transformeren van shapes

Naast het transformeren van het hele venster, is het ook mogelijk om een shape los te transformeren, en hier een nieuwe shape van te maken. Op deze manier kunnen we gemakkelijk een enkel object verplaatsen, zonder het hele canvas te verplaatsen of de shape zelf aan te passen. Dit is straks erg handig voor het laten animeren van objecten.

Om een complete transformatie voor te stellen kunnen we de AffineTransform klasse gebruiken. Een AffineTransform is een klasse die een (combinatie van) transformaties op kan slaan, en deze ook kan toepassen op vormen en punten. Intern slaat de AffineTransform een matrix op, die we kunnen manipuleren met de verschillende methoden. Voor standaard 2D transformaties wordt een 3x3 matrix gebruikt, maar omdat de onderste rij eigenlijk altijd [0, 0, 1] is, wordt deze weggelaten in de AffineTransform klasse, en slaat deze dus een 3x2 matrix op. Daarom dat je in de verschillende methoden die direct de matrix aanpassen ook maar 6 parameters ziet. Deze matrices kunnen we zelf samenstellen
![Matrices](images/week02/transformmatrices.png)
Deze matrices kun je zelf berekenen en in een AffineTransform zetten door middel van de constructor. Stel dat je een shear wil doen over de X-as met een factor 2 dan kun je de matrix
![matrix](https://latex.codecogs.com/gif.download?%5Cbegin%7Bbmatrix%7D%201%20%26%202%20%26%200%20%5C%5C%200%20%26%201%20%26%200%20%5C%5C%200%20%26%200%20%26%201%20%5Cend%7Bbmatrix%7D) gebruiken. De onderste rij gebruiken we niet, dus we kunnen deze in java invullen met de constructor ```new AffineTransform(1,2,0,0,1,0);```. Om deze nu met elkaar te combineren, kunnen we de volgende code gebruiken:

```java
AffineTransform tx = new AffineTransform();
tx.translate(10,10);
tx.concatenate(new AffineTransform(1,2,0,0,1,0));
tx.scale(0.5, 0.5);
```
In deze code worden 2 AffineTransforms gecombineerd, en worden ze verder aangepast. De `translate`, `rotate` en `scale` methoden werken op een transform door, en worden dus automatisch gecombineerd. Let hierbij ook weer op de volgorde van transformeren.

<!-- _todo:_ matrixvermenigvuldigingen en volgorde-->
Een AffineTransform bevat een matrix, die steeds aangepast wordt. De `translate(x1, y2)` methode maakt bijvoorbeeld de matrix ![matrix](https://latex.codecogs.com/gif.download?%5Cbegin%7Bpmatrix%7D%201%20%26%200%20%26%20x1%20%5C%5C%200%20%26%201%20%26%20y1%20%5Cend%7Bpmatrix%7D). Door deze matrix te vermenigvuldigen met de matrix ![matrix](https://latex.codecogs.com/gif.download?%5Cbegin%7Bpmatrix%7D%201%20%26%200%20%26%20x2%20%5C%5C%200%20%26%201%20%26%20y2%20%5Cend%7Bpmatrix%7D), krijg je de gecombineerde matrix, ![matrix](https://latex.codecogs.com/gif.download?%5Cbegin%7Bpmatrix%7D%201%20%26%200%20%26%20x1+x2%20%5C%5C%200%20%26%201%20%26%20y1+y2%20%5Cend%7Bpmatrix%7D) (ga dit na). Ditzelfde principe werkt ook voor bijvoorbeeld een schaling. Hierij is de volgorde erg belangrijk. Als eerst geschaald wordt, en hierna verplaatst, wordt ook de verplaatsing meegeschaald. We zien dit in de vermenigvuldiging:

![scale1](https://latex.codecogs.com/gif.download?%5Cbegin%7Bpmatrix%7D%201%20%26%200%20%26%20x1%20%5C%5C%200%20%26%201%20%26%20y1%20%5Cend%7Bpmatrix%7D%20%5Ctimes%20%5Cbegin%7Bpmatrix%7D%20s%20%26%200%20%26%200%20%5C%5C%200%20%26%20s%20%26%200%20%5Cend%7Bpmatrix%7D%20%3D%20%5Cbegin%7Bpmatrix%7D%20s%20%26%200%20%26%20x1%20%5C%5C%200%20%26%20s%20%26%20y1%20%5Cend%7Bpmatrix%7D)

![scale2](https://latex.codecogs.com/gif.download?%5Cbegin%7Bpmatrix%7D%20s%20%26%200%20%26%200%20%5C%5C%200%20%26%20s%20%26%200%20%5Cend%7Bpmatrix%7D%20%5Ctimes%20%5Cbegin%7Bpmatrix%7D%201%20%26%200%20%26%20x1%20%5C%5C%200%20%26%201%20%26%20y1%20%5Cend%7Bpmatrix%7D%20%3D%20%5Cbegin%7Bpmatrix%7D%20s%20%26%200%20%26%20s%20%5Ctimes%20x1%20%5C%5C%200%20%26%20s%20%26%20s%20%5Ctimes%20y1%20%5Cend%7Bpmatrix%7D)

Dit kan gebruikt om objecten in een lokaal stelsel op te slaan, en hierna te transformeren naar de juiste positie in de wereld. Hierover meer in het volgende hoofstuk

### Gebruiken van transformaties - Shape transformeren

De AffineTransform heeft ook een [`createTransformedShape()`](https://docs.oracle.com/javase/7/docs/api/java/awt/geom/AffineTransform.html#createTransformedShape(java.awt.Shape)) methode. Hiermee kun je een shape transformeren, om 'm op een andere plek te zetten. Op deze manier kun je dus gemakkeljk een AffineTransform gebruiken om een Shape te verplaatsen zonder de shape aan te passen. Dit doe je met de `createTransformedShape(Shape shape)` methode in de AffineTransform. Op deze manier kun je gemakkelijk ieder object een eigen positie, rotatie en schaal geven, en deze flexibel aanpassen. We krijgen dan dus de volgende code:

```java
class Renderable
{
    private Shape shape;
    private Point2D position;
    private float rotation;
    private float scale;

    public Renderable(Shape shape, Point2D position, float rotation, float scale)
    {
        this.shape = shape;
        this.position = position;
        this.rotation = rotation;
        this.scale = scale;
    }

    public void draw(FXGraphics2D g2d)
    {
        g2d.draw(getTransformedShape());
    }

    public Shape getTransformedShape()
    {
        return getTransform().createTransformedShape(shape);
    }

    public AffineTransform getTransform()
    {
        AffineTransform tx = new AffineTransform();
        tx.translate(position.getX(), position.getY());
        tx.rotate(rotation);
        tx.scale(scale,scale);
        return tx;
    }
}
```

Deze code tekent een object op een bepaalde positie, met een lokale rotatie en schaal. Deze attributen zijn in code gemakkelijk aan te passen, waardoor zo'n object gemakkelijk verplaatst, gedraait of geschaalt kan worden. Let bij het gebruik van deze code erop dat het object waar je een shape van maakt om zijn oorsprong draait, dus gebruik bijvoorbeeld een `new Rectangle(-50,-50,100,100)` voor een blok dat om zijn middelpunt draait. Deze coördinaten noemen we coördinaten in de lokale ruimte, de 'object space'. Om dit object te gebruiken kun je de volgende code gebruiken:

```java
public class HelloRenderable extends Application {

    Stage stage;
    ArrayList<Renderable> renderables = new ArrayList<>();

    @Override
    public void start(Stage primaryStage) throws Exception {
        stage = primaryStage;
        javafx.scene.canvas.Canvas canvas = new Canvas(1920, 1080);
        draw(new FXGraphics2D(canvas.getGraphicsContext2D()));
        primaryStage.setScene(new Scene(new Group(canvas)));
        primaryStage.setTitle("Hello transforms");
        primaryStage.show();
    }

    HelloRenderable()
    {
        renderables.add(new Renderable(new Rectangle2D.Double(-50,-50,100,100), new Point2D.Double(400,400), 0.25f * (float)Math.PI, 0.75f));
        renderables.add(new Renderable(new Rectangle2D.Double(-50,-50,100,100), new Point2D.Double(600,400), -0.25f * (float)Math.PI, 1.75f));
    }

    public void draw(FXGraphics2D g2d) {

        for(Renderable r : renderables)
            r.draw(g2d);

    }
}
```

### Gebruiken van transformaties - Camera

![camera](images/week02/scroll.gif)![camera](images/week02/scroll2.gif)<!--http://prostheticknowledge.tumblr.com/post/118534852886/scroll-back-gaming-study-by-itaykeren-looks-at-the-->

In veel applicaties kunnen we het viewport verplaatsen en in of uitzoomen op een wereld. Denk hierbij aan bijvoorbeeld een applicatie waar een wereld van boven bekeken wordt, of een sidescrolling game. Dit doen we door een transformatie uit te voeren op het gehele venster. Dit kan in Java door middel van de `Graphics2D.setTransform(AffineTransform transform)` methode. Dit werkt op dezelfde manier als dat we in [Les 1](Les1#Transformaties) hebben gedaan, maar nu kunnen we een AffineTransform object meegeven in plaats van losse translate, rotate en scale methoden te gebruiken. We kunnen hiervoor een camera object definiëren die een AffineTransform genereerd

```java
class Camera
{
    private Point2D target;
    private float zoom;
    ...
}
```

We kunnen nu spreken van een aantal verschillende coördinatenstelsels

- Screen Space. Dit zijn de scherm-pixel coordinaten en lopen van 0 tot de hoogte en breedte van het scherm
- World Space. Dit zijn de coordinaten in de wereld. Deze coördinaten kun je bijvoorbeeld uit een bestand inladen om een wereld op te bouwen
- Object Space. Dit zijn de lokale coördinaten. Deze coördinaten zijn relatief ten opzichte van de oorsprong van je object

![spaces](images/week02/spaces.png)

Door nu transformaties op een slimme manier te combineren, kunnen we transformeren van object space naar screen space. We hebben dus een object in model space, dit wordt door een object-transformatie omgezet naar world space, en door de camera-transformatie omgezet naar screen space.

### Gebruiken van transformaties - Inverse

Als een camera gebruikt wordt om het scherm te scrollen, wordt het bepalen van de wereld-coördinaten van een muisklik een stuk lastiger. Er moet rekening gehouden worden met de positie, zoom en eventueel rotatie van de camera. Om dit op te lossen kunnen we de inverse van de cameratransformatie gebruiken. Als we de inverse van de cameratransformatie toepassen op de locatie van de muiscursor, krijgen we de wereld-coördinaten van dat punt. De AffineTransform klasse heeft hier de methode `inverseTransform(Point2D source, Point2D destination)` voor. Deze methode kun je op verschilende manieren gebruiken:

```java
Point2D mousePosition = .....;
Point2D transformed1 = new Point2D.Double();
//manier 1, zet de getransformeerde waarde in een andere variabele
cameraTransform.inverseTransform(mousePosition, transformed1);

//manier 2, door null mee te geven, returned de methode een nieuw point2D
Point2D transformed2 = cameraTransform.inverseTransform(mousePosition, null);

// manier 3, je kunt ook het punt in-place transformeren zonder nieuwe punten aan te maken
cameraTransform.inverseTransform(mousePosition, mousePosition);
```

Door nu de positie van de muis op te vragen (zie [Muisinteractie](#Muisinteractie)), kan gemakkelijk berekend worden welk object aangeklikt is, in combinatie met de transformatie van de camera.

{% include week02/exercise/05-spiegel.md %}
{: .exercises }

