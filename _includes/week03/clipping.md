## Clipping

[![Clipping](images/week03/clip.gif?thumbright)](images/week03/clipping.png) Het is ook mogelijk om het tekenen op bepaalde gebieden van het scherm uit te zetten, zodat er niet getekent wordt. Dit noemen we clipping. De `FXGraphics2D` klasse heeft een `setClip(Shape shape)` methode, die een clipping-shape instelt. Als je `null` meegeeft als parameter, wordt de clipping uitgezet, en anders kan er alleen binnen de vorm getekend worden die je meegeeft. Dit kun je gebruiken om bijvoorbeeld een spotlight-effect te maken, of een vorm opvullen met andere shapes. Alles dat buiten deze vorm valt zal dus niet getekend worden.

```java
public void draw(FXGraphics2D g2d) {
    Shape shape = new Ellipse2D.Double(stage.getWidth()/2-100, stage.getHeight()/2-100, 200, 200);
    g2d.draw(shape);
    g2d.clip(shape);

    Random r = new Random();
    for(int i = 0; i < 1000; i++) {
        g2d.setPaint(Color.getHSBColor(r.nextFloat(),1,1));
        g2d.drawLine(r.nextInt() % stage.getWidth(), r.nextInt() % stage.getHeight(), r.nextInt() % stage.getWidth(), r.nextInt() % stage.getHeight());
    }
}
```

{% include week03/exercise/04-spotlight.md %}
{: .exercises }