
# How to have better discussions

Having productive conversations is quite hard. It's really easy to fall into  patterns of conversations that produce a lot of words, but don't provide useful outcomes.

What follows are suggestions about how to avoid, or at least not get stuck in, conversations that are unlikely to be productive.

## Talk about problems before talking about solutions

As in, people should be asking "exactly what problem is this solving?" and then making sure that:

1. the scope of the problem is reasonably well understood.
2. most people agree that it is a problem that should be addressed.
3. there aren't better problems to solve 

See also, the [XY problem](https://meta.stackexchange.com/questions/66377/what-is-the-xy-problem).

## Don't ask "why don't we just?"

"Asking why don't we just" is almost always a bad way of finding a solution, as it puts the onus on other people to find reason against an idea, and so allows 'ungood' ideas to slip through. In PHP, the conversation should always be "we'll do this, because it's the right solution".

In other projects, that don't have a fixed release schedule or such a large user-base, and are more willing to making BC breaks, using temporary solutions can useful in exploring the problem space.

## Identify arguments about aesthetics and avoid them

A lot of energy is spent in programming arguing about small design decisions. A lot of the time programmers will argue a particular choice is 'better', but are unable to say for exactly what reason it is better.  

At least some of the time, they will actually be having either a positive or negative gut reaction to a design choice, but aren't able to recognise that they are doing that.

Instead they will argue that a different API/syntax is more naturally 'elegant', 'intuitive', or other positive attribute. These types of arguments very often boil down to "I prefer this choice because it matches my experience". Other times it comes down to, "I prefer this choice because the other one is too boring".

## Identify neophytes and educate them

Sometimes neophytes[^neophytes] will learn some stuff, and proclaim it as the One True Way and go round the internet trying to pick fights with anyone who would dare to disagree.

Although, you can use them as an entertaining punching bag by showing how naïve they are, that isn't really a productive conversation. I mean it can be fun stress relief...but it doesn't have a useful outcome, and may result in them becoming annoyed.

Instead of that, actually taking the time to comprehend what the neophyte has just learned about (and so is excited about), and pointing out where either the limitations of it, or how they might be excited about it now, but there is still more to learn, is likely to be a more productive conversation long term.


Some good rules to follow are:

* choose the most boring API that is acceptable. People will often object to this, wanting an API that makes them feel cleverer.
* "the person who has thought the most about the problem, gets to choose the API". Or at least that seems to be working for PHP.

## Don't respond to ideas you don't like the same day

It's quite normal for people to have instinctive negative reaction to a proposal. If you respond the same day as you first read a proposal, it seems you are likely to 'bake in' you negative reaction to the idea, and it becomes permanent.

If you leave a day or two to pass before responding, the idea probably won't seem quite so bad, and you'll be slightly more open to having a productive discussion.

If you still don't like an idea, it can be worth asking yourself "under what circumstances would I like the idea" or "what has the person who is proposing the idea experienced that led to them proposing it?"

One example of this was the proposal to add a new `printf` function that automatically appends a newline character. For someone who is coming from a programming language where each `echo` automatically does have a newline, the lack of that in PHP is a surprise.

## Don't use negative emoji in conversations

From the Github emoji reaction set, I would classify emoji as positive/negative:

### Positive

* 👍 :thumbsup:
* 😄 :smile:
* 🎉 :tada:
* 🚀 :rocket:
* ❤️ :heart:

### Negative

* 👎 :thumbsdown:
* 😕 :confused:
* 👀 :eyes:

It's perfectly fine to use the 'positive' emoji in conversation. They are a light-weight way of giving approval without needing to come up with some possibly cheesy words. For example:

Q) Does this look good to merge?
A) 👍

The thumbs-up makes the person who asked the question feel good, and completely answers the question without any needing any more detail. 

The problems with negative emoji are that they make people feel bad and they stop the conversation without leaving it anywhere to go. For example:

Q) Does this look good to merge?
A) 😕

Not only does the question asker feel a bit down from having a negative response to a question where the would have assumed getting a positive response (because if they knew of any outstanding issues, they wouldn't of asked) but also, the negative emoji places the burden of continuing the conversation on them.

Or to put all of this far more pithily "[What the hell is 🥺? Use your words,](images/I_dont_speak_bottom.jpg)".

## Understand other people's position before trying to persuade them

So.

Some of the 'discussions' on the PHP internals have been completely non-productive. Some of the time this is because one side of the 'discussion' has completely failed to understand what other people have been saying. 

Quite a few of these discussions have involved BC breaks, where a few long term PHP users have said things similar to "the PHP maintainers must be idiots because they have no idea what they are doing".

Although some BC breaks could be done more smoothly[^smoother_bc_breaks], the vast majority of the time, the people who make up PHP internals have considered the BC breaks very carefully, and decided that, "yes although this is going to cause upgrade pain for some users, it's still worth doing".

When the people who object to the BC break turn up to try to undo the BC break, they often seem to be unable to comprehend that the decision was made deliberately, with full consideration of the consequences. This leads to not particularly productive conversations, as one side is unable to even comprehend the state of mind of the other side.

Obviously, this doesn't apply to people who are a ['Known Idiot'](). When someone has said stupid things frequently enough, it becomes a better to rule to completely discount their opinion rather than taking any effort to understand it.

If there is any utility in their words, it is likely someone else will repeat it in a more intelligible phrase.

[^smoother_bc_breaks]: Although I agree with most of the BC breaks in PHP core, I think some of them could have been done a lot more smoothly, to make life easier for end-users. See the 'Clear upgrade path] in [RFC Attitudes](etiquette/rfc_attitudes.md) for examples.

[^neophyte]: A programmer who is more experienced than a noob, but not that much more. They have a tendency to think they are more experienced than they actually are. 