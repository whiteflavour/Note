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

### Introduction:

定义模板，很好理解，跟 C++ 中的 Template 和 Java 的 interface 有点类似的感觉。

### Code：

Game.java:

```java
public abstract class Game {
    abstract void initialize();
    abstract void startPlay();
    abstract void endPlay();

    public final void play() {
        initialize();
        startPlay();
        endPlay();
    }
}
```

Cricket.java:

```java
public class Cricket extends Game {
    @Override
    void initialize() {
        System.out.println("Initializing cricket game...");
    }

    @Override
    void startPlay() {
        System.out.println("Starting cricket game ...");
    }

    @Override
    void endPlay() {
        System.out.println("Ending cricket game...");
    }
}
```

Football.java:

```java
public class FootballGame extends Game {
    @Override
    void initialize() {
        System.out.println("Initializing football game...");
    }

    @Override
    void startPlay() {
        System.out.println("Starting football game ...");
    }

    @Override
    void endPlay() {
        System.out.println("Ending football game...");
    }
}
```

GameTest.java:

```java
public class GameTest {
    @Test
    public void testGame() {
        Game football = new FootballGame();
        football.play();
        System.out.println();
        Game cricket = new Cricket();
        cricket.play();
    }
}
```

## Iterator Pattern:

### Introduction:

若没有迭代器，我们需要对不同的对象（如：ArrayList 和 普通的数组 ）都使用 for 循环。for 循环内其内容是大致相同的，这就导致代码可读性下降。

![Iterator Pattern](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Iterator Pattern\Iterator Pattern.png)

### Code:

Container.java:

```java
public interface Container {
    Iterator getIterator();
}
```

Iterator.java:

```java
public interface Iterator {
    boolean hasNext();
    Object next();
}
```

NameRepository.java:

```java
public class NameRepository implements Container {
    public String[] names = {"Tom", "Jack", "Rose", "Jerry"};

    @Override
    public Iterator getIterator() {
        return new NameRepositoryIterator();
    }

    private class NameRepositoryIterator implements Iterator {
        private int index;

        @Override
        public boolean hasNext() {
            return index < names.length;
        }

        @Override
        public Object next() {
            if (this.hasNext()) {
                return names[index++];
            }
            return null;
        }
    }
}
```

IteratorPatternTest.java:

```java
public class IteratorPatternTest {
    @Test
    public void testIteratorPattern() {
        NameRepository nameRepository = new NameRepository();
        Iterator iterator = nameRepository.getIterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

From: https://www.tutorialspoint.com/design_pattern/iterator_pattern.htm （发现菜鸟教程是抄的这个网站，哈哈，应该把，不知道是谁抄谁）

## State Pattern:

### Introduction:

能在各个状态 (State) 之间进行转换，并且进行封装。

![State Pattern From Wiki](/Users/fuck/Documents/Note/IT/Platforms/Udemy/Design Pattern/Pictures/State Pattern/State Pattern From Wiki.png)

### Code: (From Wiki)

State.java:

```java
public interface State {
    void writeName(String name, StateContext context);
}
```

LowerCaseState.java:

```java
public class LowerCaseState implements State {
    @Override
    public void writeName(String name, StateContext context) {
        System.out.println(name.toLowerCase());
        context.setState(new MultipleUpperCaseState());
    }
}
```

MultipleUpperCaseState.java:

```java
public class MultipleUpperCaseState implements State {
    private int counter = 0;

    @Override
    public void writeName(String name, StateContext context) {
        System.out.println(name.toUpperCase());
        if (++counter > 1) {
            context.setState(new LowerCaseState());
        }
    }
}
```

StateContext.java:

```java
public class StateContext {
    private State state;

    public StateContext() {
        state = new LowerCaseState();
    }

    public void setState(State state) {
        this.state = state;
    }

