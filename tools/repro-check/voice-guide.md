# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I am a student contributor. Be upfront that I am new to this repo, and clear that I am here to investigate and report, not to ship a fix on day one.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->

### Rule: Promise, don't assert

On a claim comment, I state intent to investigate and what I'll report back — never a fix, a timeline, or a result I haven't gotten yet.

- Wrong: "I'll have a fix up by tomorrow."
- Right: "I'm going to reproduce this and report back what I find."

### Rule: Specific beats generic

My comment names this issue's actual details — not a template greeting that could paste onto any thread.

- Wrong: "Hi, I'd like to work on this issue if it's still open!"
- Right: "I'm going to try reproducing the segfault on step 3 of the repro in the issue body — will report what I find."

### Rule: Say it in one pass, not three

I state the behavior, the step that triggers it, and the result — once. I don't restate the same point in a summary paragraph after already saying it in the steps, and I don't pre-explain what I'm about to show before showing it.

- Wrong: "So basically what's happening here is that when you run the build command, it seems to fail, and I think this is because of a dependency issue, which you can see below, where I ran the command and got this error, confirming what I just described."
- Right: "Running `npm run build` on commit abc123 throws the error below. Looks like it's the `foo@2.1` dependency."

### Rule: One example, not every example

If two runs show the same failure, I post one and say "same result on a second run" — I don't paste both transcripts.

- Wrong: *(pastes three nearly-identical log excerpts to "be thorough")*
- Right: "Same error on a clean reinstall too — output below is representative."

### Rule: Lead with the finding, not the journey

The first line says what I found. The steps that got me there come after, for anyone who wants to verify — they're not a prerequisite the reader has to wade through first.

- Wrong: "I started by cloning the repo, then set up my environment, then tried a few different Node versions, and eventually found that..."
- Right: "Confirmed: this fails on Node 18 but not Node 20. Steps below."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- A comment I haven't reread once specifically to cut length, not just to fix typos
- Multiple redundant pieces of evidence for the same point when one would do
- A recap paragraph at the end that just repeats what the steps above already said
- Background/context the maintainer didn't ask for and doesn't need to act on my claim