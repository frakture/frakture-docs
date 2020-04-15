# Attribution Design -- Constrained vs Unconstrained attribution

Assigning credit is one of the most difficult tasks to get right at scale -- not least of which because techniques that work in individual or small numbers of situations often deliver weird or just flat-out bad results when applied to other situations.  It comes up in a lot of scenarios, but here we'll focus on designing algorithms and processes for attributing credit for transactions and revenue to different channels.

"Unconstrained" and "Constrained" are two different frameworks for assigning credit.

## Unconstrained attribution

To keep the conversation from getting into the weeds, we'll start with a metaphor.  Imagine a company meeting where a director of sales, Sue, is determining how to assign commission to her 10 person sales team.  She starts with giving 10% commission of each signed deal to the rep that closed it.  If someone assisted, they get 3%.  She's experienced, so factors in conditions of clients not paying, early closed contracts, etc, etc.  It works absolutely great.  Company does awesome.

This is an example of unconstrained attribution.  Developing smart rules to incentivize good behavior.  There's absolutely nothing wrong with it.  But if you change some of the conditions, it can go absolutely haywire.

John was one of her sales reps, and moves on to a manager role at a much larger company.  He works his way up, and eventually is in charge of 30 people.  Having had such a good experience with Sue's model, he implements it with his new team.  Within the first month it's pretty clear that things are going wrong.  The different product requires a lot more people involved with the sale -- so suddenly he's paying out 3% commission to 10 assistants for every sale.  Way too much.  Budgets get missed, staplers go missing, absolute bedlam.  Company fails.

It's fairly obvious to humans that these different conditions require some tweaking of the rules depending on the situation.  It's actually pretty straightforward.  In fact, you can probably start listing out a bunch of ways to 'fix' the algorithm (if more than 10 people, cut it to 1% commission, etc, etc).  You'll probably catch a bunch of cases you missed before.  You may even believe that the algorithm is perfect for all scenarios.  But if you're still working in an unconstrained, open-ended process, it's far, far more likely that you're going to miss something, and that algorithm is going to blow up somewhere.

## Constrained attribution

Automation relies on code and algorithms that work in all the situations, often without any human oversight. 'Tweaking' the rules per situation is not easy -- nor can the effects of that tweaking always be immediately seen.  Because of this, "Constrained" algorithm designs focus first on "Not blowing up", and then effectively work backwards to accommodate the different scenarios.  In the company case above, a constrained design might first start with saying

	"We're going to give out 15% commission *total* on any deal"

That's the constraint.  Then fractions of credit would be given to team members based on how involved they were in the sale.  For example, 10% to the prime rep, the remaining 5% distributed amongst all assistants.  Or perfectly even distribution, etc, etc.  It accomplishes similar goals (crediting people for the sale), but with a design that *cannot blow past the constraint*.

As long as that constraint is maintained, basically any algorithm you choose won't behave badly.  It may not be perfect -- and lots of tweaks may need to get it just right, but by maintaining that constraint it assures you're not going to get ludicrous results in situations you haven't considered.


## Attribution models

Turning to our real use case, attributing transactions to channels, we can lay out an unconstrained model.

	Assign credit to the source channel if this message was involved in the transaction,
	and for any future gifts this person gave if they were new.
	Make sure not to count the same transaction twice.

Makes sense.  Of course, if someone was signed up with one channel, and made a transaction from another ... now you've got a decision.  Which channel gets the credit?  Both?  But then we count the same transaction twice, which would lead to reporting double the revenue (unless we tell people to just not do the math - ick).  Uh-oh.  Okay, maybe we tweak it -- we say that in that situation, the most recent channel gets the credit.  Well, now you're basically not crediting the first channel at all, unless they gave directly on it. And etc, etc.  The rules start to multiply, but it's not clear we're getting closer to a foolproof algorithm.

Typically, as long you're only looking at one channel, we're absolutely fine.  But it completely blows up if you start comparing multiple channels -- and even if you keep adding rules, you can't ever be sure it's not going to blow up somewhere.  It may even work the first 20 times you use it, and lull you into believing it will always work -- but the more complicated it is, the more likely it is to collapse when you least expect it.

### Constrained attribution models

There is, however, an alternative, and that's to use a Constrained attribution model.  If instead of starting with assigning credit, we first start with the constraint:

	Don't attribute more than 100%

then we can do all kinds of complicated things, and be assured that the end result isn't going to blow up.  In the attribution world, this is often called Fractional (Fraktional :) attribution.  Rather than coming up with rules to assign credit, and hoping it adds up, we first start with 100%, and then distribute fractions of that whole depending on our rules.

The same information is typically used as an unconstrained model, such as first transaction, most recent message, etc, but instead of assigning full credit based on "if (this) then (that)", constrained attribution starts with 100% of a transaction, and then portions out parts of that to different channels.  So in the above example, you might assign 40% of the credit to the original source channel, and 60% to the most recent channel.  No matter how you do the split, and no matter how many interactions you involve, and no matter how complicated you make it, if you hold to the constraint, you're *assured* you're never going blow up.

There's lots of opinions on the *best* way to attribute -- but as long as they all follow the same constraint, they can be compared and swapped out without affecting the bottom line.

Check out Google and Facebook's attribution model explanations for different examples of fractional attribution:

<a href="https://support.google.com/google-ads/answer/6259715" target="_blank">About Attribution Models [Google]</a>

<a href="https://www.facebook.com/business/help/370704083280490?id=399393560487908" target="_blank">About attribution models [Facebook]</a>
