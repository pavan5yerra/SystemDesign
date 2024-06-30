# Design Pattern

Please Read https://refactoring.guru/design-patterns/factory-method

1. Creational Patterns
    1. Factory Pattern
    2. Abstract Factory Pattern
    3. Singleton Pattern
    4. Prototype Pattern
2. Structural patterns
    1. Adapter Pattern
    2. Decorator Pattern
    3. Proxy Pattern
3. Behavioural Patterns
    1. Iterator Pattern
    2. Observer Pattern




# Creational Patterns
**Factory Pattern:**

**Factory Method** is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.



### Key Points:
- **Encapsulation**: Factory pattern encapsulates the object creation logic within the factory class, separating it from the client code.
- **Flexibility**: Easily extendable by adding new subclasses (`Bike` , `Bus` , etc.) and modifying the factory method to support new types of objects.
- **Code Reusability**: Promotes code reusability by centralizing object creation logic, reducing duplicate code in the client.


```java
// Step 1: Define Vehicle interface (Product)
interface Vehicle {
    void start();
}

// Step 2: Concrete classes implementing Vehicle interface
class Car implements Vehicle {
    @Override
    public void start() {
        System.out.println("Car started");
    }
}

class Truck implements Vehicle {
    @Override
    public void start() {
        System.out.println("Truck started");
    }
}

// Step 3: Factory class to create and return instances of vehicles
class VehicleFactory {
    // Factory method to create Vehicle objects
    public Vehicle createVehicle(String type) {
        if (type.equalsIgnoreCase("car")) {
            return new Car();
        } else if (type.equalsIgnoreCase("truck")) {
            return new Truck();
        }
        return null;
    }
}

```
```java
// Step 4: Client code to use the Factory to create objects
public class FactoryPatternDemo {
    public static void main(String[] args) {
        VehicleFactory vehicleFactory = new VehicleFactory();

        // Create a car using the factory
        Vehicle car = vehicleFactory.createVehicle("car");
        car.start();

        // Create a truck using the factory
        Vehicle truck = vehicleFactory.createVehicle("truck");
        truck.start();
    }
}
```




**Abstract Factory Pattern :**

**Abstract Factory** is a creational design pattern that lets you produce families of related objects without specifying their concrete classes.



### Key Points:
- **Flexibility**: Abstract Factory pattern allows the client code (`GUIComponentClient` ) to use different families of related products (`Windows`  or `Mac`  GUI components) interchangeably.
- **Encapsulation**: Concrete factories (`WindowsGUIFactory`  and `MacGUIFactory` ) encapsulate the creation of product objects, providing a centralized way to manage product variants.
- **Scalability**: Easily extendable to support new product families (e.g., adding support for Linux GUI components) by adding new concrete factory implementations without modifying existing client code.


```java

// Abstract product for Chair
interface Chair {
    void sitOn();
}

// Abstract product for Sofa
interface Sofa {
    void lieOn();
}

// Concrete product: ModernChair
class ModernChair implements Chair {
    @Override
    public void sitOn() {
        System.out.println("Sitting on a Modern Chair");
    }
}

// Concrete product: ModernSofa
class ModernSofa implements Sofa {
    @Override
    public void lieOn() {
        System.out.println("Lying on a Modern Sofa");
    }
}

// Concrete product: VictorianChair
class VictorianChair implements Chair {
    @Override
    public void sitOn() {
        System.out.println("Sitting on a Victorian Chair");
    }
}

// Concrete product: VictorianSofa
class VictorianSofa implements Sofa {
    @Override
    public void lieOn() {
        System.out.println("Lying on a Victorian Sofa");
    }
}

// Abstract factory interface
interface FurnitureFactory {
    Chair createChair();
    Sofa createSofa();
}

// Concrete factory: ModernFurnitureFactory
class ModernFurnitureFactory implements FurnitureFactory {
    @Override
    public Chair createChair() {
        return new ModernChair();
    }

    @Override
    public Sofa createSofa() {
        return new ModernSofa();
    }
}

// Concrete factory: VictorianFurnitureFactory
class VictorianFurnitureFactory implements FurnitureFactory {
    @Override
    public Chair createChair() {
        return new VictorianChair();
    }

    @Override
    public Sofa createSofa() {
        return new VictorianSofa();
    }
}

// Factory producer class
class FurnitureShop {
    public static FurnitureFactory getFactory(String type) {
        if (type.equalsIgnoreCase("Modern")) {
            return new ModernFurnitureFactory();
        } else if (type.equalsIgnoreCase("Victorian")) {
            return new VictorianFurnitureFactory();
        }
        return null;
    }
}


```
```java
// Client code to demonstrate Abstract Factory Pattern
public class FurnitureShopSimulator {
    public static void main(String[] args) {
        // Create a Modern furniture factory
        FurnitureFactory modernFactory = FurnitureShop.getFactory("Modern");

        // Create Modern chair and sofa
        Chair modernChair = modernFactory.createChair();
        Sofa modernSofa = modernFactory.createSofa();

        // Use Modern chair and sofa
        modernChair.sitOn();
        modernSofa.lieOn();

        // Create a Victorian furniture factory
        FurnitureFactory victorianFactory = FurnitureShop.getFactory("Victorian");

        // Create Victorian chair and sofa
        Chair victorianChair = victorianFactory.createChair();
        Sofa victorianSofa = victorianFactory.createSofa();

        // Use Victorian chair and sofa
        victorianChair.sitOn();
        victorianSofa.lieOn();
    }
}
```


