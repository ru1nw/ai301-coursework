# Voice guide: how I talk upstream

<!--
THIS IS A CARRY-OVER SLOT, not a new hole. You wrote this guide in
week 2; paste your filled week-2 voice-guide.md here, whole. It is not
re-authored and it is not graded as new work this week.

Then reread it with the plan comment in mind. Your claim and repro
comments promised and reported; a plan comment commits you to an
approach in front of the people who maintain the code. If your rules
do not cover that register (for example: how you state an approach you
are not certain of, or how you respond when a maintainer already
suggested a direction), extend the guide with what it needs. Extending
is allowed and encouraged; starting over is not required.

Live mode reads this file before your plan comment goes out and
reports any rule your draft breaks. Eval mode ignores it entirely,
because your voice is yours and carries no gold labels.
-->

## Who I am in threads

<!-- Paste your week-2 section here. -->

I am a student contributor. Be upfront that I am new to this repo, and clear that I am here to investigate and report, not to ship a fix on day one.

## Rules I write by

<!-- Paste your week-2 rules here, wrong/right pairs and all. Add any
rule the plan-comment register needs that your week-2 comments did
not. -->

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

<!-- Paste your week-2 list here; extend it if planning tempts you
toward new ones (overpromised timelines are the classic). -->

- A comment I haven't reread once specifically to cut length, not just to fix typos
- Multiple redundant pieces of evidence for the same point when one would do
- A recap paragraph at the end that just repeats what the steps above already said
- Background/context the maintainer didn't ask for and doesn't need to act on my claim