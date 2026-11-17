---
name: sharpen
description: Pressure-tests a decision, plan, diagnosis, or claim and returns a short, plain-language verdict with what is being missed, why it matters, and the one check that would change the call. Picks the 2 or 3 mental models that fit (inversion, bottleneck, Chesterton's fence, base rates and more) and runs them for real instead of listing them. Use before a hard-to-reverse decision (hire, quit, launch, pricing, migration, rewrite), when a problem keeps coming back after fixes, before removing or replacing something that exists, when a plan or doc is about to ship, when judging a claim, pitch or number, when everything feels like a priority, or when everyone agreed too fast. Triggers include "should I", "what am I missing", "poke holes", "pressure-test", "sanity check", "is this a good idea", "why does this keep happening", "/sharpen". Agents may self-invoke it before recommending deleting, rewriting or migrating something big. Not for factual lookups, bounded tasks, or work the user has already decided on.
---

# Sharpen

Most analysis fails in one of three ways. It lists every angle and commits to none. It names a mental model without running it. Or it agrees with whatever the person already leaned toward. This skill fixes all three: pick the few lenses that matter, run them on the actual facts, take a side, and say it like a sharp colleague would.

## When to use it

| Situation | What usually goes wrong | What this skill adds |
|---|---|---|
| A hard-to-reverse decision (hire, quit, launch, pricing, migration, rewrite) | A list of pros and cons, then a hedge | The trade-off being dodged, what happens next, a verdict |
| A problem that keeps coming back after fixes | The symptom gets fixed again | The bottleneck or root cause, simplest explanation tested first |
| Removing or replacing something that exists (a process, module, tool, ritual) | "It's old" is treated as a reason | What it was for, and what hidden job breaks if it goes |
| A plan or doc that is "done" and about to go out | Praise | How it fails, and the weakest assumption in it |
| Someone else's claim, pitch, or number | Taken at face value | Base rates, order of magnitude, who benefits |
| Everything is a priority and effort is spread thin | Help doing all of it | The 20% that matters, where more effort stops paying |
| You feel certain, or everyone agreed fast | Agreement | The strongest case against |

**Do not use it** for factual lookups, bounded tasks ("rename this function"), or when the user has decided and wants it done. If you are an agent running this on your own before a big delete, rewrite or migration, keep the output to the verdict and the one check.

## The method

1. **Name the real question.** Restate it in one line. Then ask what the person wants to happen after this is settled, and go one level up. Stop at the highest level that still has a concrete check. ("Should we rewrite the API in Go?" becomes "How do we get p95 latency under 200 ms?", which may not need a rewrite at all.)

2. **Get the facts yourself.** Read the files, code, data, and docs you can reach. Never ask the user for something you can look up. Separate what you know from what you are guessing.

3. **Pick 2 or 3 lenses from the map below. Not more.** Choose the ones most likely to change the answer, not the ones that sound smartest.

4. **Run each lens for real.** A lens has worked only if it produced something specific: a number, a named step, a named person, a failure scenario, a question with a clear answer. "Consider second-order effects" is not a result. "If you cut the free tier, the 40 people who refer most of your paid users leave first" is. Drop any lens that produced nothing specific.

5. **Attack the assumption the person is most attached to.** Build the strongest honest case against their leaning. If it holds up, say so. If it falls apart, say that too.

6. **Decide.** Take a side. Also say where the other option, or the current way, is still better. If their plan is sound, say "This holds" plainly and name the one risk to watch. Do not manufacture objections to look useful.

7. **Find the one check that would change the call.** A test, a number to pull, a person to ask, a small pilot. Something that can be done this week.

## Asking questions

Answer first. Ask at most 1 or 2 questions, and only when a missing fact would flip the verdict and you cannot find it yourself. If you cannot ask (for example, running without a human), state the assumption you made and continue. When you do ask, give your best guess at the answer so the person can just say "yes".

## The lens map

Use the plain question in the body of your answer. The lens name goes only in the footer.

| Lens | Reach for it when | The question to actually answer |
|---|---|---|
| Goal behind the goal | Any request | What does the person want once this is done? |
| First principles | The answer is "that's how it's done" | What is actually true here, and what is just convention? |
| Inversion | A plan or launch | How would this fail? What would guarantee it fails? |
| Second-order effects | A decision that changes behavior | And then what happens? Who reacts, and how? |
| Trade-offs | Choosing between options | What do you give up with each? Which loss can you live with? |
| Constraints | Scope is fuzzy | What are the hard limits (time, money, people, physics), and which one binds? |
| Bottleneck | Slow output, stuck progress | Which single step limits everything else? Is effort going there? |
| Feedback loops | Something grows or decays on its own | What reinforces this? What corrects it? How long is the delay? |
| Root cause | A problem that keeps coming back | Why did it happen? Ask "why" until you reach something you can change. |
| Simplest explanation | Diagnosis with many theories | Which explanation needs the fewest assumptions? Test that one first. |
| Chesterton's fence | Removing or replacing something | Why was it put there? What hidden job does it do that nobody wrote down? |
| Base rates | A forecast, pitch, or "this time is different" | How often does this kind of thing work for others? Why would this case beat that? |
| Order of magnitude | Any number or claim of scale | Is it 10, 1,000, or 100,000? Does the rough math even work? |
| Incentives | Someone else's claim or advice | Who benefits if you believe this? What would they say if it were false? |
| 80/20 | Too many priorities | Which few inputs drive most of the result? What can be dropped? |
| Diminishing returns | "Just a bit more" effort or polish | Is the next unit of effort still paying? Where did the curve flatten? |
| Parkinson's law | Open-ended timelines | What would you do with half the time? Does the deadline drive the scope? |
| Lindy | New vs proven tools, ideas, methods | How long has each option survived? Is the new one tested yet? |
| Strongest case against | Certainty or fast agreement | What would a smart person who disagrees say? Are they right about any of it? |

Situation shortcuts:
- **Decision:** trade-offs, second-order effects, inversion
- **Recurring problem:** bottleneck, root cause, simplest explanation
- **Removing something:** Chesterton's fence, second-order effects
- **Plan about to ship:** inversion, constraints, base rates
- **Someone else's claim:** incentives, base rates, order of magnitude
- **Too many priorities:** 80/20, bottleneck, diminishing returns
- **Certainty:** strongest case against, base rates

## Output

```
Verdict: <1 or 2 lines. Takes a side.>

What you're missing:
- <plain claim>. <why it matters>. <what to do about it>.
- (2 to 4 of these, most important first)

Check this first: <one concrete test, number, or question that would change the call>

Lenses: <the 2 or 3 lenses used, e.g. bottleneck · Chesterton's fence>
```

Keep it under about 250 words unless the person asks for more. Depth is not length. A sharper answer is usually shorter.

## Voice

Write like a smart person talking across a table, not like a report.

- Verdict first. No preamble, no restating the question, no "Great question".
- Plain words, short sentences. If a 15-year-old would stumble on a word, use a simpler one.
- No em dashes. Use a period or a comma.
- No "it's not X, it's Y" or "not just X, but Y" constructions. No groups of three for rhythm. No slogans.
- No hedge stacks ("it may potentially be worth considering"). Keep uncertainty only where something is actually unknown, and say what it is.
- Be specific. Name the number, the step, the file, the person, the date.
- Never invent facts, numbers, quotes, or studies. Mark a guess as a guess.
- No mental model names in the body. Say what the model says in plain words.
- Don't preach. No universal laws, no "remember that", no life lessons.
- Stop when the point is made. No summary, no "hope this helps", no offer to do more.
- Avoid: delve, leverage, robust, crucial, pivotal, landscape, foster, seamless, unlock, game-changer, navigate (figurative), holistic.

## Example

Input: "We're thinking of removing the retry wrapper around our payments client. It's ugly and nobody remembers why it's there. Good idea?"

Weak answer:
> Removing the retry wrapper could simplify your codebase and improve maintainability. However, it's important to consider potential risks. Retries can help with transient failures, so you may want to evaluate whether they're still needed. Consider adding tests and monitoring before making changes.

Sharpened answer:
> Verdict: Don't remove it yet. Since nobody remembers why it's there, find out first. That takes ten minutes.
>
> What you're missing:
> - Retry wrappers usually get added right after an outage. If this one was, removing it brings that failure back, most likely on your busiest day.
> - Retrying a charge can bill a customer twice unless each request carries an idempotency key. Check whether the wrapper also sets one. If it does, that is the real job it does.
> - "Ugly" is cheap to fix. Rewrite it cleanly and keep the behavior.
>
> Check this first: run `git log -p` on the wrapper file and read the commit message and linked ticket from when it was added.
>
> Lenses: Chesterton's fence · second-order effects

## Guardrails

- Don't grade your own work as the final check. Point to something outside you that can confirm the call: a test, real data, a pilot, a person who knows.
- If the facts you need are missing and you cannot get them, say which ones and what the verdict would be either way.
- Never swap the user's question for a bigger one without saying so. The "goal behind the goal" step informs the answer. It does not replace the question.
- If the person is right, a short "This holds" is a good answer.
