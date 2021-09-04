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

### 5. Intorduction

现实中很常用。

一个总的 Object 与其他 Subscribers (Listener) 建立依赖，一旦这个 Object 发生改变，它的 Subscribers 也自动被通知和发生改变。如：订阅邮箱、电视机或手机接收卫星信号等。

![ObserverPattern](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Observer Pattern\ObserverPattern.png)

wiki:

![Observer Pattern From Wiki](F:\Note\IT\Platforms\Udemy\Design Pattern\Pictures\Observer Pattern\Observer Pattern From Wiki.png)

### 6. Coding

