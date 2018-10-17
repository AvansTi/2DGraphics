>> ### Opgave 1-4. Regenboog
>>
>> Schrijf een applicatie die een regenboog tekent, waar aan de linkerkant van de regenboog rood zit, en de rechterkant ook weer rood, met alle kleuren van het hue-spectrum ertussenin. 
>>
>> Om dit aan te pakken, moet je de coördinaten op de binnenste en de buitenste boog berekenen en hiertussen een lijn tekenen met een bepaalde kleur. Het is niet heel erg als er witte lijnen tussen sommige van de segmenten zitten, doordat je lijnen niet dicht genoeg op elkaar zitten. Om deze punten te berekenen kun je weer gebruik maken van poolcoordinaten en carthesische coördinaten. Je kunt hiervoor de onderstaande code gebruiken. Hierin zijn `radiusBinnen` en `radiusBuiten` de binnen en buitenradius (afmeting) van de regenboog, en `hoek` de hoek in de boog die je wilt berekenen.
>>
>> ```java
>> float x1 = radiusBinnen * Math.cos(hoek);
>> float y1 = radiusBinnen * Math.sin(hoek);
>> float x2 = radiusBuiten * Math.cos(hoek);
>> float y2 = radiusBuiten * Math.sin(hoek);
>> ```
>>
>> Voorbeeldoutput:
>> 
>> ![rainbow](images/week01/rainbow.png)
>>
>{: .exercise}