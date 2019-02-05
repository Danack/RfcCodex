# Enums

## General idea

Other languages allow programmers to define sets of constants. For example the days of week.

```
enum Days {
   SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, ;
}
```

These sets of constants can be used as a type (for parameter and return types) and the individual constants can be referenced.

```
function getDayDescription(Days day) : string {

    switch (day) {
        case Days.SUNDAY: return "Its Sunday :-)";
        case Days.MONDAY: return "Its Monday :*--(";
        case Days.TUESDAY: return "Its Tuesday :*-(";
        case Days.WEDNESDAY: return "Its Wednesday :*(";
        case Days.THURSDAY: return "Its Thursday :)";
        case Days.FRIDAY: return "Its Friday ;-D";
        case Days.SATURDAY: return "Its Saturday :=D";
    }
    
}
```

Additionally some IDEs/static code analysis tools can 'understand' enum sets, and so give warnings if some code does not handle all of the possible cases.

In the example above, if we missed one of the days in the switch statement, some tools would be able to warn us about that potential error.


## Hurdles to overcome


### Difference in views of what enums should be

There are some small differences in how enums could be implemented that need to be though through. e.g. should definitions of enums be allowed to define some of the values used for the entries, or not:

enum Foo {
    
    ZOQ,       // Defaults to 0?
    FOT = 2,   // user sets to 2?        
    PIK,       // defaults to 3?  
    ZEBRANKY = 'Frungy' // Allow mixture of types for enums?
};


### Time

The people who have worked on it are limited in time and energy.

## Forecast

Likely to happen.

More likely to happen sooner if a company could sponsor Levi or Bob to work on it with a few months salary.


## Notes

A draft RFC is at https://wiki.php.net/rfc/enum