**Singleton Pattern :**

**Singleton** is a creational design pattern that lets you ensure that a class has only one instance, while providing a global access point to this instance.



### Key Points:
- **Lazy Initialization**: The singleton instance is created only when `getInstance()`  is called for the first time, using lazy initialization. This approach is thread-safe in the context of single-threaded applications but may need synchronization for multi-threaded scenarios.
- **Thread-Safety**: For multi-threaded environments, additional synchronization (like double-checked locking or using `volatile`  keyword) may be necessary to ensure thread safety during instance creation.
- **Usage**: Singleton pattern is useful when you need a single, shared instance of a class throughout your application, such as for configuration settings, logging, caching, etc.


```java
public class Singleton {

    // Private static instance variable
    private static Singleton instance;

    // Private constructor to prevent instantiation from outside
    private Singleton() {
        // Optional: Constructor logic
    }

    // Public static method to get the instance (Singleton pattern)
    public static Singleton getInstance() {
        // Lazy initialization: Create the instance only when needed
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    // Optional: Add some business logic methods
    public void showMessage() {
        System.out.println("Hello, I am a singleton instance!");
    }

    public static void main(String[] args) {
        // Get the singleton instance
        Singleton singleton = Singleton.getInstance();

        // Call a method
        singleton.showMessage();
    }
}
```






**Prototype pattern :**

**Prototype** is a creational design pattern that lets you copy existing objects without making your code dependent on their classes.



### Key Points:
- **Cloning**: Instead of creating objects from scratch, the Prototype pattern allows us to clone existing objects and modify them as needed, reducing the overhead of object creation.
- **Usage**: Useful when object creation is expensive or complex (e.g., involves database operations, network calls) and the application needs multiple instances with similar initial state.
- **Prototype vs. Constructor**: Prototype pattern emphasizes cloning existing objects, while traditional object creation focuses on using constructors to create new objects.
```java
// Prototype interface
interface Prototype {
    Prototype clone();
}

// Concrete prototype: Rectangle
class Rectangle implements Prototype {
    private int width;
    private int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    // Clone method
    @Override
    public Prototype clone() {
        return new Rectangle(width, height);
    }

    // Optional: Getter and Setter methods
    public int getWidth() {
        return width;
    }

    public void setWidth(int width) {
        this.width = width;
    }

    public int getHeight() {
        return height;
    }

    public void setHeight(int height) {
        this.height = height;
    }
}

// Client code to demonstrate Prototype pattern
public class PrototypePatternDemo {
    public static void main(String[] args) {
        // Create an initial prototype object
        Rectangle prototype = new Rectangle(10, 20);

        // Clone the prototype to create a new object
        Rectangle rectangle1 = (Rectangle) prototype.clone();
        System.out.println("Rectangle 1 - Width: " + rectangle1.getWidth() + ", Height: " + rectangle1.getHeight());

        // Modify the cloned object as needed
        rectangle1.setWidth(15);
        System.out.println("Modified Rectangle 1 - Width: " + rectangle1.getWidth() + ", Height: " + rectangle1.getHeight());

        // Clone the prototype again to create another new object
        Rectangle rectangle2 = (Rectangle) prototype.clone();
        System.out.println("Rectangle 2 - Width: " + rectangle2.getWidth() + ", Height: " + rectangle2.getHeight());
    }
}
```
```java
Rectangle 1 - Width: 10, Height: 20
Modified Rectangle 1 - Width: 15, Height: 20
Rectangle 2 - Width: 10, Height: 20
```






# Structural Patterns : 


**Adapter Pattern :**

