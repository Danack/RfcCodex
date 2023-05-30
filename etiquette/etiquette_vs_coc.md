
# Etiquette in open-source projects

There are multiple levels of "getting along" with other people.

Most projects have a code of conduct, frequently the '[Contributor Covenant](https://www.contributor-covenant.org/). A Code of Conduct tries to define the base level of behaviour that the members of a project find acceptable, where any violation of those rules by someone, puts their continued participation in that project at risk.

That isn't enough.

Merely avoiding "completely unacceptable" behaviour isn't good enough to make other people want to continue talking to you. For projects to be successful, and for people to be successful in projects, the people taking part in them need to enjoy interacting[^enjoy_interacting]. with each other.

There are many patterns of communication that can be annoying to some people. The rules or guidelines to follow to avoid being annoying are generally known as etiquette.

## Etiquette, attunement and discordance 

When new contributors arrive at an open source project, there are two common patterns, attunement and discordance.

New contributors to an open source project will often make small mistakes or not follow standard ways of working.

For PHP this could include things like:

* include code-style commits in a PR that also makes functional changes.
* merging instead of rebasing their branch.
* targeting the wrong branch in a PR.
* changing some subtle behaviour of some code where people are likely to complain about a BC break.

The maintainers handling their PR will give the new contributor feedback in a gentle way:

> Hey, this PR changes the behaviour of the function. It needs to target 'master'.

How this feedback is processed often follows one of two paths: 

### Attunement

Over the course of weeks, months, years new contributors will earn the respect of maintainers, and the maintainers will develop a simpatico relationship with the contributors; knowing what the skill level and attention to detail the contributor has, and so what level of care needs to be given to reviewing their PR. 

Without having a formal discussion, the new contributor will be accommodated and acclimatised to the way that the team works, and also influence and change how the team works. 

### Discordance

* just not responding.
* arguing whether the thing is appropriate 


TODO
TODO
TODO


### Etiquette frustration

This feedback _can_ be done poorly. It is possible to give people feedback in a way that makes them feel like shite, but mostly the feedback is given and accepted and the new contributor will learn the subtle working rules for the project.

Unfortunately some people are just really bad at picking up 'suggestions' and bristle against them.

The PHP project (and most online communities) don't have a good way of handling situations where people who are not taking etiquette-hints, and need a quiet talking to.

When someone is breaking etiquette rules, despite people having made many suggestions to them, the pattern is typically this:

* someone starts getting annoyed by someone's behaviour, and it starts getting on their nerves.

* they start noticing that other person's behaviour more and more, and then they also start getting frustrated that other people either aren't also noticing it.
* they say something a bit extreme both to try to get other people more worked up by the person's behaviour, and also as a stress release.
* if they do that release in public, to the person, it makes resolving the conflict even harder.

The problem with this pattern are these:

* it allows people who are more sensitive to 

TODO
TODO
TODO



## The difficulties of etiquette

Implementing and enforcing a Code of Conduct is difficult enough. Unfortunately, trying to get people to follow an etiquette guideline is even more difficult.

Some of the difficulties of etiquette compared to a Code of Conduct are:

### Etiquette 'rules' are not obvious

You need to be on the receiving end of bad behaviour to realise an etiquette rule exists

TODO
TODO
TODO


### Etiquette 'rules' are not fixed and definitive

TODO
TODO
TODO


### Violations are understandable and sometimes needed

Sometimes people are just in a really bad mood. This can be caused by things outside of the project IRL, e.g. a pet dying, or it can be caused by things inside the project, e.g. a single person repeatedly breaking the build or trying to commit a change they've been told not to.

Maintainers are people.

Expecting maintainers to never lose their temper is an inhuman burden to place upon them. I would go so far as to say that having that expectation is a form of abuse. 

I have heard of at least occurrence where a person was deliberately harassed by someone breaking etiquette rules, but not the Code of Conduct rules, to drive them out of the project. Humans, eh?

