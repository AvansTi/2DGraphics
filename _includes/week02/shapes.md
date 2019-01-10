## Shapes

Naast het tekenen van lijnen, kunnen we ook allerlei andere vormen tekenen. Al deze vormen erven over van de Shape klasse en kunnen we met dezelfde ```draw``` methode tekenen. In de Java2D library zitten al een aantal klassen die deze shape klasse implementeren.

![shapes](images/week02/shapes.png)

- Line2D
  Tekent een lijnstuk. Dit lijnstuk heeft een beginpunt en eindpunt.
- Rectangle2D
  Tekent een rechthoek. De constructor ```new Rectangle2D.Double(double x, double y, double width, double height)``` kun je gebruiken om een rectangle te maken op een bepaalde positie.
- Ellipse2D
  Tekent een ellipse. Je kunt met de constructor ```new Ellipse2D.Double(double x, double y, double width, double height)``` een ellipse maken. Om een cirkel te tekenen kun je dit ook object gebruiken, met een gelijke breedte en hoogte.
- Arc2D
  Tekent een stuk van een cirkel of een ellipse. Je kunt de constructor ```new Arc2D.Double(double x, double y, double width, double height, double start, double extend, int type)``` gebruiken om een stuk van een ellipse te tekenen. Je kunt de positie aangeven, de grootte en waar begonnen moet worden. Deze hoek begint rechts met 0° en gaat tegen de klok in. Je moet deze hoek in graden opgeven (0° - 360°).
- CubicCurve2D
  Je kunt met de constructor ```CubicCurve2D.Double(double x1, double y1, double ctrlx1, double ctrly1, double ctrlx2, double ctrly2, double x2, double y2)``` een [Bézierkromme](https://nl.wikipedia.org/wiki/Bézierkromme) met 2 steunpunten tekenen. Je geeft een beginpunt op (x1,y1), een eindpunt (x2,y2), en 2 steunpunten. De curve zal door het begin en eindpunt gaan, maar niet door de steunpunten
- QuadCurve2D
  Je kunt met de constructor ```QuadCurve2D.Double(double x1, double y1, double ctrlx, double ctrly, double x2, double y2)``` een [Bézierkromme](https://nl.wikipedia.org/wiki/Bézierkromme) met 1 steunpunt tekenen. Je geeft een beginpunt op (x1,y1), een eindpunt (x2,y2), en 1 steunpunt. De curve zal door het begin en eindpunt gaan, maar niet door het steunpunt
- RoundRectangle2D
  Je kunt met de constructor ```RoundRectangle.Double(double x, double y, double width, double height, double arcwidth, double archeight)``` een rechthoek tekenen met afgeronde hoeken. De arcwidth en archeight geven aan hoe breed en hoog het hoekje moet zijn dat afgerond wordt.

Je kunt deze vormen tekenen met de ```Graphics.draw(Shape shape)``` of de ```Graphics.fill(Shape shape)``` methoden. De draw methode tekent een lijn in de vorm van de Shape die is opgegeven en de fill methode vult de vorm op. Deze lijn of opvulling kun je een kleur geven met de ```setColor``` methode, maar kunnen we ook een andere opvulling geven. Hierover meer in de hoofdstukken over [Strokes](#Strokes) en [Paints](#Paints).

Daarnaast kun je aan shapes nog een aantal vragen stellen. Zo kun je bijvoorbeeld kijken of een punt binnen de shape is met de ```contains(Point2D point)``` methode. Deze methode kun je bijvoorbeeld gebruiken om te kijken of de gebruiker op een vorm heeft geklikt.
Daarnaast kun je ook een bounding-rectangle opvragen met de ```getBounds()``` methode. Dit is de rechthoek die de volledige shape omlijnt.


