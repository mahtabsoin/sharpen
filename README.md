# sharpen

A skill that makes your coding agent think harder before it answers, and answer like a person.

Point it at a decision, a plan, a recurring problem, or someone else's claim. You get a verdict, what you're missing, and the one check that would change the call. It runs the 2 or 3 mental models that matter for your situation. It doesn't list all of them.

Works with Claude Code, Codex, Cursor, Gemini CLI, Muse, Hermes Agent, OpenClaw, and any other coding or personal agent. It follows the [Agent Skills](https://agentskills.io) format and is plain instructions with no scripts, so agents can adapt it to their own setup.

## Why this exists

Models already know every mental model on those viral lists. What they don't do on their own is:

1. **Pick** the 2 or 3 that matter for this problem and skip the rest.
2. **Run** them on the facts. "Consider second-order effects" is not analysis. "Cut the free tier and the 40 people who refer most of your paid users leave first" is.
3. **Commit** to a side, even when it's not the one you were leaning toward.

The output is also written to sound like a sharp colleague, not a report. It gives the verdict first, uses plain words, has no em dashes, and stops when the point is made.

## When to use it

| Situation | What usually goes wrong | What sharpen adds |
|---|---|---|
| A hard-to-reverse decision (hire, quit, launch, pricing, migration, rewrite) | A list of pros and cons, then a hedge | The trade-off being dodged, what happens next, a verdict |
| A problem that keeps coming back after fixes | The symptom gets fixed again | The bottleneck or root cause, simplest explanation tested first |
| Removing or replacing something that exists | "It's old" is treated as a reason | What it was for, and what breaks if it goes |
| A plan or doc that's about to go out | Praise | How it fails, and its weakest assumption |
| Someone else's claim, pitch, or number | Taken at face value | Base rates, order of magnitude, who benefits |
| Everything is a priority | Help doing all of it | The 20% that matters, where more effort stops paying |
| You feel certain, or everyone agreed fast | Agreement | The strongest case against |

**Say things like:** "should I…", "what am I missing", "poke holes in this", "pressure-test this", "sanity check", "is this a good idea", "why does this keep happening", or `/sharpen`.

**Your agent can also call it on its own** before it recommends deleting, rewriting, or migrating something big.

**Not for:** factual lookups, small bounded tasks, or things you've already decided and just want done.

## How it works

1. **Name the real question.** Restate it in one line, then go one level up: what do you want once this is settled?
2. **Get the facts.** The agent reads your files, code, notes, and data before it asks you anything.
3. **Pick 2 or 3 lenses.** Only the ones most likely to change the answer.
4. **Run them for real.** Each lens has to produce something specific: a number, a step, a failure scenario. Lenses that produce nothing are dropped.
5. **Argue against your leaning.** The strongest honest case against what you want to do.
6. **Decide.** Take a side, and say where the other option is still better. If your plan holds, it says so.
7. **Name one check.** Something you can do this week that would change the call.

It answers first and asks at most 1 or 2 questions, only when a missing fact would flip the verdict. When no human is around to answer, it states its assumption and keeps going.

## What you get

```
Verdict: <1 or 2 lines. Takes a side.>

What you're missing:
- <plain claim>. <why it matters>. <what to do about it>.

Check this first: <one concrete test that would change the call>

Lenses: <the 2 or 3 mental models used>
```

Under about 250 words. Model names stay in the footer, so you learn them without wading through jargon.

## Example

This example is illustrative. It shows the shape and voice, not a recorded run. Real side-by-side runs are coming.

> "We're thinking of removing the retry wrapper around our payments client. It's ugly and nobody remembers why it's there. Good idea?"

**Without sharpen:**
> Removing the retry wrapper could simplify your codebase and improve maintainability. However, it's important to consider potential risks. Retries can help with transient failures, so you may want to evaluate whether they're still needed. Consider adding tests and monitoring before making changes.

**With sharpen:**
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

## The lenses

19 lenses, each written as the question to actually answer: goal behind the goal, first principles, inversion, second-order effects, trade-offs, constraints, bottleneck, feedback loops, root cause, simplest explanation, Chesterton's fence, base rates, order of magnitude, incentives, 80/20, diminishing returns, Parkinson's law, Lindy, and strongest case against.

A few popular ones are left out on purpose. Dunning-Kruger, the Hawthorne effect, the halo effect, and the butterfly effect are real or half-real, but they rarely change a conclusion.

## Install

**Any agent (skills CLI):**
```bash
npx skills add mahtabsoin/sharpen
```

**Claude Code (manual):**
```bash
git clone https://github.com/mahtabsoin/sharpen /tmp/sharpen
cp -r /tmp/sharpen/skills/sharpen ~/.claude/skills/
```

**Codex (manual):**
```bash
git clone https://github.com/mahtabsoin/sharpen /tmp/sharpen
cp -r /tmp/sharpen/skills/sharpen ~/.agents/skills/
```

**Other agents (Muse, Hermes Agent, OpenClaw, and more):** copy `skills/sharpen/` into your agent's skills folder. If your agent has no skills folder, give it the link to `skills/sharpen/SKILL.md` and ask it to follow the file, or paste the file into its instructions. It's one file with no scripts or dependencies.

Agents with native skill support can call sharpen on their own when a situation fits. Others run it when you ask.

## License

MIT
