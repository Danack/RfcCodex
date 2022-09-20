# Chained comparison operators 

## General idea

Currently in PHP operators if you want to check a number is in a range you have to reference it twice in an if statement:

```
if (0 <= x && x <= 1) {
    echo "x is between zero and one";
} 
```

Other languages allow operators to be chained:

```
if (0 <= x <= 1) {
    echo "x is between zero and one";
} 
```


## Hurdles to overcome

### Better examples needed

Because a compelling example is about 50% of the battle for getting an RFC passed.

### More restrictions than Python 

This is a [good video tutorial](https://www.youtube.com/watch?v=M3GAJ1AIIlA) about chained operators in Python.
 

#### Good

```
def chained_comparisons_good_uses(x, y, z):
    if 0 < x < 1:
        print("x in range (0,1)")

    if 0 <= x < 1:
        print("x in range [0,1)")

    if x <= y <= z:
        print("y in range [x,z]")

    if x >= y >= 1:
        print("y in range [1,x]")

    if x == y == z:
        print("x,y,z all equal")

```


#### Meh

```
def chained_comparisons_ok_to_questionable_uses(x, y, z):
    if 0 < x < y == z < 1:
        print("x,y in (0,1) with x<y and z==y")

    if x <= y <= z != 1:
        print("y in range(x,z) with z != 1")

    if x == y == z != 1:
        print("x,y,z all equal something that isn't 1")

    if x is y is z:
        print("x,y,z all identical")

    if x is y is z in [1, 2, 3]:
        print("x,y,z all identical and in [1,2,3]")
```

#### Bad

These should be forbidden:

```
def chained_comparisons_bad_uses(x, y, z):
    if x < y > z:
        print("y > max(x,z)")

    if x != y != z:
        print("kinda looks like x,y,z all distinct, but may have x==z")

    if 0 > x < y != z > 1:
        print("WHY??")

    if 0 < x > 1 >> y << 1 < z > 1:
        print("please remove this from the language")

```


## Forecast

A lot of people will have a gut instinct against this, so the vote might be close even with a good implementation.

## Notes



