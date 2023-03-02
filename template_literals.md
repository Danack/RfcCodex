# Template string literals

## General idea

As part of the [is_literal RFC discussion](https://wiki.php.net/rfc/is_literal), one thing was mentioned was that just being able to tell if some string is a literal written in the source code doesn't provide much value.

The feature of [template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) is much more useful as it makes it easier to write custom DSL's in PHP code. We should steal it from JavaScript.

The TL:DR of template literals is that they provide an easy way of separating strings written by a programmer from values.

Imagine that PHP supported template literals through the syntax of three backticks "`​``template goes here`​``", then the following code:

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

foo(```That {$person} is age {$age}.```);

```

Would have the output of:

```
String parts are:
array(3) {
  [0]=>
  string(5) "That "
  [1]=>
  string(6) " is age "
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
$db->query(```select * from foo where user_id = {$_SESSION['user_id']} and topic like {$_REQUEST['search']}```);
```

Without having to jump through the hoops of using a special query builder to ensure the parameters are handled correctly.

The exact details of the syntax who probably depend on parser and other technical limitations.

## Heredoc + string limitations on calling functions


It is possible to use variables inside a string:
```
// String example

$name = "Danack";

echo "Hello there {$name}!";

// Output is 'Hello there Danack!'
```

Or a heredoc block:

```
$name = "Danack";
$text = <<< TEXT
Hello there {$name}!
TEXT;

// Output is 'Hello there Danack!'
```


However, it is not possible to directly use a function inside a string: 

```
// String example
function get_name()
{
    return "Danack";
}

echo "Hello there {get_name()}!";

// Output 'is Hello there {get_name()}!' 
```

or a heredoc block:

```
function get_name()
{
    return "Danack";
}

echo <<< TEXT
Hello there {get_name()}!
TEXT;

// Output 'is Hello there {get_name()}!' 

```

Instead, you need to jump through the hoop of using a variable to reference a closure of the function:

```
// string example
function get_name()
{
    return "Danack";
}

$fn_get_name = get_name(...);

echo "Hello there {$fn_get_name()}!";
```

```
// heredoc example

function get_name()
{
    return "Danack";
}

$fn_get_name = get_name(...);

echo <<< TEXT
Hello there {$fn_get_name()}!
TEXT;

// Output is 'Hello there Danack!'
```

Which is an 'ungreat' limitation. If PHP is getting a new way of doing template strings, then fixing this limitation would be good. 


## Hurdles to overcome

### Syntax needs to be chosen

Currently, backticks as used in JavaScript are used as the [execution operator in PHP](https://www.php.net/manual/en/language.operators.execution.php).

Although using the same syntax as JavaScript would be nice, not clashing with the current usage is probably a priority.

Triple backticks seem to be an available option, and would allow a Markdown style of indicating what the type of text was:

```
$name = 'John';
$greeting = ```html

<p>Hello there {$name}, I am clearly some HTML. </p>

`​``  

echo $greeting;

```


## Forecast

Probably a good idea, that will happen when someone has time, energy and inclination to implement it.

## Notes

### Why string template literals are superior to literal string for security hole preventation

Imagine you have some insecure code like:

```
$sql = "
  select * from foo
  where user_id = {$_SESSION['user_id']} and
  topic like {$_REQUEST['search']}
";
```

to convert that to secure code, using statements and bound parameters would take a non-trivial amount of work.

Converting to use a string template literal like:


```
$sql = `​``
  select * from foo
  where user_id = {$_SESSION['user_id']} and
  topic like {$_REQUEST['search']}
`​``;
```

takes mere seconds.

### JS implementation

The JavaScript implementation also gives access to the 'raw' string:

> The special raw property, available on the first argument to
> the tag function, allows you to access the raw strings as they
> were entered, without processing escape sequences.

This is to avoid [Leaning toothpick syndrome](https://en.wikipedia.org/wiki/Leaning_toothpick_syndrome), which is the phenomenon that happens when you embed a string that needs to contain a slash into a string that is escaped by a slash character.
