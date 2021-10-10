# Design Pattern (2021.7.2 - 2021. )

## Strategy Design Pattern：

### 1. The Concepts Behind Design Patterns:

设计模式帮助我们设计灵活的软件。

The Gang of Four 的那本设计模式，是设计模式的起源，一定要看。★

### 2. Introduction:

策略设计模式：用来在运行时决定需要调用哪个类中的方法。

Hirerarchy:

![Class Hierarchy](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Strategy Pattern\Class Hierarchy.png)

他讲的跟 Wikipedia 不大一样（貌似也差不多，哈哈哈），Wikipedia：

<img src="F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Strategy Pattern\Strategy Pattern From Wiki.png" alt="Strategy Pattern From Wiki" style="zoom:200%;" />

### 3. Coding - Score System

ScoreBoardBase.java:

```java
public interface ScoreBoardBase {
    void showScore();
}
```

ScoreBoard.java:

```java
public class ScoreBoard {
    private ScoreBoardBase scoreBoardBase;

    public ScoreBoard(ScoreBoardBase scoreBoardBase) {
        this.scoreBoardBase = scoreBoardBase;
    }

    public void showScore() {
        scoreBoardBase.showScore();
    }
}
```

Balloon.java:

```java
public class Balloon implements ScoreBoardBase {
    @Override
    public void showScore() {
        System.out.println("Balloon: 30 points");
    }
}
```

Clown.java:

```java
public class Clown implements ScoreBoardBase {
    @Override
    public void showScore() {
        System.out.println("Clown: 20 points");
    }
}
```

SquareBalloon.java:

```java
public class SquareBalloon implements ScoreBoardBase {
    @Override
    public void showScore() {
        System.out.println("SquareBalloon: 45 points!");
    }
}
```

Example1Test.java:

```java
public class Example1Test {
    @Test
    public void testScore() {
        ScoreBoard score;
        score = new ScoreBoard(new Balloon());
        score.showScore();
        score = new ScoreBoard(new Clown());
        score.showScore();
        score = new ScoreBoard(new SquareBalloon());
        score.showScore();
    }
}
```

### 4. Payment System:

![Example2](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Strategy Pattern\Payment System.png)

Payment.java:

```java
public interface Payment {
    void pay(String name, double amount);
}
```

ShoppingCart.java:

```java
public class ShoppingCart {
    private List<Product> products = new ArrayList<>();

    public void addProduct(Product product) {
        products.add(product);
    }

    public void removeProduct(Product product) {
        products.remove(product);
    }

    public List<Product> getProducts() {
        return products;
    }

    public void setProducts(List<Product> products) {
        this.products = products;
    }
}
```

Product.java:

```java
public class Product {
    private String name;
    private double price;

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void pay(Payment payment) {
        payment.pay(name, price);
    }
}
```

PaypalPayment.java:

```java
public class PaypalPayment implements Payment {
    @Override
    public void pay(String name, double amount) {
        System.out.println("paid with paypal: " + name + ", " + amount + "$");
    }
}
```

CreditCardPayment.java:

```java
public class CreditCardPayment implements Payment {
    @Override
    public void pay(String name, double amount) {
        System.out.println("paid with credit card: " + name + ", " + amount + "$");
    }
}
```

Example2Test.java:

```java
public class Example2Test {
    @Test
    public void testPayment() {
        ShoppingCart shoppingCart = new ShoppingCart();
        shoppingCart.addProduct(new Product("MacBook pro", 1999));
        shoppingCart.addProduct(new Product("Google Pixel", 999));
        for (Product product : shoppingCart.getProducts()) {
            product.pay(new PaypalPayment());
            product.pay(new CreditCardPayment());
        }
    }
}
```

## Observer Design Pattern

### 1. Intorduction

现实中很常用。

一个总的 Object 与其他 Subscribers (Listener) 建立依赖，一旦这个 Object 发生改变，它的 Subscribers 也自动被通知和发生改变。如：订阅邮箱、电视机或手机接收卫星信号等。

![ObserverPattern](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Observer Pattern\ObserverPattern.png)

