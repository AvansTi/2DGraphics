>> ### Opgave 4-1. Verlet
>>
>> 1. Bestudeer de verlet engine die in de les is gebouwd
>>
>> 2. Voeg extra modelijkheden toe om punten en distance constraints toe te voegen aan het systeem
>>    - Als gewoon links geklikt wordt voeg een particle toe met 1 constraint
>>    - Als gewoon rechts geklikt wordt, voeg een particle toe met 2 distance constraints.
>>    - Als Ctrl-rechts geklikt wordt, voeg een particle toe met 2 distance constraints met 2 vaste lengtes (bijvoorbeeld 100)
>>    - Als shift-rechts geklikt wordt, voeg een constraint toe tussen de 2 dichtsbijzijnde particles
>>    - Met Ctrl-links geklikt een particle met een StaticConstraint op dat punt
>>
>>    Tip: Het MouseEvent object heeft de methoden `isControlDown()`, `isAltDown()` en `isShiftDown()`. Deze kun je gebruiken om te kijken welke knoppen zijn ingedrukt. Daarnaast kun je kijken welke muisknop ingedrukt is met `getButton()` kijken welke muisknop ingedrukt is.
>> 3. Verkleur de constraints op basis van de kracht die op een constraint staat. De 'kracht' kun je krijgen door het verschil te nemen van de lengte tussen de 2 punten, en de lengte die het zou moeten zijn
>>
>> 4. Maak een nieuwe constraint toe, `RopeConstraint`, die alleen punten dichter naar elkaar zet als de punten te ver weg van elkaar zijn, maar als de punten te dicht bij elkaar zijn niets doet
>>
>> 5. Voeg de mogelijkheid toe om een doek toe te voegen.
>>
>> 6. Zorg ervoor dat de scene opgeslagen en ingeladen kan worden.
>>
>{: .exercise}