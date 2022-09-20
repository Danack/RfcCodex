


engine called "*class static initialization block*".

https://v8.dev/blog/v8-release-94

In short, it is a method that is executed once when a class is imported and
loaded, allowing for some more advanced initialization process to be done.

class Test {
static readonly Carbon $now;

    static () {
        self::$now = now();
    }
}

Currently I can only do this in a very hacky way, usually by creating a
public static method and calling it after class initialization.

class Test {
static Carbon $now;

    public static function init(): void {
        self::$now = now();
    }
}


In `MyClass.php`:

```php
class MyClass {
    public static DateTimeImmutable $startup;
    public function horribleInitializationPractices() {
        self::$startup = new DateTimeImmutable();
    }
}

MyClass::horribleInitializationPractices();
```
Previously

https://wiki.php.net/rfc/static_class_constructor