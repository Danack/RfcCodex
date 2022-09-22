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

The situation is even worse if you want to check one number is less than another, and that they are both in a range:

```
if (0 <= x <= y <= 1) {
    echo "Both x and y are between zero and one, and x is less than or equal to y.";
}
```

is the equivalent of:

```
if ((0 <= x <= 1) && (0 <= y <= 1) && (x <= y) ) {
    echo "Both x and y are between zero and one, and x is less than or equal to y.";
}
```

## Lessons from Python

The implementation of chained operators in Python allows arbitrary chaining of different types of operators. This is a choice that people have come to regret.

Careful consideration of the allowed chaining would be better than just allowing everything.

### Good

These are good examples that show how using chained comparision is better than not using it.

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


### Meh

These aren't terrible, but few people would call them easier to read than the unchained equivalents:

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

### Bad

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

Note, the `x != y != z` is similar to the 'ungood' [variadic empty rfc](https://wiki.php.net/rfc/variadic_empty), which people did not understand imho.

## Hurdles to overcome

Someone needs to have the time and inclination to implement it.

### More restrictions than Python


## Forecast

A lot of people will have a gut instinct against this, so the vote might be close even with a good implementation.


## Notes

Some details of [how they work in Python](https://mathspp.com/blog/pydonts/chaining-comparison-operators)

> Did you know that you can actually chain an arbitrary number of comparison operators? For example, a == b == c == d == e checks if all five variables are the same, while a < b < c < d < e checks if you have a strictly increasing sequence.

A [nice video](https://www.youtube.com/watch?v=M3GAJ1AIIlA&ab_channel=mCoding) that explains some good uses, questionable uses, and bad uses of chained operators from about the 4 minute mark onwards.


## Spare words

Python allows this:

```
if (0 <= x <= 10) {...}
```

i.e. compare that x is greater or equal than zero, and also that x is less than or equal to 10. It's nice as it reads nice, but also avoids a problem. That code is equivalent to:

```
if (0 <= x && x <= 10) {...}
```

But imagine we had:
```
if (0 <= foo() <= 10) {...}
```
and foo() had side-effects then the equivalent code:

```
if (0 <= foo() && foo() <= 10) {...}
```
is calling foo() twice, which is bad as the side-effect is produced twice. The workaround of:

```
y = foo()

if (0 <= y && y<= 10) {...}
```
is jankier, as it makes the code harder to read.

PHP would be better if we just stole this feature. Did I say steal? I meant be inspired by. I apologies for the confusion.

