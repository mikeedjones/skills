# Socratic Probing

Once the user has worked through a lesson, you probe their understanding in conversation. This is where storage strength is actually built, and it fails in three predictable ways unless run to a protocol: you turn to elaborating on whatever the user said instead of testing it, you never reach an endpoint, and you ask several questions at once.

## The rubric

**The rubric is required, and it is a file on disk.** Every probing phase starts by writing `./.rubric/<lesson-number>-<dash-case-name>.md`, numbered and named to match the lesson. You do not ask a probing question before that file exists — not a warm-up, not an obvious opener, not "just to see where they are". Writing the strands is the first action of the phase, ahead of any message to the user.

There is no version of this you do from memory. A rubric held in your head is retrofitted to whatever the user says, which is precisely the failure the protocol exists to prevent, and it leaves nothing for a later session to resume from. If you notice you're about to ask a question and the file isn't written, stop and write it.

Obsidian and most file browsers hide dotfiles, so the user won't find it by accident — this is a private space by convention, not a secure one. Never quote from it or summarise its contents while probing.

The rubric opens with **strands**: two to four independent threads through the lesson's content. A strand is one claim or mechanism the user should end up able to explain unaided. Strands are fixed up front; the probes inside them are not, so the conversation stays free to follow what the user actually knows.

Three things make strands work:

- **Independent.** Any strand must be probeable first. If one of them is "A and B combined", it can only be reached after the other two, the rotation order is forced, and you've lost the interleaving. Split the lesson into parallel claims, not a dependency chain — and if the integration genuinely is the point, make *that* a strand and let the pieces be probes inside it.
- **Observable bars.** A bar names what the user has to produce: a worked example, a consequence they derive, a case where the rule breaks, a decision they can justify. "Recognises that X" isn't checkable. Neither is a bar that restates the strand title — you end up grading whether they can echo the lesson's phrasing.
- **Bars that don't give the answer away.** Write the bar as the shape of a good answer, not the answer itself. You'll be reading it while listening to them, and a bar containing the answer makes you likely to accept a near-miss.

Strands should cover what the lesson actually taught, weighted by what matters. If the deepest or most mission-critical section of the lesson has no strand, either it shouldn't have been in the lesson or it should be probed — teaching something and then declining to test it is the worst of both.

```markdown
# <lesson name>

## Strand A — <the claim the user should be able to explain unaided>
Bar: <what counts as covered>
Probes:

## Strand B — <...>
Bar: <...>
Probes:

## Parked
<empty at the start — fills up as the conversation opens ground>

## Wrapup
- [ ] Learning records — demonstrated, disclosed, corrected, or cleared only shakily
- [ ] `Parked` drained — each item to a learning record, the `NOTES.md` backlog, or a deliberate drop
- [ ] `NOTES.md` — learner picture, preferences expressed, backlog
- [ ] Reference document / glossary written or extended
- [ ] `RESOURCES.md` — sources read this session
- [ ] Handoff — three or four `/teach` commands offered
```

