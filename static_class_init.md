# Static class initialization

## General idea

Some languages allow you to define some code that is run when a class is loaded for the first time.

```java
public class Demo
{
    static double percentage;
    static int rank;
    static
    {
        percentage = 44.6;
        rank = 12;
        System.out.println("STATIC BLOCK");
    }
    public static void main(String args[])
    {
        Demo st = new Demo();
        System.out.println("MAIN METHOD");
        System.out.println("RANK: " + rank);
    }
}
```

People who are used to this style of code miss having it in PHP.

## Hurdles to overcome

### Easier in static linked languages

TODO - link to explanation of PHP's circular class dependency problem

### Quite magic

The behaviour of static class initialization is quite magic. Johannes Schlüter put it quite clearly:

  'In my opinion this makes the language way more complex as there are more
  places which "suddenly" execute code but solves a small problem compared
  to that. (Which actually is an issue many people would suggest to avoid
  completely instead of ennobling this with a language feature.)

  Why am I saying it makes the language more complex? - Your proposal
  seems to miss mentioning when exactly the method is executed. what is
  the output of

```
a.php:
<?php
echo 'A: '.__FILE__.':'.__LINE__."\n";
class A {
    static function __static() {
      echo __CLASS__.'::'.__METHOD__."\n";
    }
}
echo 'B: '.__FILE__.':'.__LINE__."\n";
class B {
    static function __static() {
      echo __CLASS__.'::'.__METHOD__."\n";
    }
}
echo 'C: '.__FILE__.':'.__LINE__."\n";
?>

b.php:
<?php
echo 'D: '.__FILE__.':'.__LINE__."\n";

C::$foo = 23;
echo 'E: '.__FILE__.':'.__LINE__."\n";

include 'a.php';
echo 'F: '.__FILE__.':'.__LINE__."\n";


class C {
    static $foo = 0;
    static function __static() {
      echo __CLASS__.'::'.__METHOD__."\n";
    }
}

echo 'G: '.__FILE__.':'.__LINE__."\n";

class D extends B {
    static function __static() {
      echo __CLASS__.'::'.__METHOD__."\n";
    }
}

echo 'H: '.__FILE__.':'.__LINE__."\n";
?>
```

  Mind that in b.php we make use of class C above the declaration, which
  we can do as C is a simple class and can be bound early during
  compilation. Class D however can only be bound during run-time, after
  including a.php, which happens after C was already used.'


### It's already possible without engine support

```php
class MyClass {
    public static DateTimeImmutable $startup;
    public function horribleInitializationPractices() {
        self::$startup = new DateTimeImmutable();
    }
}

MyClass::horribleInitializationPractices();
```

It's quite hard to make an argument for something to be added to the engine, when it's already possible in userland.

## Forecast

Quite unlikely to happen, unless someone can find a strong justification for adding it to the language.

## Notes

Previous [static class constructor RFC](https://wiki.php.net/rfc/static_class_constructor)