**The adapter** is a structural design pattern that allows objects with incompatible interfaces to collaborate.

```java
// Step 1: Define an interface for XML data source
interface XMLDataSource {
    String getXMLData(); // Method to fetch XML data
}

// Step 2: Concrete classes implementing XMLDataSource interface
class StockDataSource1 implements XMLDataSource {
    @Override
    public String getXMLData() {
        // Simulate fetching XML data from the first source
        return "<stock_data><symbol>XYZ</symbol><price>100.0</price></stock_data>";
    }
}

class StockDataSource2 implements XMLDataSource {
    @Override
    public String getXMLData() {
        // Simulate fetching XML data from the second source
        return "<stock_data><symbol>ABC</symbol><price>150.0</price></stock_data>";
    }
}

// Step 3: Adapter interface to convert XML to JSON
interface JSONAdapter {
    String getJSONData();
}

// Step 4: Adapter class implementing JSONAdapter and using XMLDataSource
class XMLToJSONAdapter implements JSONAdapter {
    private XMLDataSource xmlDataSource;

    public XMLToJSONAdapter(XMLDataSource xmlDataSource) {
        this.xmlDataSource = xmlDataSource;
    }

    @Override
    public String getJSONData() {
        // Convert XML data to JSON format (simplified conversion for illustration)
        String xmlData = xmlDataSource.getXMLData();
        String jsonData = "<json_data>{\"symbol\":\"XYZ\",\"price\":100.0}</json_data>"; // Simplified conversion
        return jsonData;
    }
}

// Step 5: Client code using the adapters
public class AdapterPatternDemo {
    public static void main(String[] args) {
        // Use adapters to fetch and convert XML data to JSON
        XMLDataSource dataSource1 = new StockDataSource1();
        JSONAdapter adapter1 = new XMLToJSONAdapter(dataSource1);
        String jsonData1 = adapter1.getJSONData();
        System.out.println("Converted JSON Data 1: " + jsonData1);

        XMLDataSource dataSource2 = new StockDataSource2();
        JSONAdapter adapter2 = new XMLToJSONAdapter(dataSource2);
        String jsonData2 = adapter2.getJSONData();
        System.out.println("Converted JSON Data 2: " + jsonData2);
    }
}
```


**Decorator Pattern :**

**A decorator** is a structural design pattern that lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.

### Key Points:
- **Dynamic Extensibility**: Decorator pattern allows adding or modifying behavior of objects dynamically at runtime.
- **Composition**: Decorators use composition to wrap objects and add additional behavior, promoting code reuse and flexibility.
- **Open-Closed Principle**: The pattern supports the Open-Closed Principle by allowing classes to be easily extended with new behavior without modifying existing code.

```java
// Component interface: Beverage
interface Beverage {
    String getDescription();
    double cost();
}

// Concrete Component: Espresso
class Espresso implements Beverage {
    @Override
    public String getDescription() {
        return "Espresso";
    }

    @Override
    public double cost() {
        return 1.99;
    }
}

// Concrete Component: HouseBlend
class HouseBlend implements Beverage {
    @Override
    public String getDescription() {
        return "House Blend Coffee";
    }

    @Override
    public double cost() {
        return 0.89;
    }
}

// Decorator abstract class: CondimentDecorator
abstract class CondimentDecorator implements Beverage {
    protected Beverage beverage;

    public CondimentDecorator(Beverage beverage) {
        this.beverage = beverage;
    }

    public String getDescription() {
        return beverage.getDescription();
    }
}

// Concrete Decorator: Milk
class Milk extends CondimentDecorator {
    public Milk(Beverage beverage) {
        super(beverage);
    }

    @Override
    public String getDescription() {
        return beverage.getDescription() + ", Milk";
    }

    @Override
    public double cost() {
        return beverage.cost() + 0.30;
    }
}

// Concrete Decorator: Mocha
class Mocha extends CondimentDecorator {
    public Mocha(Beverage beverage) {
        super(beverage);
    }

    @Override
    public String getDescription() {
        return beverage.getDescription() + ", Mocha";
    }

    @Override
    public double cost() {
        return beverage.cost() + 0.20;
    }
}

```
```java
// Client code
public class DecoratorPatternDemo {
    public static void main(String[] args) {
        // Order an Espresso with Milk and Mocha
        Beverage espresso = new Espresso();
        System.out.println("Order: " + espresso.getDescription() + " $" + espresso.cost());

        Beverage espressoWithMilk = new Milk(espresso);
        System.out.println("Order: " + espressoWithMilk.getDescription() + " $" + espressoWithMilk.cost());

        Beverage espressoWithMilkAndMocha = new Mocha(espressoWithMilk);
        System.out.println("Order: " + espressoWithMilkAndMocha.getDescription() + " $" + espressoWithMilkAndMocha.cost());

        // Order a HouseBlend with double Mocha
        Beverage houseBlend = new HouseBlend();
        Beverage houseBlendWithDoubleMocha = new Mocha(new Mocha(houseBlend));
        System.out.println("Order: " + houseBlendWithDoubleMocha.getDescription() + " $" + houseBlendWithDoubleMocha.cost());
    }
}
```
```java
Order: Espresso $1.99
Order: Espresso, Milk $2.29
Order: Espresso, Milk, Mocha $2.49
Order: House Blend Coffee, Mocha, Mocha $1.29
```


