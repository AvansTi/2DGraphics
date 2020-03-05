>> ### Opgave 2-6. Blokken Slepen
>>
>> Maak een applicatie om blokken te slepen. Let erop dat als je een blokje sleept, het blokje niet verspringt.
>>
>> Om dit programma te maken, kun je het beste een nieuwe klasse maken zoals de Renderable klasse, waarin je de kleur, positie en shape van het blokje opslaat. Deze objecten kun je in de `init()` methode van `BlockDrag`, en in de `draw` methode van `BlockDrag` teken je deze. In de mousePressed, mouseDragged methode deze array te inspecteren en te manipuleren kun je de blokken verplaatsen
>>
>> **Uitdaging:** Voeg een camerasysteem toe. Door met de rechtermuisknop te slepen kun je het complete scherm verslepen, met het scrollwieltje kun je de camera inzoomen en uitzoomen, en met de linker muisknop kun je een blok verslepen. Daarnaast moet het slepen natuurlijk ook werken als de camera verschoven of ingezoomed is. Let erop dat het 't gemakkelijkst is om de camerapositie en zoom los op te slaan, en iedere keer dat getekend wordt de cameraAffineTransform te berekenen.
>>
>> [![Block Dragger](images/week02/blocks.gif)](images/week02/blocks.gif)
>>
>{: .exercise}