### Depend on interpersonal relationships

And interpersonal relationships are fractally complicated; each detail of the relationship can change whether a certain behaviour is going to be viewed positively or negatively.

Someone who you know and like will be able to speak to you without causing offence in ways that would cause huge offence if the same things were said by someone you don't know.

### Informing people about etiquette rules is confrontational

Almost by definition, letting people know they have violated an etiquette rule is going to be confrontation, as the only situations that needs to be done are:

* the person is not an arsehole, but was unaware of the etiquette rule, and assumed that their behaviour was acceptable. Telling someone "Hey that thing you thought was okay, actually isn't okay" is a confrontation as you are challenging assumptions they have made. 
* the person is an arsehole, and doesn't care about your etiquette rules. You bet that's a confrontation. 
* you've got the wrong end-of-the-stick and are over-reacting, or the etiquette rule doesn't actually apply in this situation. There are a non-zero number of times I have gone to tell someone "don't violate this rule" and regretted doing so[^zero_isnt_the_goal] which is going to happen because etiquette rules are fuzzy.  

The thing that makes this problem even worse is that some forms of communication are not possible on the internet.

In real life, if you see someone be a bit of an ass, and do something that is slightly inappropriate, you are able to approach them and have a quiet word in their ear, saying something like "Hey, the thing you just did is not cool". This can lead on to a conversation where the reason why the behaviour is problematic, and the two people can look each other in the eye. 


## Other resources

Online etiquette is a fundamental problem facing humanity. Here are some resources that I think help explain the phenomenon.

### Eternal September

The wiki page on ['Eternal_September'](https://en.wikipedia.org/wiki/Eternal_September) is worth contemplating.

Every generation needs to be educated as to how to behave online to avoid pissing people off.

In my opinion, learning how to behave was difficult enough when most communication was done face-to-face and only a small amount was done via writing. These days almost anyone on the planet send me a message that is either subtly or obviously insulting.

This phenomenon needs to be recognised not just as a Problem, but also as an Eternal Problem; something to be coped with rather than solved. btw, have you read Systemantics yet?

### Systemantics

Most people instincts are just wrong when it comes to how Systems and Problems behave.

The book Systemantics will help you understand how Systems behave, and how Problems are meant to be coped with, rather than solved.

### Working in public

[Working in Public: The Making and Maintenance of Open Source Software](https://www.amazon.co.uk/Working-Public-Making-Maintenance-Software/dp/0578675862) is a reasonably good book that documents how much of a burden of educating programmers to how to fucking behave is falling to Open Source maintainers.

The short version is this; I strongly doubt the morality of Open Source. Despite the obvious huge benefits to humanity, I am still not sure it is a moral good.

### The history of Cyberville

Cyberville was a very early online forum, created by Stacy Horn in 1990 and still functioning. But only accessible over telnet/ssh...

The history and behaviour is very well documented in, [Cyberville: Clicks, Cultures, and the Creation of an Online Town](https://www.amazon.co.uk/Cyberville-Clicks-Cultures-Creation-Online/dp/044651909X)

Most of the patterns of behaviour are analogous to those I have seen and experienced.

[^enjoy_interacting]: "enjoy interacting" is possibly too strong a phrase. The test is more "do they learn to fear interacting with a particular person. For anyone who hasn't gone through the harrowing that is being an open source maintainer, the phrase 'fear' might seem quite strong. It is not. Being an open source maintainer can be dreadful experience. See [Working in public]() for more details.

[^zero_isnt_the_goal]: For both being right about "telling people they are violating etiquette rules" and "bank manager making loans to startups" the goal isn't being wrong zero percent of the time. If a bank manager is _never_ wrong and never makes a loan to a company that goes on to become bankrupt before the loan is repaid, that means they are being too safe and are refusing loans to some companies that actually should have been invested in.

If you are _never_ wrong about pointing out code of etiquette violations, that means you are being too safe and letting some behaviour slide that should have resulted in having some words.



