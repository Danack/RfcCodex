# PHP project coordination

This is an experiment that attempts to make it much easier for people to find things to work on for PHP internals, related infrastructure, extensions and most other non-userland things.

Due to it being an experiment, it's currently outside of the PHP project's infrastructure. 
 
 
 on my own server. PR's accepted at https://github.com/imagick/imagick for the file https://github.com/Danack/Imagick-demos/blob/master/public/stuff_to_work_on.php.

## RFCs to work on


### Union Types v2

Proposal for the addition of union types T1|T2|.... There has been a previous proposal on this topic, which has been declined.

Link: https://github.com/php/php-rfcs/pull/1

## Internal stuff to work on

## Resource to object conversion in extensions

The 'resource' type was needed before PHP had classes to represent non-trivial types. However since PHP now has classes, it would be good to replace the resource types used internally.

Link: https://github.com/php-pecl/ProjectCoordination/blob/master/change_resource_to_specific_type.md

### Annotate internal function types

We now have the capabilty to add type information to PHP core functions. The work is not difficult, but there is a large amount of it.

Link: https://github.com/php-pecl/ProjectCoordination/blob/master/annotate_internal_function_types.md

## Infrastructure stuff to work on


### Move documentation from SVN to Git/github

Editing the documentation is currently quite difficult. Moving it to git/github would make it easier.

Link: https://github.com/phpdoctest/meta

## Bugs to work on

### PDO -> PDO driver error conditions

There is an oversight between PDO and some PDO drivers on how certain error conditions are missed. This leads to some error conditions having their error message or exception not triggered: https://bugs.php.net/bug.php?id=77490

Link: https://github.com/php/php-src/pull/4288