**Proxy pattern :**

**Proxy** is a structural design pattern that lets you provide a substitute or placeholder for another object. A proxy controls access to the original object, allowing you to perform something either before or after the request gets through to the original object.

### Key Points:
- **Proxy Pattern**: Provides a  placeholder object to control access to the real object (`RealInternet`  in this case).
- **Access Control**: The proxy (`ProxyInternet` ) checks and restricts access to certain server hosts based on predefined rules (`restrictedSites` ).
- **Separation of Concerns**: Proxy allows for separation of the client code (`ProxyPatternDemo` ) from the implementation details of access control (`ProxyInternet` ).
```java
// Subject interface: Image
interface Image {
    void display();
}

// Real Subject: RealImage
class RealImage implements Image {
    private String filename;

    public RealImage(String filename) {
        this.filename = filename;
        loadImageFromDisk();
    }

    private void loadImageFromDisk() {
        System.out.println("Loading image: " + filename);
    }

    @Override
    public void display() {
        System.out.println("Displaying image: " + filename);
    }
}

// Proxy: ProxyImage
class ProxyImage implements Image {
    private RealImage realImage;
    private String filename;

    public ProxyImage(String filename) {
        this.filename = filename;
    }

    @Override
    public void display() {
        if (realImage == null) {
            realImage = new RealImage(filename);
        }
        realImage.display();
    }
}

```
```java
// Client code
public class ProxyPatternDemo {
    public static void main(String[] args) {
        Image image1 = new ProxyImage("image1.jpg");
        Image image2 = new ProxyImage("image2.png");

        // Image 1: Loaded from disk
        image1.display();

        // Image 1: Already loaded, no disk access
        image1.display();

        // Image 2: Loaded from disk
        image2.display();

        // Image 2: Already loaded, no disk access
        image2.display();
    }
}
```
```java
Loading image: image1.jpg
Displaying image: image1.jpg
Displaying image: image1.jpg
Loading image: image2.png
Displaying image: image2.png
Displaying image: image2.png
```

# Behavioral Patterns :


**Iterator pattern :**

**Iterator** is a behavioral design pattern that lets you traverse elements of a collection without exposing its underlying representation (list, stack, tree, etc.).

### Key Points:
- **Flexibility**: JavaScript's iterators can be implemented using generator functions (`*createIterator()` ) or by defining `[Symbol.iterator]()`  methods for objects, providing flexibility in how collections are iterated over.
- **Iterator Protocol**: By adhering to the iterator protocol (`next()`  method returning `{ value, done }` ), JavaScript iterators can seamlessly integrate with language features like `for...of`  loops and spread syntax (`...` ).
- **Customization**: Custom iterators allow control over how elements of a collection are accessed, supporting lazy evaluation, filtering, and transformation of data during iteration.
```
const numbers = [1, 2, 3];

const iterator = numbers[Symbol.iterator]();

let result = iterator.next();

while (!result.done) {
    console.log(result.value); // Output: 1, 2, 3 (printed sequentially)
    result = iterator.next();
}
```




**Observer Pattern :**

**Observer** is a behavioral design pattern that lets you define a subscription mechanism to notify multiple objects about any events that happen to the object they’re observing.



### Key Points:
- **Observer Pattern**: Establishes a one-to-many dependency between objects, ensuring that when one object changes state, all its dependents are notified and updated automatically.
- **Loose Coupling**: Subjects (observable objects) and observers (dependent objects) are loosely coupled, allowing for flexibility and easier maintenance of the code.
- **Event Handling**: In JavaScript, the Observer Pattern is commonly used for event handling and UI updates, where elements (subjects) trigger events and notify registered listeners (observers).
- React reconciliation uses observer pattern



