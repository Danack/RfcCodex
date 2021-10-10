# Understanding RFC attitudes 

This guide seeks to help people understand the attitude the PHP internal participants take when evaluating RFCs, and what factors are likely to make RFCs be less or more likely to pass.

It is written as my personal understanding of other people's priorities; which means that it is not guaranteed to be correct, and may become inaccurate over time as people's view change.

Please note, they are things people consider to evaluate the trade-offs. They are not hard or absolute rules.

The aim of this guide is to make it easier to understand the arguments people are going to make either in favour or against the RFC. Hopefully this will make it easier to write RFCs that address people's concerns and so lead to more productive conversations.

## Things people will consider as reasons to vote against an RFC

### Adding ini options

There is a general feeling that ini options are a mistake. In general they are harder to manage than not having them.

They are a particular problem where two libraries might want to have different settings (e.g. error handlers, or floating point precision) as there isn't any effective way to do that.

Application level ini settings are significantly less terrible (i.e. where one setting should be used across the entire application e.g. disabled functions) as they don't have the problem of different libraries needing different settings.

Any RFC that introduces new ini settings (except as short term workarounds for BC) is likely to not have a good reception.

### Can be done in userland

PHP is written in C. Maintaining C code is a lot harder than maintaining PHP code.

The release cycle of PHP is fixed, and relatively slow compared to userland projects. This means that BC breaks or adding new features is much harder for core PHP than userland projects.

Anything that is implemented in core PHP adds to the burden of maintaining core PHP. 

