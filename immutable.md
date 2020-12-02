# Immutable objects

## General idea

Currently it is not possible to prevent 'accidental' mutation of object properties.

Considers this code, where a PR has been made to add a setPath method to a class:

```php

class Settings {

    protected string $path;

    public function __construct(string $path)
    {
        check_path_is_acceptable($path);
        // Do not change path after this point!
        $this->path = $path;
    }

    // 400 lines of code here
    // 400 lines of code here
    // 400 lines of code here

    // Team member wants to add this function 
    // And as the PR is many lines below the note saying
    // do not change, the reviewer might not notice the problem
    public function setPath(string $path)
    {
        $this->path = $path; // 
    }
}
```

It would

```php

class Settings {

    protected immutable string $path;

    public function __construct(string $path)
    {
        check_path_is_acceptable($path);
        // Do not change path after this point!
        $this->path = $path;
    }

    // Team member wants to add this function 
    // And as the PR is many lines below the note saying
    // do not change, the reviewer might not notice the problem
    public function setPath(string $path)
    {
        $this->path = $path;
        // This generates an error saying the value of path
        // cannot be modified after being set.
    }
}
```

## Hurdles to overcome


The main reason the RFC failed before was due to a lack of support modiyfing properties during the cloning process of an object, which would have greatly restricted people's abilities to use immutable properties.  

### Syntax needed for clone

Sometimes during the clone of an object, you need to modify at least one property of the object. The new value can either be generated internally, or externally from the class. 

#### Internal variation of properties

When the new value of the property is generated internally to the clone method, this probably requires 'unlocking' the properties to be mutable again, during the clone of that object.

```php
class Foo
{
    private immutable $id;

    public function __construct()
    {
        $this->id = generate_unique_id();
    }

    public function __clone()
    {
        // This doesn't error, as object properties are 'unlocked'
        // from being immutable during clone.
        $this->id = generate_unique_id();
    }
}
```

#### External variation of properties

```php
class Foo
{
    private immutable $id;

    public function __construct($id)
    {
        $this->id = $id;
    }

    public function withNewId($newId) {
        $clone = clone $this;
        // This wouldn't work, we'd need a better solution
        $clone->id = $newId;
        return $clone;
    }
}
```


```php
class Foo
{
    private immutable $id;

    public function __construct($id)
    {
        $this->id = $id;
    }

    public function withNewId($newId) {
        $clone = clone($this, id: $newId);
        // This wouldn't work, we'd need a better solution
        $clone->id = $newId;
        return $clone;
    }
}
```

### Untyped properties that have an implicit default value

tbd this apparently is an issue.

### Constant-alike init-only properties that have a default value

tbd this apparently is an issue.

### Relation of property accessors to this idea

There is at least some overlap between this idea, and 'property accesores' aka `public get, private set` types of things, which have been raised before. However it's reasonably likely imo that i) the immutable idea is the more important of the two ii) it's also the more likely to have a reasonable discussion and implementation.

https://wiki.php.net/rfc/propertygetsetsyntax-v1.2
https://wiki.php.net/rfc/propertygetsetsyntax

### Bike-shedding over the name

Looking at the C# feature, init-only might be the best one, as it accurately describes when the property can be changed.

### Reflection

It's almost certainly the case that it would be appropriate for immutable/init-only properties to be changeable via Reflection, as this is both a useful thing to do, and consistent with other parts of the language where reflection can work around limits in the language. 

## Forecast

Likely to pass when the above hurdles are addressed.

## Notes

Two previous RFCs.

https://wiki.php.net/rfc/object-initializer
https://wiki.php.net/rfc/write_once_properties