wiki:

![Observer Pattern From Wiki](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Observer Pattern\Observer Pattern From Wiki.png)

### 2. Coding

AmericanObserver:

```java
public class AmericanObserver implements Observer {
    private String name = getClass().getSimpleName();

    @Override
    public void update() {
        System.out.println("America got");
    }

    @Override
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

ChineseObserver:

```java
public class ChineseObserver implements Observer {
    private String name = getClass().getSimpleName();

    @Override
    public void update() {
        System.out.println("China got");
    }

    @Override
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

Observer:

```java
public interface Observer {
    void update();
    String getName();
}
```

Subject:

```java
public class Subject {
    private List<Observer> observers = new ArrayList<>();

    public void registerObserver(Observer observer) {
        if (observer == null) {
            throw new NullPointerException("observer is null");
        }
        if (!observers.contains(observer)) {
            observers.add(observer);
            System.out.println(observer.getName() + " registered");
        }
    }

    public void unregisterObserver(Observer observer) {
        observers.remove(observer);
        System.out.println(observer.getName() + " unregistered");
    }

    public void notifyObservers(List<Observer> observers) {
        for (Observer observer : observers) {
            observer.update();
        }
    }

    public List<Observer> getObservers() {
        return observers;
    }

    public void setObservers(List<Observer> observers) {
        this.observers = observers;
    }
}
```

ObserverPatternTest:

```java
public class ObserverPatternTest {
    @Test
    public void testObserverPattern() {
        Subject subject = new Subject();
        ChineseObserver chineseObserver = new ChineseObserver();
        AmericanObserver americanObserver = new AmericanObserver();
        subject.registerObserver(chineseObserver);
        subject.registerObserver(americanObserver);
        subject.notifyObservers(subject.getObservers());
        subject.unregisterObserver(americanObserver);
        subject.notifyObservers(subject.getObservers());
    }
}
```

## Decorator Pattern:

### 1. Introduction:

许多类继承一个类，那么所有继承类都需要实现同一个方法许多次，效率非常低下，于是就有了 Decorator Pattern 。

加入其他新类时，在不改变现有的继承结构下“修饰”类的属性。——https://www.tutorialspoint.com/design_pattern/decorator_pattern.htm![Decorator Pattern From Tutorialspoint](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Decorator Pattern\Decorator Pattern From Tutorialspoint.png)

修饰之后的结果就相当于把新的东西封装在原来的东西上（在原来的基础上包装一层）：

![Decorator Pattern](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Decorator Pattern\Decorator Pattern.png)

### 2. Coding:

IceCream:

```java
public interface IceCream {
    double cost();
}
```

IceCreamDecorator:

```java
public abstract class IceCreamDecorator implements IceCream {
    private IceCream iceCream;

    public IceCreamDecorator(IceCream iceCream) {
        this.iceCream = iceCream;
    }

    @Override
    public double cost() {
        return iceCream.cost();
    }
}
```

BasicIceCream:

```java
public class BasicIceCream implements IceCream {
    public BasicIceCream() {
        System.out.println("Your basic ice cream!");
    }

    @Override
    public double cost() {
        return 0.5;
    }
}
```

MintIceCream:

```java
public class MintIceCream extends IceCreamDecorator {
    public MintIceCream(IceCream iceCream) {
        super(iceCream);
        System.out.println("Adding mint ice cream!");
    }

    @Override
    public double cost() {
        return 2 + super.cost();
    }
}
```

ChocolateIceCream:

```java
public class ChocolateIceCream extends IceCreamDecorator {
    public ChocolateIceCream(IceCream iceCream) {
        super(iceCream);
        System.out.println("Adding chocolate ice cream!");
    }

    @Override
    public double cost() {
        return 1.5 + super.cost();
    }
}
```

VanillaIceCream:

```java
public class VanillaIceCream extends IceCreamDecorator {
    public VanillaIceCream(IceCream iceCream) {
        super(iceCream);
        System.out.println("Adding vanilla ice cream!");
    }

    @Override
    public double cost() {
        return 1.5 + super.cost();
    }
}
```

IceCreamTest:

```java
public class IceCreamTest {
    @Test
    public void testIceCream() {
        IceCream basicIceCream = new BasicIceCream();
        System.out.println("Cost: " + basicIceCream.cost() + "$");
        IceCream vanillaIceCream = new VanillaIceCream(basicIceCream);
        System.out.println("Now cost: " + vanillaIceCream.cost() + "$");
        IceCream chocolateIceCream = new ChocolateIceCream(vanillaIceCream);
        System.out.println("Now cost: " + chocolateIceCream.cost() + "$");
        IceCream mintIceCream = new MintIceCream(chocolateIceCream);
        System.out.println("Now cost: " + mintIceCream.cost() + "$");
    }
}
```

## Factory and Simple Factory Pattern:

### Simple Factory:

#### Introduction:

Simple Factory 不是设计模式，Factory 才是，但是人们说的设计模式通常都是 Simple Factory。

若不使用 Factory，那么若有许多不同种类的 Hamburger，则要使用许多个 if / else 语句，非常繁杂；若使用了，我们只需要传入 type 即可。

![SimpleFactory](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Factory Pattern\SimpleFactory.png)

### Factory:

![Factory Pattern](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Factory Pattern\Factory Pattern.png)

#### Coding:

Hamberger.java:

```java
public abstract class Hamburger {
    private String name;
    private String sauce;
    private String buns;

    protected void prepare() {
        System.out.println("Preparing " + name + "...");
        System.out.println("Adding " + sauce + "...");
        System.out.println("Adding " + buns + "...");
    }

    protected void cook() {
        System.out.println("Cooking...");
    }

    protected void box() {
        System.out.println("Boxing...");
    }

    public String getName() {
        return name;
    }

    protected void setName(String name) {
        this.name = name;
    }

    public String getSauce() {
        return sauce;
    }

    protected void setSauce(String sauce) {
        this.sauce = sauce;
    }

    public String getBuns() {
        return buns;
    }

    protected void setBuns(String buns) {
        this.buns = buns;
    }
}
```

HamburgerStore:

```java
public abstract class HamburgerStore {
    public Hamburger orderHamburger(String type) {
        Hamburger burger;
        burger = createHamburger(type);
        burger.prepare();
        burger.cook();
        burger.box();
        return burger;
    }

    protected abstract Hamburger createHamburger(String type);
}
```

JamHamburgerStore:

```java
public class JamHamburgerStore extends HamburgerStore {
    @Override
    public Hamburger createHamburger(String type) {
        if (type.equalsIgnoreCase("cheese")) {
            return new JamaicanCheeseHamburger();
        } else if (type.equalsIgnoreCase("veggie")) {
            return new JamaicanVeggieHamburger();
        } else {
            return null;
        }
    }
}
```

JamaicanVeggieHamburger:

```java
public class JamaicanVeggieHamburger extends Hamburger {
    public JamaicanVeggieHamburger() {
        super.setName("Jamaican Style Veggie Burger");
        super.setSauce("Spicy Jamaican Sauce");
        super.setBuns("Lettuce Wrap");
    }
}
```

JamaicanCheeseHamburger:

```java
public class JamaicanCheeseHamburger extends Hamburger {
    public JamaicanCheeseHamburger() {
        super.setName("Jamaican Style Cheese Burger");
        super.setSauce("Spicy Jamaican Sauce");
        super.setBuns("Cookie Dough Buns");
    }
}
```

FactoryPatternTest:

```java
public class FactoryPatternTest {
    @Test
    public void testBurgerStore() {
        HamburgerStore hamburgerStore = new JamHamburgerStore();
        Hamburger jamaicanCheeseBurger = hamburgerStore.orderHamburger("cheese");
        System.out.println("Tom's " + jamaicanCheeseBurger.getName() + "!\n");

        Hamburger jamaicanVeggieBurger = hamburgerStore.orderHamburger("veggie");
        System.out.println("Rose's " + jamaicanVeggieBurger.getName() + "!\n");
    }
}
```

## Singleton Pattern:

保证对象只有一个实例。

根据菜鸟教程，有很多种 Singleton 实现代码：

### 1. 懒汉式，线程不安全：

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

### 2. 懒汉式，线程安全：（效率低）

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
    }

    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

