# RFC etiquette

There are some behaviours that I see people do when discussing RFCs, and other software projects (both open source, and closed source) that I think are either subtly but incredibly rude, or otherwise do not help people have a productive conversation.

## Don't publicise draft work

The site wiki.php.net/rfc is a tool that is meant to allow people to draft RFCs and share the idea with other people who want to work on the RFC before it is a polished idea, and before it is ready to be presented to the world.

Having someone other than the RFC author announce the RFC on internals before the author thinks the RFC is ready for comment, is an act of sabotage.

## Do try to talk about the problem before talking about possible solutions

Some RFCs don't make it clear what problem it is they are trying to solve before proposing a solution.

This leads to the discussions being not productive as if the problem was introduced first.

Some people might disagree on what the exact problem is, or disagree that it even is a problem that needs solving to begin with. If people can't clearly understand that there is a problem that needs solving, then the discussion about possible solutions is going to be incredibly heated, with people not understanding the other side.

Some people might offer different solutions to the same set of problems. If the original RFC has skipped over defining the problem clearly, then it makes it a lot harder for people to suggest alternative solutions to the same problem.

Additionally, although some sets of problems may be closely related, by talking about the problems clearly, they might be broken up into separate problems to be solved by separate RFCs.


## Don't volunteer other people for huge amounts of work

The response to some RFCs has been to suggest that the RFC doesn't cover enough scope, and that the RFC author should make the RFC be a lot bigger.

While that sounds reasonable on the surface, the amount of time people have to work on PHP RFCs is often limited. Having someone tell you "yeah, you need to contribute a few months of work" is a dick move.

It's okay for RFCs to be small in scope, so long as they are self-contained. It would only be appropriate to say that the RFC needs to be bigger if it would otherwise leave new inconsistencies in the language that would need to be resolved before the next release.


## Don't say that other people's use cases are invalid

The response to some RFCs is disappointing. Rather than accepting other people as being individuals with different priorities and motivations, some people on internals have responded with "I don't want to use this proposed feature, therefore I don't think any people should use this feature".

It's okay to question how many people would need a feature, but when you have someone saying "I want this feature", and your response is "I don't believe you actually want that feature", then you've crossed a line from being reasonable to arguing based on Solipsism, which is not going to lead to a productive discussion.