    public void writeName(String name) {
        state.writeName(name, this);
    }
}
```

StatePatternTest.java:

```java
public class StatePatternTest {
    @Test
    public void testStatePattern() {
        StateContext context = new StateContext();
        context.writeName("Monday");
        context.writeName("Tuesday");
        context.writeName("Wednesday");
        context.writeName("Thursday");
        context.writeName("Friday");
        context.writeName("Saturday");
        context.writeName("Sunday");
    }
}
```

## Proxy Pattern

### Introduction:

请求一个中间人(middleman)，代替我们去访问。（如：我们取钱本来要直接去银行，但是有了信用卡，我们就可以通过 ATM 机取钱，代替我们向银行访问。

### 三种 Proxy：

1. 代理访问远程目标 -> Remote Proxy
2. 访问复杂目标（不好创建）-> Virtural Proxy
3. 安全 -> Protection Proxy

![ProxyPattern](/Users/fuck/Documents/Note/IT/Platforms/Udemy/Design Pattern/Pictures/Proxy Pattern/ProxyPattern.png)

### Code:

Bank.java:

```java
public interface Bank {
    void withdrawMoney();
}
```

ProxyBank.java:

```java
public class ProxyBank implements Bank {
    private Bank bank;

    public ProxyBank() {
        bank = new RealBank();
    }

    @Override
    public void withdrawMoney() {
        System.out.println("Withdraw money from ATM...");
        bank.withdrawMoney();
    }
}
```

RealBank.java:

```java
public class RealBank implements Bank {
    @Override
    public void withdrawMoney() {
        System.out.println("Withdraw money from real bank...");
    }
}
```

ProxyPatternTest.java:

```java
public class ProxyPatternTest {
    @Test
    public void testProxyBank() {
        Bank proxyBank = new ProxyBank();
        proxyBank.withdrawMoney();
        System.out.println();
        Bank realBank = new RealBank();
        realBank.withdrawMoney();
    }
}
```

## MVC Pattern:

### Introduction:

在 MVC Pattern 中也可能使用其他的设计模式，这些设计模式并不是独立的，而是跟据使用场景配合使用的。

### Code：

Student.java:

```java
public class Student {
    private String rollNo;
    private String name;

    public Student(String rollNo, String name) {
        this.rollNo = rollNo;
        this.name = name;
    }

    public String getRollNo() {
        return rollNo;
    }

