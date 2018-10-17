# Kwaliteit

![quality](/images/week01/quality.png)

Om de kwaliteit van lijnen te verbeteren kan anti-aliasing aangezet worden. [Anti-aliasing](https://nl.wikipedia.org/wiki/Anti-aliasing) is een techniek om kartelranden te voorkomen bij het tekenen van scheve objecten zoals lijnen. Anti-aliasing kan aangezet worden binnen het Graphics2D object en kan ook uitgezet worden indien het niet nodig is. Anti-aliasing zorgt voor een beter ogend resultaat, maar gaat wel ten koste van performance omdat het renderen langzamer gaat.

```java
public void paintComponent(Graphics g)
{
    super.paintComponent(g);
    Graphics2D g2d = (Graphics2D)g;

    g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_OFF);
    g2d.drawLine(10,10,100,100);

    g2d.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
    g2d.drawLine(30,10,130,100);
}
```
