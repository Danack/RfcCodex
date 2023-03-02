

## Talk about problems before talking about solutions

As in, people should be asking "exactly what problem is this solving?" and then making sure that:

1. the scope of the problem is reasonably well understood.
2. most people agree that it is a problem that should be addressed.
3. there aren't better problems to solve 

See also, the [XY problem](https://meta.stackexchange.com/questions/66377/what-is-the-xy-problem).

## Don't ask "why don't we just?"

"Asking why don't we just" is almost always a bad way of finding a solution, as it puts the onus on other people to find reason against an idea, and so allows 'ungood' ideas to slip through. In PHP, the conversation should always be "we'll do this, because it's the right solution".

In other projects, that don't have a fixed release schedule or such a large user-base, and are more willing to making BC breaks, using temporary solutions can useful in exploring the problem space.

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

It's perfectly fine to use the positive emoji in conversation. They are a light-weight way of giving approval without needing to come up with some possibly cheesy words. For example:

Q) Does this look good to merge?
A) 👍

The thumbs-up makes the person who asked the question feel good, and completely answers the question without any needing any more detail. 


The problems with negative emoji are that they make people feel bad and they stop the conversation without leaving it anywhere to go.


Q) Does this look good to merge?
A) 😕

Not only does the question asker feel a bit down from having a negative response to a question where the would have assumed getting a positive response (because if they knew of any outstanding issues, they wouldn't of asked) but also, the negative emoji places the burden of continuing the conversation on them.

Or to put all of this far more pithily "[What the hell is 🥺? Use your words,](images/I_dont_speak_bottom.jpg)".
