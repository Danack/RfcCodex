# Ternary operator change from left-associative to right-associative  

## General idea

Note please see the <a href='#forecast'>forecast</a>.

Quoting from [phpsadness](http://phpsadness.com/sad/30):

(In PHP) the ternary operator is left-associative and therefore behaves entirely 'incorrectly':

```bash
$ cat ternary.php
<?php
echo (FALSE ? "a" : FALSE ? "b" : "c")."\n";
echo (FALSE ? "a" : TRUE ? "b" : "c")."\n";
echo (TRUE ? "a" : FALSE ? "b" : "c")."\n";
echo (TRUE ? "a" : TRUE ? "b" : "c")."\n";
?>

$ php ternary.php
c
b
b
b
```

In any other language with a ternary operator, you can stack them and build an if-elseif-elseif-else expression:

```bash
$ cat ternary.pl
#!/usr/bin/perl -w
use strict;

print +(0 ? "a" : 0 ? "b" : "c")."\n";
print +(0 ? "a" : 1 ? "b" : "c")."\n";
print +(1 ? "a" : 0 ? "b" : "c")."\n";
print +(1 ? "a" : 1 ? "b" : "c")."\n";

$ perl ternary.pl
c
b
a
a

```


## Hurdles to overcome

There are a couple of big hurdles that would need to be overcome.

### How to make the change

It would not be feasible to solely change the associativity without taking any other steps. This would silently break any code that contains any nested ternaries.

A better plan that allows for a deprecation notice to be generated for at least one minor version of PHP would be required.

An alternative approache might be to use a different symbol.

### Break a large amount of existing code

People would need convincing that breaking existing code would justified by the change in associative rules.  

### Nested ternary operators are terrible

Nested ternaries in real code do not look like the 'clean' examples given:

```php
print +(0 ? "a" : 0 ? "b" : "c")."\n";
```

Instead, when you use actual variable names with them they look much more like this:

```php
print($isBookingBlocked ? "Unavailable" : $hasBeenReserved ? "Reserved" : "Open") . "\n";
```

Although people who like ternaries may disagree, this code is not easy to read. It requires the reader to accurately parse a line horizontally.  It also requires a user to remember multiple things at once, which tends to lead to mistakes.

Using actual if else statements makes the code far easier to read.

```php
$status = "Open";
if ($isBookingBlocked) {
    $status = "Unavailable";
}
else if ($hasBeenReserved) {
    $status = "Reserved";
}
```

## Forecast

---Quite unlikely to happen without a cunning plan.---

---About the only way this could be addressed would be to use a new symbol for a right associative ternary operator.---

---To keep the similarity with the current question mark `?`, an inverted question mark `¿` could be used. /s---

From PHP 7.4 [ternaries require parentheses](https://wiki.php.net/rfc/ternary_associativity) to set the correct order. This would allow us to implement them to be right associative by default if we wanted to.


## Notes

http://phpsadness.com/sad/30
