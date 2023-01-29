# RFC etiquette

There are some behaviours that I see people do when discussing RFCs, and other software projects (both open source, and closed source) that I think are either subtly, but incredibly rude, or otherwise do not help people have a productive conversation.

## Don't publicise other people's draft work

The site wiki.php.net/rfc is a tool that is meant to allow people to draft RFCs and share the idea with other people who want to work on the RFC before it is a polished idea, and before it is ready to be presented to the world.

Having someone other than the RFC author announce the RFC on internals before the author thinks the RFC is ready for comment, is "not okay". If you discuss an RFC on internals before the author thinks the RFC is ready to be discussed, the only thing that could achieve is to make the conversation less productive.

If you want to influence how the RFC is drafted, it is appropriate to reach out to the RFC author, and offer to help them. 

## Do open new RFCs rather than re-use existing documents.

When revisiting ideas, and the previous version of an RFC hasn't been discussed in a long time (e.g. more than 6 months) or when a previous version was declined by vote, it is preferable to open new documents on the wiki, rather than re-use existing documents.

We have rules in place about when RFCs are allowed to be put into voting. If a RFC document has been re-used there could be some confusion about when it is allowed to be put to a vote.

Additionally, leaving the previous RFC document intact, with the results of a vote if one was taken, leaves a clearer document trail than if the document has been recycled. 

To put it another way - in general the status of an RFC should not be moved backwards to an earlier status. In practice there will be times when people accidentally open the voting too early, or some serious problem is found with an RFC during the voting phase, in which cases it's fine to move the status back until the problem is fixed. But in general leaving each RFC document with a clear history of what happened to that RFC makes it easier to understand past discussions.


## Don't volunteer other people for huge amounts of work

The response to some RFCs has been to suggest that the RFC doesn't cover enough scope, and that the RFC author should make the RFC be a lot bigger.

While that sounds reasonable on the surface, the amount of time people have to work on PHP RFCs is often limited. Having someone say "thanks for volunteering, but now I want you to do a lot more work than you volunteered for" is a subtle way of preventing RFCs from being implemented.

In some cases the suggestion to make the RFC be bigger has been well-intentioned, and so the damage has been accidental.

In other cases, it would seem that the suggestion that the RFC needs to be a lot bigger or not done at all has come from someone who doesn't want the RFC to pass, which could be interpreted as deliberately making it more difficult for the RFC to pass. 

It's okay for RFCs to be small in scope, so long as they are self-contained.

It would only be appropriate to say that the RFC needs to be bigger if it would otherwise leave new inconsistencies in the language that would need to be resolved before the next release.


## Do try to talk about the problem before talking about possible solutions

Some RFCs don't make it clear what problem it is they are trying to solve before proposing a solution.

This leads to the discussions being not as productive as if the problem was introduced first.

Some people might disagree on what the exact problem is, or disagree that it even is a problem that needs solving to begin with. If people can't clearly understand that there is a problem that needs solving, then the discussion about possible solutions is going to be incredibly heated, with people not understanding the other side.

Some people might offer different solutions to the same set of problems. If the original RFC has skipped over defining the problem clearly, then it makes it a lot harder for people to suggest alternative solutions to the same problem.

Additionally, although some sets of problems may be closely related, by talking about the problems clearly, they might be broken up into separate problems to be solved by separate RFCs.


## Don't say that other people's use cases are invalid

The response to some RFCs is disappointing. Rather than accepting other people as being individuals with different priorities and motivations, some people on internals have responded with "I don't want to use this proposed feature, therefore I don't think any people should use this feature".

When you have someone saying "I want this feature", and your response is "I don't believe you actually want that feature", then you've crossed a line from being reasonable to arguing based on Solipsism, which is not going to lead to a productive discussion.

It's still okay to question how many people would want or actually use a feature, but just straight refusing to believe that anyone could find something useful doesn't give a productive discussion.


## Do try to improve RFCs

Even if you disagree with an RFC, it is good to try suggest improvements to it, if you can see them, rather than just criticising the RFC.

