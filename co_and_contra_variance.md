# Co and contravariance


# General idea

Consider this specific case:

```php
class A {
    function foo(): B {
        return new B();
    }
}
class B extends A {
    function foo(): C {
        return new C();
    }
}
class C extends B {}
```

# Hurdles

The way we did our passes at the time (and I still believe this is the case even on master) meant that trying to verify that C is a subclass of B (which is required for seeing if B::foo(): C is compatible with A::foo(): B) would trigger the autoloader. We currently do not have any code that exists that requires you to use an autoloader (meaning you can always re-order things and include things in a different order and get around it) so I was very unhappy with that solution.


The alternative and better option is to first register all the classes and their inheritance hierarchies then in another pass verify them for correctness. This would prevent the autoloader from triggering in the above case. I expect when we add covariant return types we will take this approach.


# Result

The RFC was accepted for PHP 7.4 before I wrote this one up properly.