Because of those reasons, any RFC that could be implemented in userland (e.g. [Server-Side Request and Response Objects
](https://wiki.php.net/rfc/request_response) ) is going to have a pretty hard time passing without a clear justification of how being in core is better than being a userland library. 


### Bespoke syntax

Some RFCs have suggested introducing a new syntax to solve a relatively small problem.

* [Compact Object Property Assignment](https://wiki.php.net/rfc/compact-object-property-assignment)

* [Object Initializer](https://wiki.php.net/rfc/object-initializer)

Adding new syntax in this way does not seem a good approach to language design.

Rather than introducing the new syntax to be used for a small RFC, it would be better to introduce the new syntax as its own RFC, so that all the use cases of that syntax can be thought through, and then show how it could be used for the specific RFCs.  

For example, the [named parameters](https://wiki.php.net/rfc/named_params) introduces new syntax but does it in a way that fully thinks through that syntax, and how it would interact with existing PHP code. 

If the Named Parameters RFC was introduced, the syntax would be usable for the 'Object Initializer' and 'Compact Object Property Assignment' RFCs.

### Being obviously incomplete

It's okay for an RFC to deliberately leave stuff for future expansion out of the RFC, but it's much less okay to not address things that are going to be immediately frustrating for PHP users.

For example, for the [Write-Once Properties](https://wiki.php.net/rfc/write_once_properties) RFC, at least some of the no votes were because it did not address object cloning, which is a vital consideration when dealing with immutable objects.


### Not being aware of PHP's idiosyncrasies

There are features in other languages that are possible in those langauges because of the type system used in that language.

Because PHP's type system includes much more type juggling than other languages have, some features would be much more difficult to use in PHP.

For example, [Method Overloading](https://github.com/Danack/RfcCodex/blob/master/method_overloading.md) is something that people have asked for. However this idea is much more difficult to use in PHP where the type juggling makes it harder to reason about what method is going to be called.


### Adding more edge cases

The PHP language is not a perfect design. But internals would prefer to not make the language any worse by adding features that have many edge-cases.

Although the [Allow function calls in constant expressions](https://wiki.php.net/rfc/calls_in_constant_expressions) clearly makes PHP more powerful, it does so in a way that dramatically increases the number of edge-cases - in this case by allowing some, but not all functions to be used in const initializers.

### Small ratio of reward to work involved and BC breaks. 

There are some ideas that while they would definitely make PHP better, but currently don't justify doing the the work that would be involved to implement them, or the work the users of PHP would have to do to adapt to the backward-compatibility break.

This is the main reason that I haven't pursued the [Consistent Callables](
https://wiki.php.net/rfc/consistent_callables) RFC. Although that RFC would make PHP better, it wouldn't be significantly better. 

Instead being able to specify 'callable' signatures along the lines of:
```
typedef validateFn = function(string $item): bool;
```

Would provide a lot more value to PHP, as well as allow existing code to continue to work, until in a future version of PHP the whole callable type could be removed.

See also the [Function interfaces](https://wiki.php.net/rfc/functional-interfaces) RFC.

### Non-beneficial changes

Similar to the attitude of 'small ratio of reward to work', there is a separate phenomenon where the current maintainers think that the RFC provides no value, so no matter how little work it is, they still don't want to make that change.

Some of the examples of this were:

 * Deprecating {} for strings and arrays.
 * Short PHP tags.
 * Scalar types.
 * Using a top level namespace for core PHP functions (other than for code strongly coupled to the PHP engine). 

### Duplicating features to save a few characters

PHP is relatively verbose compared to some languages. There are [some suggestions](https://wiki.php.net/rfc/short-functions) that PHP [would be better](https://news-web.php.net/php.internals/116231) if fewer characters were needed for some things.

However the tradeoffs for that would be:

* more complexity in the engine.
* more complexity in static analysis tools.
* more stuff to learn for new programmers.

Most people don't seem to feel that being able to write slightly fewer characters is worth that much.

### Ideas that make code harder to reason about

One of the strengths of PHP is that code written in it is usually reasonably easy to understand. For example the Doctrine ORM is written in PHP, so that if you ever encounter unexpected behaviour in it, you can debug the PHP code yourself.

That is much better than Java's Hibernate ORM, where sometimes unexpected behaviour happens at [the VM level](https://stackoverflow.com/a/10808563/778719) which is much harder to debug.

Any RFC that makes code harder to reason about is less likely to be passed. Two examples of this issue are reusing keywords, and context dependent parsing.


#### Reusing keywords

This is an example of an existing choice in PHP being 'sub-optimal'. The static keyword in PHP can mean any of:

* static method - a method that is bound to a class, not an instance of that class.

* static property - a property that is bound to a class, not an instance of that class.

* static variables - a local variable that persists across multiple calls to a function.

* static closure - Skips binding `$this` to a [closure created within a class](https://www.exakat.io/5-usages-of-static-keyword-in-php/).

* static classname - aka the late static binding classname

Which is approximately three meanings too many.

#### Context dependent parsing

As part of the discussion around [Attributes](https://wiki.php.net/rfc/attributes_v2) some suggestions were made that the syntax could be made to be parser context sensitive to avoid the problem of the @ character already having meaning in PHP e.g. something like:

```
@bar(123)
function foo()
{
    @bar(123);
}
```
 
where `@bar(...)` immediately before a function declaration would be parsed as an annotation, and `@bar(...)` inside a function would be parsed as a silenced function call. This context dependent meaning is confusing.



### Not being compatible with the PHP release schedule

PHP doesn't not strictly follow semver, but the project does attempt to minimise semver violations.

This restriction on releases makes including libraries that would need a different release schedule be a logistical nightmare. Here are two examples.

#### New libraries that have rapidly a evolving API 

Most new libraries go through initial periods where the API is evolving rapidly. Later, when the library has matured the API will naturally change less frequently.

As a API change is either a minor or major BC break, this means either the library will evolve very slowly, or there will be unexpected BC breaks in each version of PHP. Neither situation is good.

It is much better for new libraries to be shipped separately from core. Though we also need to make it easier for people to install extensions...

#### Imagick extension

The Imagick extension is a relatively thin wrapper around the ImageMagick library. The ImagickMagick library does not follow semver.

The version numbers for ImageMagick look like "7.0.10-3", which is "major.minor.bugfix-patch_number". However there are sometimes BC breaks in minor versions, and also BC breaks between patch versions. Trying to handle these changes in a way that is compatible with PHP's release schedule would be a very complicated thing to do.


## Things people will consider as reasons to vote for an RFC

### Clear upgrade path

PHP internals values backwards compatibility more than other projects typically do. Where changes that break backwards compatibility need to happen, having a clear upgrade path from the current behaviour to the new behaviour makes it much more likely the RFC will be accepted.

This is a large topic, but two examples are:

#### Spreading BC breaks over multiple versions

For years, the behaviour of [ternary operator associativity](http://phpsadness.com/sad/30) was a source of sadness.

> The ternary operator is left-associative and therefore behaves entirely incorrectly

Rather than trying to fix this in one step, the [Deprecate left-associative ternary operator](https://wiki.php.net/rfc/ternary_associativity) RFC made it so that using nested ternaries without explicit parentheses will throw a deprecation warning.

This means that in a future version of PHP, we could drop the requirement for parentheses and allow for the default behaviour to be right-associative (aka what people expect).

#### Allowing code to work on multiple versions

For example, renaming a class should have at least one version where both the old name and new name is supported.

i) User has code running on version x.y of PHP that uses the old name, as that is the only name available.
ii) User code runs on version x.(y+1) of PHP that still uses the old name, to check that all their code works on that version of PHP.
iii) The user changes any use of old names on x.(y+1) to the new name.
iv) Old names can be remove in version x.(y+2)


### Being written clearly 

There are couple of things that should be covered in an RFC.

#### Explain why something is a problem

This might seem obvious, but having a clear description of why the current situation is sub-optimal makes it much more likely that the conversation will be conducive to the RFC being passed.

#### Explain why it should be solved in PHP core

Not all problems can or should be solved in PHP core. As well as the preference for 'solving it in userland', there are some problems that just can't be solved adequately in PHP core.

An example of this is the various 'taint' RFCs. Although having these in PHP core would help guard against trusting user input, there would still be cases where it wasn't obvious what was and wasn't user input, which means that people would still need to guard against trusting that data. 


#### Explain why the solution proposed is likely to be the right one

Putting it simply, an RFC needs to explain why an idea is the right one, rather than just something that could be done. 

If this is done well, it will limit how many alternative suggestions people suggest, as well as make people more comfortable adding to core, where it will need to be maintained for many years. 


## Why I wrote this document

PHP is a language that is evolving, and so how people view an idea will also evolve over time. A good example of this is the attitude towards union types.

The RFC [Union types](https://wiki.php.net/rfc/union_types) in 2015 failed 11 - 18.

The RFC [Union types v2](https://wiki.php.net/rfc/union_types_v2) in 2019 passed 61 - 5.

I believe a large part of the change in attitude was that people had grown more used to working with scalar types, and using static analysis tools like PHPStan, Psalm and Phan. That experience made it easier for people to understand that union types solved a problem in a good way.

Being able to understand how other people think greatly increases the chances that you can have a productive conversation with them, and so greatly increases the chances we can continually improve the language.