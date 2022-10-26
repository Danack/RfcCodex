# Template string literals

## General idea

As part of the [is_literal RFC discussion](https://wiki.php.net/rfc/is_literal), one thing was mentioned was that just being able to tell if some string is a literal written in the source code doesn't provide much value.

The feature of [template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) is much more useful as it makes it easier to write custom DSL's in PHP code. We should steal it from JavaScript.

The TL:DR of template literals is that they provide an easy way of separating strings written by a programmer from values.

Imagine that PHP supported template literals through the syntax "$\`template goes here\`", then the following code:

```
function foo(TemplateLiteral $tl) {
    echo "String parts are:\n";
    var_dump($tl->getStringParts());

    echo "\n";

    echo "Values are:\n";
    var_dump($tl->getValues());
}

$person = 'John';
$age = 42;

foo($`That $person is a $age.`);

```

Would have the output of:

```
String parts are:
array(3) {
  [0]=>
  string(5) "That "
  [1]=>
  string(6) " is a "
  [2]=>
  string(1) "."
}

Values are:
array(2) {
  [0]=>
  string(4) "John"
  [1]=>
  int(42)
}
```

i.e. all of the literal strings are available, and all of the values of the variables are available, but those two things are completely separated.


The improvement over is_literal is that it would allow users to write things like DB queries in a very natural way, e.g.:

```
$db->query($`select * from foo where user_id = $_SESSION['user_id'] and topic like $_REQUEST['search']`)
```

Without having to jump through the hoops of using a special query builder to ensure the parameters are handled correctly.

The exact details of the syntax who probably depend on parser and other technical limitations.

## Hurdles to overcome

### Syntax needs to be chosen

Currently backticks as used in JavaScript are used as the [execution operator in PHP](https://www.php.net/manual/en/language.operators.execution.php).

Although using the same syntax as JavaScript would be nice, not clashing with the current usage is probably a priority.


## Forecast

Probably a good idea, that will happen when someone has time, energy and inclination to implement it.

## Notes

The JavaScript implementation also gives access to the 'raw' string:

> The special raw property, available on the first argument to
> the tag function, allows you to access the raw strings as they
> were entered, without processing escape sequences.

The utility of this needs to be understood.
