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

StrategyTest.java:

```java
public class StrategyTest {
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



