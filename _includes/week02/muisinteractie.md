## Muisinteractie

De muis werkt in Java event-driven, op basis van de EventHandler<> generic interface. Je kunt aan een component (zoals de canvas), een EventHandler koppelen, door middel van de `setOn....` methoden. Om bijvoorbeeld te kijken of er geklikt is, kun je gebruik maken van de `setOnMouseClick` methode. Deze methode accepteert een instantie van een EventHandler interface implementatie, die we ook met een lambda kunnen implementeren. 

Een voorbeeld:

```java
public class HelloMouse extends Application {
	Stage stage;
	@Override
	public void start(Stage primaryStage) throws Exception {
		stage = primaryStage;
		javafx.scene.canvas.Canvas canvas = new Canvas(1920, 1080);
		draw(new FXGraphics2D(canvas.getGraphicsContext2D()));

		canvas.setOnMouseDragged(e ->
		{
			position = new Point2D.Double(e.getX(), e.getY());
			draw(new FXGraphics2D(canvas.getGraphicsContext2D()));
		});

		primaryStage.setScene(new Scene(new Group(canvas)));
		primaryStage.setTitle("Hello Mouse");
		primaryStage.show();
	}
	public Point2D position = new Point2D.Double(100,100);

	public void draw(FXGraphics2D g2d)
	{
		g2d.setBackground(Color.white);
		g2d.clearRect(0,0,1920,1080);
		g2d.setStroke(new BasicStroke(20));
		g2d.draw(new Rectangle2D.Double(position.getX()-50, position.getY()-50, 100, 100));
	}

}
```

Deze code zal een canvas aanmaken met een MouseDragged event listener erop, en zodra gesleept (met de muisknop ingedrukt) wordt, wordt de positie van een rectangle aangepast. 

Van het MouseEvent kunnen een aantal eigenschappen opgevraagd worden. Zo kun je met de ```getX()``` en ```getY()``` opvragen waar de muiscursor is, met ```getClickCount()``` hoevaak er is geklikt (dus om dubbelkliks te detecteren). Met de ```getButton()``` methode kun je opvragen welke knop is ingedrukt. Deze waarde kun je vergelijken met ```MouseButton.PRIMARY```, ```MouseButton.SECONDARY``` of ```MouseButton.MIDDLE```. 