### 3. 饿汉式：（比较常用）

```java
public class Singleton {
    private static Singleton instance = new Singleton();

    private Singleton() {
    }

    public static Singleton getInstance() {
        return instance;
    }
}
```

### 4. 双检锁/双重校验锁（DCL，即 double-checked locking）

```java
public class Singleton {
    private static volatile Singleton instance;

    private Singleton() {
    }

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

### 5. 登记式/静态内部类

```java
public class Singleton {
    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    private Singleton() {
    }

    public static Singleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

### 6. 枚举：

```java
public enum Singleton {
    INSTANCE;
    public void whateverMethod() {
    }
}
```

### 经验之谈：

一般情况下，不建议使用第 1 种和第 2 种懒汉方式，建议使用第 3 种饿汉方式。只有在要明确实现 lazy loading 效果时，才会使用第 5 种登记方式。如果涉及到反序列化创建对象时，可以尝试使用第 6 种枚举方式。如果有其他特殊的需求，可以考虑使用第 4 种双检锁方式。

—— https://www.runoob.com/design-pattern/singleton-pattern.html （菜鸟教程）

## Command Pattern:

### Introduction:

就像游戏机一样，有些地方用来接收游戏，有些地方用来控制对游戏选项的移动，还有些地方用来对游戏角色的控制:

![Example](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Command Patter\Example.png)![Command Pattern](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Command Patter\Command Pattern.png)

### Coding:

Command.java:

```java
public interface Command {
    void execute();
}
```

GameBoy.java:

```java
public class GameBoy {
    private Command upCommand;
    private Command leftCommand;

    public GameBoy(Command upCommand, Command leftCommand) {
        this.upCommand = upCommand;
        this.leftCommand = leftCommand;
    }

    public void arrowUp() {
        upCommand.execute();
    }

    public void arrowLeft() {
        leftCommand.execute();
    }
}
```

MarioCharacterReceiver.java:

```java
public class MarioCharacterReceiver {
    private String name;

    public MarioCharacterReceiver(String name) {
        this.name = name;
    }

    public void moveUp() {
        System.out.println(name + " moving up!");
    }

    public void moveLeft() {
        System.out.println(name + " moving left!");
    }
}
```

MarioUpCommand.java:

```java
public class MarioUpCommand implements Command {
    private MarioCharacterReceiver marioCharacter;

    public MarioUpCommand(MarioCharacterReceiver marioCharacter) {
        this.marioCharacter = marioCharacter;
    }

    @Override
    public void execute() {
        marioCharacter.moveUp();
    }
}
```

TomLeftCommand.java:

```java
public class TomLeftCommand implements Command {
    private TomCharacterReceiver tomCharacter;

    public TomLeftCommand(TomCharacterReceiver tomCharacter) {
        this.tomCharacter = tomCharacter;
    }

    @Override
    public void execute() {
        tomCharacter.moveLeft();
    }
}
```

CommandTest.java:

```java
public class CommandTest {
    @Test
    public void testCommandPattern() {
        MarioCharacterReceiver mario = new MarioCharacterReceiver("Mario");
        Command marioUpCommand = new MarioUpCommand(mario);
        Command marioLeftCommand = new MarioLeftCommand(mario);
        GameBoy gameBoy = new GameBoy(marioUpCommand, marioLeftCommand);
        gameBoy.arrowUp();

        TomCharacterReceiver tom = new TomCharacterReceiver("Tom");
        Command tomUpCommand = new TomUpCommand(tom);
        Command tomLeftCommand = new TomLeftCommand(tom);
        GameBoy gameBoy2 = new GameBoy(tomUpCommand, tomLeftCommand);
        gameBoy2.arrowLeft();
    }
}
```

## Adapter Pattern:

### Introduction:

Real-World Example: 插座适配器。![AdapterPattern](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Adapter Pattern\AdapterPattern.png)

### Coding:

LightningPhone.java:

```java
public interface LightningPhone {
    void useLightning();
    void recharge();
}
```

MicroUsbPhone.java:

```java
public interface MicroUsbPhone {
    void useMicroUsb();
    void recharge();
}
```

AndroidPhone.java:

```java
public class AndroidPhone implements MicroUsbPhone {
    private String model;
    private boolean isConnected;

    public AndroidPhone(String model) {
        this.model = model;
    }

    @Override
    public void useMicroUsb() {
        isConnected = true;
        System.out.println("MicroUsb connected!");
    }

    @Override
    public void recharge() {
        if (isConnected) {
            System.out.println(model + " is recharging using MicroUsb");
        } else {
            System.out.println("Connect MicroUsb first");
        }
    }
}
```

IPhone.java:

```java
public class IPhone implements LightningPhone {
    private String model;
    private boolean isConnected;

    public IPhone(String model) {
        this.model = model;
    }

    @Override
    public void useLightning() {
        isConnected = true;
        System.out.println("Lightning connected!");
    }

    @Override
    public void recharge() {
        if (isConnected) {
            System.out.println(model + " is recharging using Lighting");
        } else {
            System.out.println("Connect lightning first");
        }
    }

    public String getModel() {
        return model;
    }

    public void setModel(String model) {
        this.model = model;
    }
}
```

LightningToMicroUsbAdapter.java:

```java
public class LightningToMicroUsbAdapter implements MicroUsbPhone {
    private IPhone iPhone;

    public LightningToMicroUsbAdapter(IPhone iPhone) {
        this.iPhone = iPhone;
    }

    @Override
    public void useMicroUsb() {
        iPhone.useLightning();
        System.out.println("MicroUsb connected!");
    }

    @Override
    public void recharge() {
        System.out.println(iPhone.getModel() + " is recharging using MicroUsb");
    }
}
```

AdapterTest.java:

```java
public class AdapterTest {
    @Test
    public void testAdapter() {
        IPhone iPhone = new IPhone("iPhone 13 Pro");
        AndroidPhone androidPhone = new AndroidPhone("Google pixel 6");
        iPhone.useLightning();
        iPhone.recharge();
        androidPhone.useMicroUsb();
        androidPhone.recharge();

        LightningToMicroUsbAdapter adapter = new LightningToMicroUsbAdapter(iPhone);
        adapter.useMicroUsb();
        adapter.recharge();
    }
}
```

From wiki - https://en.wikipedia.org/wiki/Adapter_pattern

## Facade Pattern:

### Introduction:

比如一台电脑有许多部件：CPU. GPU, Memery, Disk ... ，但是我们使用的时候只需要通过一个用户接口，即可使用，而不需要了解其中的每个部件；开车也是，你只需要知道怎么开，但是不需要知道车的每个部件的内部情况。

### Code:

Computer.java:

```java
public class Computer {
    private CPU cpu;
    private HardDrive hardDrive;
    private Memory memory;

    public Computer() {
        cpu = new CPU();
        hardDrive = new HardDrive();
        memory = new Memory();
    }

    public void startComputer() {
        cpu.freeze();
        memory.load(123, hardDrive.read(654, 2));
        cpu.jump(123);
        cpu.execute();
    }
}
```

CPU.java:

```java
public class CPU {
    public void freeze() {
        System.out.println("Freezing...");
    }

    public void jump(long position) {
        System.out.println("Jumping to position: " + position);
    }

    public void execute() {
        System.out.println("Executing...");
    }
}
```

HardDrive.java:

```java
public class HardDrive {
    public byte[] read(long lba, int size) {
        return new byte[]{'l', 'z'};
    }
}
```

Memery.java:

```java
public class Memory {
    public void load(long position, byte[] data) {
        System.out.println("Loaded data: " + Arrays.toString(data) + ", from: " + position);
    }
}
```

You.java:

```java
public class You {
    public static void main(String[] args) {
        Computer facade = new Computer();
        facade.startComputer();
    }
}
```

## Template Pattern:
