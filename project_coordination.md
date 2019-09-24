# PHP project coordination

This is an experiment that attempts to make it much easier for people to find things to work on for PHP internals, related infrastructure, extensions and most other non-userland things.

Due to it being an experiment, it's currently outside of the PHP project's infrastructure. 

If you have an item you would like added please provide:

* a title
* a short description
* a link to where the work is described in greater detail, and people can ask questions.


The link to where the work can be discussed could be bugs.php.net, a github/gitlab repo, a slack channel. Whatever you think is appropriate for the piece of work being discussed. 

The main thing is that people should be able to see what needs to be done, and discuss it.


## RFCs to work on

### Union Types v2

Proposal for the addition of union types T1|T2|.... There has been a previous proposal on this topic, which has been declined.

Link: https://github.com/php/php-rfcs/pull/1

## Internal stuff to work on

## ext/* - Resource to object conversion in extensions

The 'resource' type was needed before PHP had classes to represent non-trivial types. However since PHP now has classes, it would be good to replace the resource types used internally.

Changing resources to objects only has an extremly minimal BC impact which is limited to code using the ``is_resource()`` and
``get_resource_type()`` functions. This is due that a resource is produced as a return value from a function and passed as a parameter
to all relevant functions.
This means that these changes can occur in between minor version as can be seens with the resource to object migration for the Hash
extension in PHP 7.2. [1]

Link: https://github.com/php-pecl/ProjectCoordination/blob/master/change_resource_to_specific_type.md
[1] https://www.php.net/manual/en/migration72.incompatible.php#migration72.incompatible.hash-ext-to-objects

### Core - Annotate internal function types

We now have the capabilty to add type information to PHP core functions. The work is not difficult, but there is a large amount of it.

Link: https://github.com/php-pecl/ProjectCoordination/blob/master/annotate_internal_function_types.md

### ext/phar - Phar Extension - Need OSS Fuzz coverage

OSS Fuzz aims to find bugs by randomizing ("fuzzing") input. Phar has had a few bugs owing to edge cases in path processing and, being widely distributed form of PHP code, would benefit from fuzz testing. See https://github.com/google/oss-fuzz/tree/master/projects/php

Link: https://bugs.php.net/bug.php?id=78571

### ext/imap - Imap Extension - Reboot

The IMAP extension, while used across many open projects, performs poorly when compared to userspace implementations like Horde/Imap_Client. The library on which it is based (c-client) is unmaintained since 2011. And, there are a ton of bugs. We need to formulate a plan to either (a) accept the performance/features for what they are and just fix bugs or (b) reboot the extension from the ground up. Help wanted to steer and implement.
 
Link: https://bugs.php.net/bug.php?id=78572

## Infrastructure stuff to work on

### Move documentation from SVN to Git/github

Editing the documentation is currently quite difficult. Moving it to git/github would make it easier.

Link: https://github.com/phpdoctest/meta


### Setup easier to use wiki

The number of people who are able to edit our wiki are very small due to how hard it is to collorate on documents, as well as how difficult it is for people who don't have a php.net account to make changes. We need to keep the RFCs and voting on the wiki, due to needing the karma system to check who can vote. However pretty much everything else could be migrated to make it easier to collaborate.

Link: https://github.com/brzuchal/php-dev

### Smoother PECL signup process

Currently the pecl signup process is heavily 'gate-keepered'. People sometimes wait weeks for their account to be approved. We could change the workflow, so that people have to submit a compilable repo, and then after that their account is either automatically approved, or the number of people who can approve those validated signup requests should be increased.

Link: https://github.com/php-pecl/ProjectCoordination/blob/master/pecl_signup_allow_full_repos.md

## Bugs to work on

### PDO -> PDO driver error conditions

There is an oversight between PDO and some PDO drivers on how certain error conditions are missed. This leads to some error conditions having their error message or exception not triggered: https://bugs.php.net/bug.php?id=77490

Link: https://github.com/php/php-src/pull/4288


