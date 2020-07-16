# Strings and encoding 

## General idea

Strings in PHP are a little bit terrible.

In particular the way that the standard string functions like strlen are not aware of text encodings is 'not good'.

Actually strings are pretty terrible in most computer languages
https://dev.to/awwsmm/why-no-modern-programming-language-should-have-a-character-data-type-51n


## Locale aware

> No, the problem results because lowercase i (in most languages) and uppercase I
(in most languages) are not actually considered to be the upper/lower variant of
the same letter in Turkish. In Turkish, the undotted ı is the lowercase of I,
and the dotted İ is the uppercase of i. If you have a class named Image, it
will break if the locale is changed to turkish because class_exists() function
uses zend_str_tolower(), and changes the case on all classes, because they are
supposed to be case insensitive.


## Hurdles to overcome


### Hurdle 1 


## Forecast


## Notes



