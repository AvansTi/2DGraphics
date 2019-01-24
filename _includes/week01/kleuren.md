## Kleuren

De Graphics klasse slaat op met welke kleur getekend gaat worden. Deze kleur kun je veranderen waarna alle opvolgende teken-commandos met deze kleur getekend zullen worden. De kleur kun je aanpassen met de setColor(Color color) methode. Kleuren kunnen op verschillende manieren aangemaakt worden via de [Color](https://docs.oracle.com/javase/8/docs/api/java/awt/Color.html) klasse:
 `new Color(float r, float g, float b)`
  
  Maakt een kleur aan met rood, groen en blauw waarden. De parameters liggen tussen 0 en 1. `new Color(1.0f, 1.0f, 1.0f)` geeft dus een witte kleur.
- `new Color(int r, int g, int b)`

  Maakt een kleur aan met rood, groen en blauw waarden. De parameters liggen tussen 0 en 255.
- `Color.getHSBColor(float hue, float saturation, float brightness)`

  Maakt een kleur aan volgens het HSB model. Met de hue kun je een kleur instellen, de saturation is de kleurverzadiging en de brightness is de helderheid. De parameters liggen tussen 0 en 1, Color.getHSBColor(0.0f, 1.0f, 1.0f) geeft dus rood.
- `Color.BLACK, Color.WHITE, Color.GREEN`

  Kleur-constanten zijn binnen java gedefinieerd als vaste basiskleuren die je gemakkelijk kunt gebruiken. De volledige lijst kun je vinden in [de java documentatie](https://docs.oracle.com/javase/8/docs/api/java/awt/Color.html#black). Let op dat de constanten altijd op twee manieren te benaderen zijn, het kan bijvoorbeeld door Color.BLACK en Color.black. Color.BLACK is later toegevoegd omdat Color.black niet aan de styleguide voldoet.

Door nu een kleur aan te maken en deze in het Graphics2D object te zetten, kun je bijvoorbeeld lijnen tekenen met deze kleur. Door steeds nieuwe kleuren te maken kunnen we verschillende lijnen tekenen met verschillende kleuren:

```java
public class HelloJava2D extends Application {

    private Canvas canvas;
    @Override
    public void start(Stage primaryStage) throws Exception {
        this.canvas = new Canvas(640, 480);
        draw(new FXGraphics2D(canvas.getGraphicsContext2D()));
        primaryStage.setScene(new Scene(new Group(canvas)));
        primaryStage.setTitle("Hello Java 2D");
        primaryStage.show();
    }

    public void draw(FXGraphics2D g) {
        for(int i = 0; i < 500; i++) {
            g2d.setColor(Color.getHSBColor(i/500.0f, 1, 1));
            g2d.drawLine(i, 10, i, 100);
        }
    }

    public static void main(String[] args) {
        launch(HelloJava2D.class);
    }
}
```

Deze code zal dus 500 lijnen tekenen, met ieder een andere kleur op basis van het HSB model. De hue verloopt hierbij van 0° tot 360°, waardoor je het hele kleurenspectrum te zien krijgt.

{% include week01/exercise/04-rainbow.md %}
{: .exercises }
