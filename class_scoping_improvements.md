# Class scoping improvements

## General idea

There are times when a class needs to expose a public method to other classes, but it is not intended for this method to be called by any arbitrary code; it should only be called by 'collaborating' classes within the same package as that class.

For example, everything inside the [Doctrine\ORM\Internal\*](https://github.com/doctrine/orm/tree/master/lib/Doctrine/ORM/Internal) namespace are things that people shouldn't touch. However the public methods need to be public so that they are accessible to the other Doctrine classes.

Currently there is no way to enforce that some methods should be available to some classes, but not all other classes.

### Similarity to nested/inner classes

Java has the the idea of nested classes, where a class can be defined within another class, and is only available from within that outer class.

```php

class Outer_Demo {
   int num;
   
   // inner class
   private class Inner_Demo {
      public void print() {
         System.out.println("This is an inner class");
      }
   }
   
   // Accessing he inner class from the method within
   void display_Inner() {
      Inner_Demo inner = new Inner_Demo();
      inner.print();
   }
}
```


## Hurdles to overcome

### Low demand

Although there is some need for it, the problem it addresses is not one that is stopping people from being able to actually write applications in PHP.

Additionally, the problem can also be 'fixed' through documentation and/or automatically closing any issues raised by people who are ignoring the 'do not touch this class' warning sign. 


### Design of implementation

It's not obvious what a good design for this problem would be.

The design in C++ of class 'friendship' is not a good one to copy, at least in part because it requires coupling the 'private' class to any other class that might need it.

For PHP it might make more sense to have the declarations done at a namespace level, so something like "the classes and methods in this namespace are only callable from these namespaces". 

## Forecast

Might happen, if someone finds enough energy to really push for it.

I suspect it just is never going to be high up enough on anyone's list of things that ought to be done, though, as there are many other better ways of spending energy.

## Notes

The idea of importing C++ style 'friendship' declarations was rejected quite decisively: https://wiki.php.net/rfc/friend-classes

It looks like there may be another draft: https://wiki.php.net/rfc/namespace-visibility

