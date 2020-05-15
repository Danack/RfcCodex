
# SPL notes

Below are some notes on the issues with the SPL library.

In addition to those, there is a general problem that some APIs need to evolve separately from the [PHP release schedule](https://github.com/Danack/RfcCodex/blob/master/rfc_attitudes.md#not-being-compatible-with-the-php-release-schedule).

If a library it tied to the PHP release schedule, any mistake in the design of the  API is locked in until the next minor release.

Additionally, it means that people can't run their application on two versions of PHP. That makes upgrading from one version of PHP to another much more difficult than it would otherwise be.

## Iterators

These are quite useful, though possibly could do with a better developer experience around using them.

The file related ones are best avoided though - see File Handling below.

## Datastructures

People tend not to use them, but it is hard to express exactly why. 

It is partly due to some issues in their implementations. For example that the function [splpriorityqueue.recoverfromcorruption](https://www.php.net/manual/en/splpriorityqueue.recoverfromcorruption.php) exists is a pretty bad sign. 

There are a better set of datastructures available in the [Ds extension](https://github.com/php-ds/ext-ds).

I think possibly it is related about the difficulty in converting from arrays to custom data structures and back again, being a not good experience.

## Exceptions

The attempt has two fundamental mistakes in my opinion.

First, I think all exceptions should extend a base exception that is specific to library that the code is in. e.g.  

try {
  $image = new Imagick("foo.png");
  $image->someMethodThatMightThrow();
}
catch (ImagickException $e) {
  // This catch should be guaranteed to catch all exceptions
  // that could possibly be thrown by 'someMethodThatMightThrow'
}

Any exceptions to that rule, like a TypeError that is not caught internally and rethrown with an Imagick specific version, should be considered as a bug.

Second, having a hierarchy of exceptions that builds up more specific meaning is something that has a strong aesthetic appeal to developers, but has no actual benefit. Other than extending a base exception for that library.


## File Handling

There are multiple issues for them. They are not well designed classes, are kind of difficult to work with, and also some of the assumptions in them are unsafe. For example cloning a FileSystemIterator assumes that the directory has not changed: https://bugs.php.net/bug.php?id=69291

More fundamentally I think these classes are also a mistake. Here is a quote from a paper by [Edsger W. Dijkstra](https://www.cs.utexas.edu/~EWD/transcriptions/EWD03xx/EWD340.html):

> the purpose of abstracting is not to be vague, but to create 
> a new semantic level in which one can be absolutely precise.

I think this can be turned round the other way. If an abstraction does not provide a new, more precise semantic level, then it does not provide any value.

Those classes are not simpler to use than the low level unix file handling routines. And so they do not provide any value over just using the low level functions. In fact they are harmful as they hide some details that you probably want to know about.

That is an opinion that I think also applies to the idea of providing an OO api to the functions for handling http requests, e.g. get_headers(). Although they could do with improvement through having less magic, and being more complete (e.g. why isn't there a get_body() function?) putting them all in an OO api seems the wrong thing to do to me.