    public void setRollNo(String rollNo) {
        this.rollNo = rollNo;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

StudentView.java:

```java
public class StudentView {
    public void printStudentDetails(Student student) {
        System.out.println("Roll NO: " + student.getRollNo());
        System.out.println("Name: " + student.getName());
    }
}
```

StudentController.java:

```java
public class StudentController {
    private Student student;
    private StudentView studentView;

    public StudentController(Student student, StudentView studentView) {
        this.student = student;
        this.studentView = studentView;
    }

    public String getStudentName() {
        return student.getName();
    }

    public void setStudentName(String name) {
        student.setName(name);
    }

    public String getStudentRollNo() {
        return student.getRollNo();
    }

    public void setStudentRollNo(String rollNo) {
        student.setRollNo(rollNo);
    }

    public void updateView() {
        studentView.printStudentDetails(student);
    }
}
```

MVCPattern.java:

```java
public class MVCPatternDemo {
    public static void main(String[] args) {
        Student model = retrieveStudentFromDatabase();
        StudentView view = new StudentView();
        StudentController controller = new StudentController(model, view);

        controller.updateView();
        controller.setStudentName("Tom");
        controller.updateView();
    }

    public static Student retrieveStudentFromDatabase() {
        return new Student("1", "Rose");
    }
}
```

## Builder Pattern:

### Introduction:

我们可以像平时那样使用 Constructor 来构造对象，但是如果对象的属性比饺多，就很混乱，于是我们可以使用 Builder Pattern，使用之后，我们就可以一步一步来构造对象，填充对象的属性，就像 JDK 中的 StringBuilder 一样。

JDK 中的 StringBuilder 就使用了 Builder Pattern:

```java
StringBuilder sb = new StringBuilder();

sb.append().append();
	.append();

...
```

### Code：

我们可以直接在对象类中使用内部类来进行，更好的方式是将其封装在 Interface 中。★

From wiki and Paulo Dichone in Udemy:

Pizza.java:

```java
/**
 * Product
 */
public class Pizza {
    private String dough;
    private String sauce;
    private String topping;

    public void setDough(String dough) {
        this.dough = dough;
    }

    public void setSauce(String sauce) {
        this.sauce = sauce;
    }

    public void setTopping(String topping) {
        this.topping = topping;
    }

    @Override
    public String toString() {
        return "Pizza{" +
                "dough='" + dough + '\'' +
                ", sauce='" + sauce + '\'' +
                ", topping='" + topping + '\'' +
                '}';
    }
}
```

PizzaBuilder.java:

```java
/**
 * Abstract Builder
 */
public abstract class PizzaBuilder {
    private Pizza pizza;

    public Pizza getPizza() {
        return pizza;
    }

    public PizzaBuilder createNewPizzaProduct() {
        pizza = new Pizza();
        return this;
    }

    public abstract PizzaBuilder buildDough();
    public abstract PizzaBuilder buildSauce();
    public abstract PizzaBuilder buildTopping();
}
```

HawaiianPizzaBuilder.java:

```java
/**
 * Concrete Builder
 */
public class HawaiianPizzaBuilder extends PizzaBuilder {
    @Override
    public PizzaBuilder buildDough() {
        getPizza().setDough("cross");
        return this;
    }

    @Override
    public PizzaBuilder buildSauce() {
        getPizza().setSauce("mild");
        return this;
    }

    @Override
    public PizzaBuilder buildTopping() {
        getPizza().setTopping("ham + pineapple");
        return this;
    }
}
```

SpicyPizzaBuilder.java:

```java
/**
 * Concrete Builder
 */
public class SpicyPizzaBuilder extends PizzaBuilder {
    @Override
    public PizzaBuilder buildDough() {
        getPizza().setDough("pan baked");

        // 这样就可以使用链式调用
        return this;
    }

    @Override
    public PizzaBuilder buildSauce() {
        getPizza().setSauce("hot");
        return this;
    }

    @Override
    public PizzaBuilder buildTopping() {
        getPizza().setTopping("pepperoni + salami");
        return this;
    }
}
```

Waiter.java:

```java
/**
 * Director
 */
public class Waiter {
    private PizzaBuilder pizzaBuilder;

    public void setPizzaBuilder(PizzaBuilder pizzaBuilder) {
        this.pizzaBuilder = pizzaBuilder;
    }

    public Pizza getPizza() {
        return pizzaBuilder.getPizza();
    }

    public void constructPizza() {
        pizzaBuilder.createNewPizzaProduct()
                    .buildSauce()
                    .buildDough()
                    .buildTopping();
    }
}
```

OrderingPizza.java:

```java
public class OrderingPizza {
    public static void main(String[] args) {
        PizzaBuilder hawaiianPizzaBuilder = new HawaiianPizzaBuilder();
        PizzaBuilder spicyPizzaBuilder = new SpicyPizzaBuilder();

        Waiter waiter = new Waiter();
        waiter.setPizzaBuilder(spicyPizzaBuilder);
        waiter.constructPizza();

        Pizza pizza = waiter.getPizza();
        System.out.println(pizza);
    }
}
```

## Prototype Pattern:

### Introduction:

克隆对象。

### Code:

**注：**

方法1和2的主要区别就是实现类的`clone()`方法。

#### 1. 不使用`Cloneable`接口：

Prototype.java:

```java
public interface Prototype {
    Prototype clone();
}
```

Person.java:

```java
public class Person implements Prototype {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public Prototype clone() {
        return new Person(name, age);
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

Dolphin.java:

```java
public class Dolphin implements Prototype {
    private String name;
    private int age;

    public Dolphin(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public Prototype clone() {
        return new Dolphin(name, age);
    }

    @Override
    public String toString() {
        return "Dolphin{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

CloneTest.java:

```java
public class CloneTest {
    @Test
    public void testClone() {
        Person bonni = new Person("bonni", 21);
        System.out.println("Person 1: " + bonni);

        Person nina = (Person) bonni.clone();
        nina.setName("Nina");
        System.out.println("Person 2: " + nina);

        Dolphin jerry = new Dolphin("jerry", 78);
        System.out.println("Dolphin 1: " + jerry);

        Dolphin sam = (Dolphin) jerry.clone();
        System.out.println("Dolphin 2: " + sam);
    }
}
```

#### 2. 使用`Cloneable`接口：

Animal.java:

```java
public interface Animal extends Cloneable {
    Animal clone();
}
```

Person.java:

```java
public class Person implements Animal {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
        System.out.println("Person is created ...");
    }

    @Override
    public Animal clone() {
        System.out.println("Creating person ...");
        Person person = null;
        try {
            person = (Person) super.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return person;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

Run.java:

```java
public class Run {
    public static void main(String[] args) {
        Person person = new Person("james", 45);
        System.out.println("Person 1: " + person);

        Person secondPerson = (Person) person.clone();
        System.out.println("Person copy: " + secondPerson);

        System.out.println(System.identityHashCode(person) + "\n"
            + System.identityHashCode(secondPerson));
    }
}
```

## Mediator Pattern (中介者模式):

### Introduction:

把复杂的信息集中控制。

就像飞机航线一样，每个飞行员不知道其他飞机的航线（什么时候起飞、哪里停止。。），但是通过总控制系统（指挥中心），就只需要指到自己什么时候起飞、哪里停止即可，简化了飞行员的工作。我们只需要在一个地方即可掌握所有的航班信息。

感觉就跟星链一代的激光通讯一样，哈哈哈。。

Java 中的`Timer`和`多线程`的某些JDK库用到了该设计模式。

### Code:

ATCMediator.java:

```java
public interface ATCMediator {
    void sendMessage(String msg, AirCraft airCraft);
    void addAirCraft(AirCraft airCraft);
}
```

AirCraft.java:

```java
public abstract class AirCraft {
    protected ATCMediator mediator;
    protected String name;

    public AirCraft(ATCMediator mediator, String name) {
        this.mediator = mediator;
        this.name = name;
    }

    public abstract void send(String msg);
    public abstract void receive(String msg);
}
```

ATCMediatorImpl.java:

```java
public class ATCMediatorImpl implements ATCMediator {
    private List<AirCraft> airCraftList;

    public ATCMediatorImpl() {
        airCraftList = new ArrayList<>();
    }

    @Override
    public void sendMessage(String msg, AirCraft airCraft) {
        for (AirCraft a : airCraftList) {
            // message should not be received by the aircraft sending the message
            if (a != airCraft) {
                a.receive(msg);
            }
        }
    }

    @Override
    public void addAirCraft(AirCraft airCraft) {
        airCraftList.add(airCraft);
    }
}
```

AirCraftImpl.java:

```java
public class AirCraftImpl extends AirCraft {
    public AirCraftImpl(ATCMediator mediator, String name) {
        super(mediator, name);
    }

    @Override
    public void send(String msg) {
        System.out.println(name + ": Sending message = " + msg);
        mediator.sendMessage(msg, this);
    }

    @Override
    public void receive(String msg) {
        System.out.println(name + ": Receiving message = " + msg);
    }
}
```

MediatorPatternTest.java:

```java
public class MediatorPatternTest {
    @Test
    public void testMediatorPattern() {
        ATCMediator mediator = new ATCMediatorImpl();

        // Create few aircraft
        AirCraft boing1 = new AirCraftImpl(mediator, "Boing 1");
        AirCraft helicopter = new AirCraftImpl(mediator, "Helicopter");
        AirCraft boing707 = new AirCraftImpl(mediator, "Boing 707");

        // Adding aircraft to the mediator
        mediator.addAirCraft(boing1);
        // mediator.addAirCraft(helicopter);
        mediator.addAirCraft(boing707);

        boing1.send("Hello from Boing 1");
    }
}
```

## Visitor Pattern:

### Introduction:

更策略模式有点像。

### Code:

Visitor.java:

```java
public interface Visitor {
    double visitor(Shirt shirtItem);
    double visitor(TShirt tShirtItem);
    double visitor(Jacket jacketItem);
}
```

Visitable.java:

```java
public interface Visitable {
    double accept(Visitor visitor);
}
```

TaxVisitor.java:

```java
public class TaxVisitor implements Visitor {
    DecimalFormat decimalFormat = new DecimalFormat("###.##");

    @Override
    public double visitor(Shirt shirtItem) {
        System.out.println("Shirt final price with tax: ");
        return Double.parseDouble(decimalFormat.format(Double.parseDouble(decimalFormat.format(shirtItem.getPrice() * 0.10)) + shirtItem.getPrice()));
    }

    @Override
    public double visitor(TShirt tShirtItem) {
        System.out.println("TShirt final price with tax: ");
        return Double.parseDouble(decimalFormat.format(Double.parseDouble(decimalFormat.format(tShirtItem.getPrice() * 0.18)) + tShirtItem.getPrice()));
    }

    @Override
    public double visitor(Jacket jacketItem) {
        System.out.println("Jacket final price with tax: ");
        return Double.parseDouble(decimalFormat.format(Double.parseDouble(decimalFormat.format(jacketItem.getPrice() * 0.20)) + jacketItem.getPrice()));
    }
}
```

Shirt.java:

```java
public class Shirt implements Visitable {
    private double price;

    public Shirt(double price) {
        this.price = price;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public double accept(Visitor visitor) {
        return visitor.visitor(this);
    }
}
```

TShirt.java:

```java
public class TShirt implements Visitable {
    private double price;

    public TShirt(double price) {
        this.price = price;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public double accept(Visitor visitor) {
        return visitor.visitor(this);
    }
}
```

Jacket.java:

```java
public class Jacket implements Visitable {
    private double price;

    public Jacket(double price) {
        this.price = price;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public double accept(Visitor visitor) {
        return visitor.visitor(this);
    }
}
```

VisitorPatternTest.java:

```java
public class VisitorPatternTest {
    @Test
    public void testVisitorPattern() {
        Visitor taxVisitor = new TaxVisitor();

        Shirt shirt = new Shirt(45.99);
        TShirt tShirt = new TShirt(129.99);
        Jacket jacket = new Jacket(399.99);

        // Use out tax calculations
        System.out.println(shirt.accept(taxVisitor));
        System.out.println(tShirt.accept(taxVisitor));
        System.out.println(jacket.accept(taxVisitor));
    }
}
```

## Memento Pattern:

### Introduction:

备忘录模式：能存储几个状态，用于后面回溯或者转换，即`undo`操作。

### Code:

Memento.java:

```java
public class Memento {
    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}
```

Originator.java:

```java
public class Originator {
    // This string is just to simplify our understanding.
    // In a real application you would have an actual Java
    // model class: Person.java, Character.java etc.
    private String state;

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }

    public Memento createMemento() {
        return new Memento(state);
    }

    public void setMemento(Memento memento) {
        state = memento.getState();
    }
}
```

CareTaker.java:

```java
public class CareTaker {
    private List<Memento> stateList = new ArrayList<>();

    public void addMemento(Memento memento) {
        stateList.add(memento);
    }

    public Memento getMemento(int index) {
        return stateList.get(index);
    }
}
```

App.java:

```java
public class App {
    public static void main( String[] args ) {
        Originator originator = new Originator();
        originator.setState("Monster");

        Memento memento = originator.createMemento();

        CareTaker careTaker = new CareTaker();
        careTaker.addMemento(memento);

        originator.setState("Monster 2");
        originator.setState("Monster 3");

        memento = originator.createMemento();
        careTaker.addMemento(memento);

        originator.setState("Monster 4");

        System.out.println("Originator current state: " + originator.getState());

        System.out.println("Originator restoring to previous state ... ");
        memento = careTaker.getMemento(1);
        originator.setMemento(memento);

        System.out.println("Originator current state: " + originator.getState());

        System.out.println("Originator restoring to previous state ... ");
        memento = careTaker.getMemento(0);
        originator.setMemento(memento);

        System.out.println("Originator current state: " + originator.getState());
    }
}
```

## Interpreter Pattern:

### Introduction:

就如其名，比如对我们语言的解释，Chinese -> English；或者 Source Code -> Interpreter/Compiler -> Bytecode。

### Code:

InterpreterContext.java:

```java
public class InterpreterContext {
    public String getBinaryFormat(int num) {
        return Integer.toBinaryString(num);
    }

    public String getHexFormat(int num) {
        return Integer.toHexString(num);
    }
}
```

Expression.java:

```java
public interface Expression {
    String interpreter(InterpreterContext interpreterContext);
}
```

IntToBinaryExpression.java:

```java
public class IntToBinaryExpression implements Expression {
    private int num;

    public IntToBinaryExpression(int num) {
        this.num = num;
    }

    @Override
    public String interpreter(InterpreterContext interpreterContext) {
        return interpreterContext.getBinaryFormat(num);
    }
}
```

IntToHexExpression:

```java
public class IntToHexExpression implements Expression {
    private int num;

    public IntToHexExpression(int num) {
        this.num = num;
    }

    @Override
    public String interpreter(InterpreterContext interpreterContext) {
        return interpreterContext.getHexFormat(num);
    }
}
```

App.java:

```java
public class App {
    private InterpreterContext interpreterContext;

    public static void main( String[] args ) {
        String first = "13 in Binary";
        String second = "28 in Hexadecimal";

        App interpreter = new App(new InterpreterContext());
        System.out.println(first + " = " + interpreter.interpret(first));
        System.out.println(second + " = " + interpreter.interpret(second));
    }

    public App(InterpreterContext interpreterContext) {
        this.interpreterContext = interpreterContext;
    }

    public String interpret(String str) {
        Expression expression = null;
        int num = Integer.parseInt(str.substring(0, str.indexOf(" ")));
        if (str.contains("Hexadecimal")) {
            expression = new IntToHexExpression(num);
        } else if (str.contains("Binary")) {
            expression = new IntToBinaryExpression(num);
        } else {
            return str;
        }
        return expression.interpreter(interpreterContext);
    }
}
```

## Chain of Responsibility Pattern:

### Introduction:

不同层次的人，能力也不同，就要进行“区别对待”，即见什么样的人，说什么样的话。

### Code:

PurchasePower.java:

```java
public abstract class PurchasePower {
    protected static final double BASE = 1000;
    protected PurchasePower successor;

    abstract protected double getAllowable();
    abstract protected String getRole();

    public PurchasePower getSuccessor() {
        return successor;
    }

    public void setSuccessor(PurchasePower successor) {
        this.successor = successor;
    }

    public void processRequest(PurchaseRequest request) {
        if (request.getAmount() < getAllowable()) {
            System.out.println(getRole() + " will approve $" + getAllowable());
        } else if (successor != null) {
            successor.processRequest(request);
        } else {
            System.out.println("Nobody can approve this!!!");
        }
    }
}
```

PurchaseRequest.java:

```java
public class PurchaseRequest {
    private double amount;
    private String purpose;

    public PurchaseRequest(double amount, String purpose) {
        this.amount = amount;
        this.purpose = purpose;
    }

    public double getAmount() {
        return amount;
    }
}
```

CEOPurchasePower.java:

```java
public class CEOPurchasePower extends PurchasePower {
    @Override
    protected double getAllowable() {
        return BASE * 100;
    }

    @Override
    protected String getRole() {
        return "CEO";
    }
}
```

DirectorPurchasePower.java:

```java
public class DirectorPurchasePower extends PurchasePower {
    @Override
    protected double getAllowable() {
        return BASE * 20;
    }

    @Override
    protected String getRole() {
        return "Director";
    }
}
```

ManagerPurchasePower.java:

```java
public class ManagerPurchasePower extends PurchasePower {
    @Override
    protected double getAllowable() {
        return BASE * 10;
    }

    @Override
    protected String getRole() {
        return "Manager";
    }
}
```

App.java:

```java
public class App {
    public static void main( String[] args ) {
        CEOPurchasePower ceoPurchasePower = new CEOPurchasePower();
        DirectorPurchasePower directorPurchasePower = new DirectorPurchasePower();
        ManagerPurchasePower managerPurchasePower = new ManagerPurchasePower();

        directorPurchasePower.setSuccessor(ceoPurchasePower);
        managerPurchasePower.setSuccessor(directorPurchasePower);

        while (true) {
            System.out.println("Enter the amount to check who should approve to their budget: ");
            System.out.print(">>");

            try {
                double d = Double.parseDouble(new BufferedReader(new InputStreamReader(System.in)).readLine());
                managerPurchasePower.processRequest(new PurchaseRequest(d, "Buy stuff"));
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## Bridge Pattern:

### Introduction:

