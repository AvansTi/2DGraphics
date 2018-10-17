>> ### Opgave 1-3. Spiraal
>>
>>Schrijf een programma dat een spiraal tekent. Voor een spiraal kun je de formules gebruiken in het [poolcoördinaten-stelsel](https://nl.wikipedia.org/wiki/Poolcoördinaten). Door de formule `Ø = n × r` te gebruiken, krijg je een spiraalfiguur. hierin is n een constante de afstand tussen de spiraal aan te passen, en r de afstand tussen de oorsprong en het punt. Je kunt bijvoorbeeld n = 1 voor nemen. Om hierna van poolcoördinaten naar carthesische te gaan kun je de sinus en cosinus gebruiken:
>>
>> ```math
>> x = r × cos(Ø)
>> y = r × sin(Ø)
>> ```
>> De formule `Ø = n × r` omgeschreven wordt dus
>> ```math
>> x = n × Ø × cos(Ø)
>> y = n × Ø × sin(Ø)
>> ```
>> waarbij n gebruikt kan worden om de dichtheid van de spiraal in te stellen
>>
>{: .exercise}