If the vote passes, and the RFC contains your suggested improvement - congratulations, you've helped make PHP better.

If the vote doesn't pass, even though the RFC was as good as it could be, then it will be clear to anyone who might think about reopening the RFC that it needs to be dramatically improved or take another approach for it to have a chance to be passed, rather than just having a small tweak. 


## Don't be too put out if people don't like your RFC

It is quite natural for an RFC author to think that the RFC the are proposing is clearly a good idea - why else would they be proposing it? It's also natural for them to hope that everyone else will think it's a good idea also.

However it is also entirely possible for people to have rational reasons to disagree with a proposal. 

Maybe some people haven't experienced the problem the RFC is trying to solve, and so they don't think the problem is even one that needs solving.

Maybe they have experienced in a different language what is being proposed for PHP, and they didn't like using it in that language, so they find it hard to see why it would be good for PHP.  

Whatever the reason, when people respond with something less than overwhelming support for the idea, they aren't doing it out of malice, they're doing it because they also want PHP to be the best possible language it can be - they just disagree about what that means. 
 

## Do take your time to respond to emails

For a couple of reasons, it is appropriate to take time to read and compose emails about RFCs; much longer than you spend writing emails on other subjects.

> I'm sorry I wrote you such a long letter; I didn't have time to write a short one.

Emails that are sent on PHP internals that discuss RFCs are read by hundreds if not thousands of people.

Writing concisely will save a lot of other people's time. It is also far more likely that people will read and understand your email if it is short than if you write long emails.

Additionally, unless someone was just discussing trivial issues (such as a typo in the RFC) it is appropriate to think about and digest what they were saying, rather than giving a response based on your first thoughts.


## Don't try to demand that people justify their opinions

It is the role of RFC authors to convince other people that an RFC is definitely a good idea, and that people should vote yes on it.

People might have many reasons to vote no, e.g. not convinced the problem the RFC addresses is one that needs solving, not convinced the problem is solved in the right way, not convinced that the solution is a correct one. Some of these feelings about why a proposal doesn't deserve a 'yes' vote are hard to express.

It isn't the responsibility of voters to explain why they're voting no.


## Don't shout down other people

Even if you don't like an RFC being discussed, it is more appropriate to ignore that thread, rather than asking people in the thread to stop talking about an idea you don't like.


# Contacting RFC authors should go through PHP internals list

Drafting RFCs and pushing them through internals is an exhausting process. Several PHP contributors have suddenly stopped contributing to the project after successfully getting an RFC passed, due to them being entirely fed up.

One of the things that is tiresome is people contacting the RFC author through communication channels (other than the PHP internals list), particularly when what they are going to say is either negative or even just based on not understanding part of the RFC.

There is a difference between giving positive feedback and negative feedback. And there is a difference between giving feedback to someone you have communicated with many times before, and contacting someone for the first time.

It's hard to draw an exact line of where communication is fine to go off-list, and where it should stay on list. But here are some examples:

"You are awesome for writing such an amazing RFC" - fine to send off-list.
"I found some typos in the RFC" - probably fine to send off-list, particularly if you communicate with the RFC author already.
"Please can you answer this question about the RFC" - possibly fine to send off-list, but only if you know the RFC author already.
"The RFC is a terrible idea for these reasons" - should only be sent via the list. 

# Don't pressure people by private communication to vote

Even with the best intentions, unsolicited off-list communications putting pressure on people to vote a particular way are rude. At best they don't have any effect, but most of the time they make the recipient uncomfortable.

If you want to influence how people are going to vote, these things are appropriate:

* Sending an email to internals saying that you would like to see this pass.
* Posting on Reddit /r/php or other platform where discussions take place, and then posting a link to internals, saying "these are my thoughts".
* Asking in a public communication channel asking someone in a neutral way 'are you going to vote?'.

Private communications trying to change people's minds are a burden that make people receiving them feel bad, even if they are intentioned to help the project.

