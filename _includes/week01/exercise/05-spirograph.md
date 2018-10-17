>> ### Opgave 1-5. Spirograaf
>>
>> ![spirograaf](images/week01/spirograaf.jpg)
>>
>> Een spirograaf is een instrument dat gebruikt kan worden om patronen te tekenen. Het werkt door een tandwiel dat binnen een ander tandwiel draait. Voor meer informatie zie [spirograaf](https://nl.wikipedia.org/wiki/Spirograaf).
>>
>> Maak een java-applicatie om verschillende spirograaf figuren te tekenen. Dit is eigenlijk vergelijkbaar met een parametrische vergelijking.
>>
>> Voor inspiratie, zie ook [nathanfriend.io/inspirograph/](http://nathanfriend.io/inspirograph/). Het gaat dus niet om de animatie, maar alleen om de uiteindelijke figuur. Zorg dat je applicatie configureerbaar is om verschillende (of misschien zelfs willekeurige) figuren te tekenen. Maak ook gebruik van kleuren.
>>
>> Voor het tekenen van de spirograaf kun je gebruik maken van de generieke formules
>>
>> ```math
>> x = a × cos(b × ø) + c × cos(d × ø)
>> y = a × sin(b × ø) + c × cos(d × ø)
>> ```
>>
>> Dit zijn versimpelde formules, op wikipedia staan net iets andere formules, deze kun je ook gebruiken maar zijn iets complexer om te implementeren, maar wel gemakkelijker te configureren. Door de variabelen a,b,c en d aan te passen kun je een andere figuur te maken.
>>
>{: .exercise}