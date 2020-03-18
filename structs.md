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
    readonly int $x;
    readonly int $y;
    readonly int $z;
}
```


## Hurdles to overcome


### Needs more thinking

Although quite a few people have suggested this as a solution, as far as I'm aware, no one has sat down and thought through exactly how it should work.

### Syntax

No doubt, everyone will have an opinion on the syntax to be chosen. 


## Forecast

Dunno. 

## Notes

