# Structs 

## General idea

The syntax for defining and using classes in PHP is quite 'heavy' through being verbose.

For example, the code to define a 3D coordinate:

```
class Coordinate3d {
    
    private int $x;

    private int $y;

    private int $z;

    public function __construct($x, $y, $z) {
        $this->x = $x;
        $this->y = $y;
        $this->z = $z;
    }

    public function getX() {
        return $this->x;
    }

    public function getY() {
        return $this->y;
    }

    public function getZ() {
        return $this->z;
    }
}


$coord = new Coordinate(1, 2, 3);

```

could be implemented by something like:

```
struct Coordinate3d {
    int $x;
    int $y;
    int $z;
}
```

## Hurdles to overcome


### Needs more thinking

Although quite a few people have suggested this as a solution, as far as I'm aware, no one has sat down and thought through exactly how it should work.

### Needs clear benefits

Although it's clear that classes are too 'heavy' it's hard to say exactly what would be better about structs. The following are possible:

#### Immutable by default

This would save a lot of typing, and is the correct behaviour for the majority of 'data storage' like objects.


```
function foo(Coordinate3d $coord) {
    $coord->x = 5;
    // Error Coordinate3d::x is immutable.
}

```

#### Checks properties are set during construction

```
struct Coordinate3d {
    int $x;
    int $y;
    int $z;
}

$coord = new Coordinate3d([x=1, y=2]);
// Error failed to initialize property Coordinate3d::z during structure construction 

```

This might not be compatible with having 'circular' data structures (where A uses B, B uses C, C uses A} as none of them could be fully constructed first before being used by the next.

#### Rust-like cloning

```
$startPosition = new Coordinate3d([x=1, y=2, z=3]);
$endPosition = new Coordinate3d([x=7, ...$startPosition]);
```


#### No inheritance?

Theoretically that could be large performance gain compared to classes. TODO get someone who knows to comment.


#### No __set, __get, __call(), __callStatic(), __isset() support

These are not appropriate things to have on structures. Should provide performance gain compared to classes. TODO get someone who knows to comment.


### Syntax

No doubt, everyone will have an opinion on the syntax to be chosen. 


## Forecast

Having named parameters first for the cloning syntax would make this idea easier. 

## Notes