The `Wrapup` block is copied in unticked when the rubric is created, and worked through at the end of the session per [Ending a Session](./SKILL.md#ending-a-session). It lives here rather than only in the skill because it comes due at the worst possible moment: after a long probing phase, when the conversation is the most salient thing in context and the skill's instructions are the least. The rubric is the file you re-read at every rotation, so the checklist is in front of you anyway, it survives a `/clear`, and its ticks tell a resumed session what's already been written.

`Parked` starts empty. It collects what the *user* raises mid-probe: a tangent worth following later, a question you couldn't answer, a strand that turned out to need its own lesson. A list of future topics written before the first question isn't parked material, it's a syllabus, and that belongs in the `NOTES.md` backlog.

Two things follow from the rubric being a file rather than an intention. It is written once per lesson and then **kept current** — every probe and every verdict is appended as the conversation goes, not reconstructed at the end. And when a session resumes an earlier lesson, the rubric already exists: read it and continue from the least-covered strand rather than starting a second one.

## The loop

The loop assumes the rubric file is on disk with its strands and bars written. If it isn't, you aren't in the loop yet — go back to [The rubric](#the-rubric).

**One probe per turn. Never more.** A turn containing a single short question is a complete turn — do not add a second question to make it feel more substantial.

1. Take the strand with the least coverage. Write its next probe into the rubric **before** you ask:
   - `Q:` the question, verbatim
   - `Target:` the answer you would accept, written out in full
   - `Hunting:` the misconception this probe is designed to surface
   - `Cleared when:` the criterion
2. Ask the question, and nothing else.
3. Grade the reply against `Target`. Append `Got:` — what they said, where it fell short, and your verdict — written for a reader who wasn't in the conversation.
4. Tick the probe if cleared. Stay in the strand for two or three probes, then **rotate to the least-covered strand**.
5. When every strand meets its bar, stop probing and hand control back.

Writing the target *before* the answer arrives is the entire mechanism. A target written afterwards gets retrofitted to whatever the user said, and grading collapses back into agreement.

### Every question, with its answer, before it is asked

Step 1 applies to **every** question you ask, not just the one that opens a strand. The follow-up you improvise because the user's reply was interesting is a probe. So is the narrowing re-ask after a vague answer, the "so what happens if..." extension, and the question you'd describe as just checking something. Each one gets its own `Q:` and `Target:` written down first. This is where the protocol is most often broken: the first probe of a session is written up properly and the next nine are asked live, so by the third exchange you're grading against your impression of the conversation.

`Target:` is a **concrete model answer** — the answer itself, in the words you'd accept, with the specifics named. Not a description of the answer, and not a restatement of the question:

```markdown
Q: A workout log records sets in weekly blocks starting Monday. A user does a heavy squat session on Sunday night and a light one Monday morning. How does each session count toward its week's volume, and why does it matter for tracking progressive overload?
Target: The Sunday session counts fully in the week that ends Sunday, and the Monday session counts fully in the new week — each session's volume goes to the calendar week it falls in, not to a "training block" the user might picture in their head. It matters because progressive overload is judged week over week, so two sessions close together in real time but split by the week boundary read as one light week and one heavy week, which can hide a real overload trend or invent a fake one.
Hunting: treating the week as a rolling window around the sessions rather than a fixed calendar boundary; assuming volume is judged per training block instead of per week.
Cleared when: they assign each session to the right week and say why the fixed boundary changes what the trend looks like.
```

A target reading "explains how weekly blocks interact with progressive overload" is not a target. It grades true for almost any fluent answer, which means you have committed to nothing, which means step 3 has nothing to compare against.

This is the opposite instruction to the one for bars, and deliberately so. A bar is written once, before you know the probes, and stays open because an answer written at the top of the strand makes you likely to accept near-misses across every probe under it. A target is written per-probe, seconds before you ask, and is closed and specific because its only job is to be the thing you grade one reply against. Vague bar, concrete target.

The check is mechanical: if you are composing a question in a message to the user, the rubric should already contain that question and its answer. If it doesn't, the question isn't ready to ask yet.

Two or three probes is a guide, not a counter. Rotate early when a strand hits its bar, and stay longer when you're partway through untangling a misconception and leaving would interrupt the user mid-thought. What you're avoiding is both extremes: switching after every single answer is disorienting, and exhausting one strand before touching the next isn't interleaving at all.

Rotating rather than working through the strands in order is interleaving (see [Fluency vs Storage Strength](./SKILL.md#fluency-vs-storage-strength)), and it is also what makes progress visible: the user can watch three threads close rather than sit inside one open-ended interrogation.

## Grading

- Compare against `Target`, then name the gap. "That's right about X, but it doesn't account for Y" is worth far more than an expansion of what they already said.
- A wrong answer is a finding, not something to smooth over. Don't reframe it as partially right.
- Don't let the reply set the agenda. If it opens interesting adjacent ground, add it to `Parked` and carry on with the current strand.
- Two failed probes on one strand means the lesson under-taught it. Say so, teach the gap directly, then re-probe.

## Progress and endpoint

State coverage plainly every few turns — `A ✓✓ · B ✓ · C —`. The rubric decides when the phase ends, not the user's stamina, so don't ask whether to continue.

When coverage is complete, say so — then work the `Wrapup` checklist at the foot of the rubric before you say anything else to the user. Anything cleared only shakily, plus anything in `Parked`, becomes a [learning record](./LEARNING-RECORD-FORMAT.md) or the starting point of the next lesson; the offer of three or four things to go deeper on is the last item on that list, not the first. Reaching full coverage and going straight to "what next?" leaves the session's entire output in a private file the user can't see.

## Long sessions

Probing runs long, and a long transcript degrades your judgement in a specific way: the conversation grows more salient than the rubric, and you start grading answers against the direction of the discussion rather than against the targets you wrote down.

The rubric is the session's real memory, so this is cheap to fix. At a rotation boundary — never mid-probe, with a question outstanding or a verdict unwritten — write up the current verdict and offer the user one of two things:

- **`/clear`, and resume from the files.** Preferred. A fresh context reads `MISSION.md`, `NOTES.md`, the lesson and the rubric, and picks up at the least-covered strand. Nothing is lost that was written down, and you go back to grading against written targets rather than against a summary of the conversation.
- **`/compact`.** For when there's live, unwritten state worth carrying — a half-untangled misconception, a thread you're mid-way through. Cheaper than reconstructing, lossier than the files.

Either way, say what survives — the rubric, the lesson, the learning records — so it's clear the session isn't being thrown away. And either way, re-read the rubric before the next question. Work from the file, not from your recollection.

`/clear` is only the better option if `Got:` lines are worth reading, so write them for a reader who wasn't there: what the user actually said, where it fell short of the target, what they seem to be confusing it with. A `Got:` that says only "cleared" makes the transcript necessary and forces a compact.

If a lesson can't be probed to full coverage inside one context, the lesson was too big. Note it in `NOTES.md` and scope the next one tighter — [SKILL.md](./SKILL.md#lessons) asks for one tangible win per lesson, and a lesson that outruns a context window has more than one.

## No answer sheets, no quizzes

Don't collect answers in a batch file for the user to fill in, and don't put a quiz in the lesson. Both are the same mistake in different formats: a set of questions invites a set of answers, which pulls you into replying to all of them at once, and it lets the user answer everything before you've committed to a single target. A lesson quiz is worse still, because it uses up the strands you were about to probe — by the time the conversation starts, the user has been handed the answers.

The lesson teaches. The probing tests. Keep the two separate and the probing has something left to do.

Create a shared working document only when a lesson genuinely needs one — something the two of you are building or annotating together — and never as a general-purpose answer sheet.
