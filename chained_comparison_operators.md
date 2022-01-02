# Chained comparison operators

## General idea

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
if (0 <=foo() <= 10) {...}
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


## Hurdles to overcome

Someone needs to have the time and inclination to implement it.

## Forecast

Might happen one day. Not hugely urgent, but possibly a reasonably small RFC.

## Notes

Some details of [how they work in Python](https://mathspp.com/blog/pydonts/chaining-comparison-operators)

> Did you know that you can actually chain an arbitrary number of comparison operators? For example, a == b == c == d == e checks if all five variables are the same, while a < b < c < d < e checks if you have a strictly increasing sequence.


A [nice video](https://www.youtube.com/watch?v=M3GAJ1AIIlA&ab_channel=mCoding) that explains some good uses, questionable uses, and bad uses of chained operators from about the 4 minute mark onwards.


