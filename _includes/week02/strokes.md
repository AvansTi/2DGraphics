## Strokes

De ```Graphics2D.draw()``` methode tekent standaard een simpele lijn. Deze lijn noemen we een '[Stroke](https://docs.oracle.com/javase/7/docs/api/java/awt/Stroke.html)'. De stroke kun je instellen met de [```setStroke(Stroke newStroke)```](https://docs.oracle.com/javase/7/docs/api/java/awt/Graphics2D.html#setStroke(java.awt.Stroke)) methode. Een van de stroke-klassen is de [BasicStroke](https://docs.oracle.com/javase/7/docs/api/java/awt/BasicStroke.html). Met deze stroke kun je de dikte instellen, het soort afrondingen aan het einde van de lijn en hoe de knikken in de lijnstukken getekend worden. Daarnaast kun je ook een streeppatroon instellen. Dit kan allemaal met de ```BasicStroke(float width, int cap, int join, float miterlimit, float[] dash, float dash_phase)``` constructor, maar het is ook mogelijk de laatste opties weg te laten met bijvoorbeeld de ```BasicStroke(float width, int cap, int join)``` constructor. De width geeft de breedte van de lijnen aan. De cap en join geven de eindes en tussenstukken van lijnstukken aan.

![Caps and Joins](images/week02/caps_and_joins.png)

- JOIN_ROUND geeft een afgeronde hoek bij scherpe hoeken.
- JOIN_BEVEL knipt een hoek af bij scherpe hoeken.
- JOIN_MITER laat een scherpe punt bij scherpe hoeken.
- CAP_BUTT geeft geen extra stukken bij het uiteinde van de lijnstukken.
- CAP_SQUARE zet een extra, recht stuk aan het uiteinde van de lijnstukken met als lengte de helft van de breedte.
- CAP_ROUND rond de uiteinden van de lijnstukken af met een cirkel.
  ```java
  Stroke s = new BasicStroke(4.0f,
                             BasicStroke.JOIN_ROUND,
                             BasicStroke.CAP_ROUND);
  ```

Deze waarden zijn integer constanten in de BasicStroke klasse, en kunnen gebruikt worden in de constructor. In het geval van de JOIN_MITER, kun je ook een extra parameter aan de constructor meegeven die de limiet van de miter-join aangeeft. Dit limiet is de diagonale afstand van de miter, dus de afstand tussen de binnenste en buitenste hoek. Standaard staat deze op 10.0f.

![dashes](images/week02/dash.png)
Daarnaast is het ook mogelijk een streep-patroon mee te geven. Deze patronen kun je in een array doorgeven en je kunt een verschuiving aangeven in een parameter. In de array staat de lengte van de gekleurde gebieden en hierna de lengte van de nietgekleurde gebieden. Het is dus eigenlijk altijd een array met een even aantal elementen. Door de verschuiving kun je aangeven waar het patroon begint.
