## Blending

Standaard bij het tekenen van vormen en afbeeldingen zal java de nieuwe kleur over de oude kleur heenschrijven. Door de composite rules aan te passen kunnen we instellen hoe de nieuwe kleur over de oude kleur heenvalt. Het is ook mogelijk de twee kleuren te combineren. In de graphics wereld worden hierbij de termen Source en Destination gebruikt. Source is de kleur die je op dat moment aan het tekenen bent en destination is de kleur die al op 't scherm staat. De manieren van combineren staan in de [AlphaComposite](https://docs.oracle.com/javase/8/docs/api/java/awt/AlphaComposite.html) klasse. Via de `AlphaComposite.getInstance()` is het mogelijk om een nieuwe AlphaComposite aan te maken met een van de standaard-regels.

![composite](images/week03/composite.png)

- *CLEAR* : maakt het scherm leeg op de plek waar getekent wordt.
- *SRC_OVER* : zet de nieuwe afbeelding over de oude afbeelding. Maakt hierbij gebruik van het alfakanaal van de nieuwe afbeelding.
- *DST_OVER* : zet de oorspronkelijke afbeelding over de nieuwe afbeelding. Maakt gebruik van het alfakanaal, tekent dus alleen op de plaatsen waar er nog niet getekend is.
- *SRC_IN* : Tekent alleen het gedeelte van de nieuwe afbeelding die op de oude afbeelding ligt.
- *DST_IN* : Vervangt het gedeelte van de destination dat in de source ligt.
- *SRC_OUT* : Het gedeelte van de source dat buiten de destination ligt vervangt de destination.
- *DST_OUT* : Het gedeelte van de destination dat buiten de source ligt vervangt de destination.
- *SRC* : Gebruikt alleen de source en blend niet met de destination.
- *DST* : Gebruikt alleen de destination en doet niets met de source.
- *SRC_ATOP* : Tekent alleen de source over de destination en houd rekening met alpha.
- *DST_ATOP* : Het gedeelte van de destination die over de source valt wordt getekend.
- *XOR* : Tekent alleen op plekken waar of de destination, of de source is, maar niet waar beide tekenen.

Daarnaast is bij sommige composite rules ook een floating point alpha waarde op te geven, deze geeft aan hoeveel geblend moet worden. Door SRC_OVER te nemen met een alpha van 0.5, zal de alpha-waarde van de destinationafbeelding voor iedere pixel met 0.5 vermenigvuldigd worden. Op deze manier kun je afbeeldingen en objecten in laten faden, door deze waarde te animeren van 0 naar 1.

```java
public void draw(FXGraphics2D g2d) {
    AffineTransform tx = new AffineTransform();

    g2d.setComposite(AlphaComposite.getInstance(AlphaComposite.SRC_OVER, 0.5f));
    g2d.fill(new Rectangle2D.Double(100,100,100,100));
}
```

{% include week03/exercise/03-image-fading.md %}
{: .exercises }
