---
title: "Что каждый программист должен знать о цифрах с плавающей точкой?"
excerpt: "В статье будет представлен пример того, какие нюансы нужно учитывать работая с float и double в Java"
modified: 2016-11-20T09:55:10-04:00
header:
tags: 
  - java
  - float
  - BigDecimal
---

## Введение

Давайте рассмотрим _классический_ пример того, с чем может столкнуться каждый программист не изучавший ранее
как работают числа с плавающей точкой в современных компьютерных системах:

```java
public class FloatingNumbersMagic {

    public static void main(String[] args) {
        double f1 = 0.3f;
        double f2 = 0.4f;
        double sum = 0.3f + 0.4f;

        System.out.println(sum);
    }
}
```

Результат поразит неискушенного новичка:

```
Вместо 0.7 мы получим
0.7000000476837158
```

## Почему мы получили такой странный результат?
Потомучто _внутри_, компьютеры используют формат который не может ТОЧНО сохранить дробные числа(такие числа как: 0.1, 0.2 или 0.3 и т.п.) 
Этот формат - [двоичный с плавающей точкой](https://ru.wikipedia.org/wiki/Число_с_плавающей_запятой). 

Когда ваш код компилируется или интерпретируется ваше число "0.1" уже округляется до ближайшего
числа с плавающей точкой. Таким образом даже еще не начав реально считать мы получаем небольшие погрешности
при переводе числа в компьютерный формат(в Java это типы данных float или double).

## Почему компьютеры делают так?
На низком уровне, компьютеры построены из биллионов электрических элементов
которые имеют всего два состояния,  обычно это или 1 или 0(низкое напряжение или высокое).
На основе этих элементов ЛЕГКО построить схемы хранения ДВОИЧНЫХ чисел
и выполнения вычислений с ними.

Конечно возможно сэмулировать поведение десятичных чисел с двоичным
представлением однако это будет менее производительно.
Если бы компьютеры использовали десятичные числа они бы были
медленнее и потребляли бы больше памяти по сравнению с использованием двоичной арифметики.

## Когда нам надо быть осторожными?

Нужно быть осторожным ВСЕГДА когда вы используете float и double.
Если у вас финансовые вычисления основаны на этих типах данных у вас могут быть проблемы.
Для корректной работы с деньгами в java лучше использовать _BigDecimal_

```java
public class BigDecimalExample {

    public static void main(String[] args) {
        BigDecimal n1 = new BigDecimal("0.3");
        BigDecimal n2 = new BigDecimal("0.4");
        BigDecimal sum = n1.add(n2);
        System.out.println(sum.toString());
    }
}
```

Результат выполнения программы выше вполне вас удовлетворит:

```
0.7
```

Подробнее про данную тему можно почитать в следующих источниках:

 * [http://floating-point-gui.de](http://floating-point-gui.de)
 * [http://stackoverflow.com/questions/588004/is-floating-point-math-broken](http://stackoverflow.com/questions/588004/is-floating-point-math-broken)
 * [Что нужно знать про арифметику с плавающей запятой](https://habrahabr.ru/post/112953/)
 * [https://docs.oracle.com/javase/8/docs/api/java/math/BigDecimal.html](https://docs.oracle.com/javase/8/docs/api/java/math/BigDecimal.html)

