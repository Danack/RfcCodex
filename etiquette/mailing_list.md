# Mailing list etiquette guidelines

The [official mailinglist rules](https://github.com/php/php-src/blob/master/docs/mailinglist-rules.md) provide a set of rules that should be followed. This document goes into a bit more detail for some of those rules, and a few subtleties.

The PHP mailing lists are one of the tools used for communication in the PHP project.

Mailing lists work best when people follow similar guidelines as appropriate for communicating on newsgroups. As many people might not have used newsgroups recently, here are a set of etiquette guidelines.

## General advice

### Read a whole thread before replying

Although it's tempting to read through a thread and respond to each message as you read them, this can have some downsides.

Someone may have already asked the same question you were about to ask, or made the same comment, and so duplicating that comment doesn't provide any value. 

Other times, there may be two very similar comments which can be responded to in a single message.

### Take time drafting your responses

Depending on the level of interest in a topic, your response may be read by hundreds or thousands of people.

Taking the time to make your communication be as clear as possible can save a significant amount of time of PHP developers.

In particular, if you're not able to spare enough time on one day to give a considered response, then it's better to wait until you do have time, rather than giving a ill-considered response.

### Don't send too many messages per day

Exactly how many is too many is hard to say, 

### Start new threads when topics drift

### Almost never send partial messages

Occasionally people will reply to someone else's message with something along the lines of:

> I'm out of the office right, now. I'll take a look at it tomorrow.

PHP Internals is a mailing list, not a real-time chat. It's okay to take days to respond to a message.

## How to reply

* Quote the right amount and properly.
* Format quotes properly
* Do not top-post. Instead place your reply underneath text you are replying to.

This is an evolution from https://www.netmeister.org/news/learn2quote.html

### How much should I quote?

As little as possible, without losing context.

People reading the thread will understand the general topic under discussion, and so should be able understand which point you're referring to by only a short piece of quoted text. On the other hand, the quotation should not be so short that it is unclear to what the author is referring to, or so that it may even appear in a totally different light.

Text to which you are not responding should be deleted. e.g. if you responding to paragraph from the middle of someone's email, then both the text preceding that paragraph, and the text that follows it should be deleted. 

Email signatures should always be deleted. Repeating them does nothing to add to the conversation. 

### Quoting attribution

Place the name of the person you are quoting before the text, followed by a wrote:

```
User C. wrote:
> Lisa wrote:
> > John wrote:
> > > blablabla
> > blubberblubber
> laberlaber
```

It's not necessary to include the date and time, except when replying to very old messages where making it obvious that you're resurrecting an inactive conversation is useful.

Most email clients will include the date and time when replying by default, it's fine to leave the date and time there.

Some conversations can span multiple locations, e.g. an RFC text, Github pull-requests or a mailing list. If you're quoting some text, that was written on the same communications channel that you're responding on, there's no need to specify the location of the quoted text, as people should be able to find it. 

But when you're quoting someone from a different communications channel, a link to the source of the quote should be included. 

Example, quoting a comment from a PR on the PHP internals mailing list should include a link to the PR, or the precise comment:
```
John wrote on https://github.com/php/php-src/pull/3:
> This is a BC break, it probably needs an RFC
```


### What is top-posting?

It is when you write your reply above the text you are quoting.

```
Ok cool. I'll draft one up.

John wrote on https://github.com/php/php-src/pull/3:
> This is a BC break, it probably needs an RFC

```

### Why should I place my response below the quoted text?

People read top to bottom. 

If it was the other way round, and your response is above the text you are responding to, people would need to scroll past your response, read the previous text, and then scroll back up.

### But my email client defaults to putting replies above the message.

Email clients are optimised for communication that is either 1-to-1 or in a small group of people. In small groups it is easy for everyone to be fully aware of the context of each message.

In a mailing list, your messages are read by many more people, and there are many more conversations happening at once. People aren't going to remember the exact state of each thread.

### Place a blank row between the quoted text and your response

It makes it much easier to see where the quoted part ends, and your response begins.

```
John wrote on https://github.com/php/php-src/pull/3:
> This is a BC break, it probably needs an RFC

Ok cool. I'll draft one up.
```

### How do I indicate text has been edited out?

When you remove individual words or sentences from the middle of quoted text, indicate there are removed words with one of "[...]", "(...)", "<snip>" or "...".

#### Example removing words from the middle of a paragraph:

```
John wrote:
> Lorem ipsum dolor sit amet, consectetur adipiscing elit. [...] In hac habitasse platea dictumst.
```

#### Example removing whole sentences/paragraphs from a quoted block.

```
John wrote: 
> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus tempor massa eu vestibulum placerat. 
> ...
> Interdum et malesuada fames ac ante ipsum primis in faucibus. In hac habitasse platea dictumst.
> ...
> Praesent dictum mi ut est convallis, et posuere metus tempor.
```

Note, if you're quoting a whole sentence/paragraph without any edit, it's not necessary to indicate that there was text before or after the part you're quoting. 


### Should I correct spelling errors in quoted text?

In general, no. People spell some words differently in different parts of the world, and 'correcting' words that they have spelled correctly is irritating.

There can be exceptions for this, for example fixing a broken link, or when someone's name has been misspelled, then it can be okay to correct it.

## Other advice

### Workflow for reducing internals stress

Leaving a window open with internals on it all day, is not good for your mental health. So instead of that I choose a regular-ish time of day that I consider interacting with internals, and then I:

1. Decide if I have the energy to read internals. If I don't, then I don't.

2. Read all the new emails for the threads I care about. As I do this I make notes of which threads I plan to respond to. Mark all emails read, having skipped over threads I don't care about.

3. Write drafts of emails in notepad, or other similar text editor. Drafting replies in an editor other than the email client means that I avoid hitting 'send' too early. It also means I can pause editing one particular email if I get writers block on it.

4. Go back to my email client, find each message I am going to respond to, and copy and paste the text from the editor.

5. Close the window that has internals on it, so I don't accidentally spend more time reading than I planned to.

### Turn off notifications

Having the rest of your day interrupted by replies to your email, is a great way to get stressed out. You should leave reading replies until you next choose to spend time reading internals, rather than having that choice made for you. 

In Gmail, this can be done by creating a filter that skips the inbox.

### It's natural for some discussions to not end in consensus

a.k.a. you can't always 'prove' someone wrong. 

People base their decisions on multiple things including their own experiences and understandings of trade-offs. Trying to force a conversation to reach a conclusion by asking things like "What would need to be changed to make you support this RFC?", does not often get the conversation to the conclusion.

Sometimes, people will just not like an RFC and not be able to express why they don't like it.




