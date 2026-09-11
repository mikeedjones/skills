# teach

A Claude Code skill that teaches you a topic over many sessions. It keeps a workspace on disk. The workspace holds your mission, your lessons, and a record of what you have learned. Each session adds one lesson and tests it in conversation.

## Install

Copy the `teach/` directory into `.claude/skills/teach/` in your project or in your home Claude Code config. Claude Code finds it there and offers `/teach` as a command.

## Start a topic

Type `/teach` and name the topic. Add a workspace directory if you want the files in a specific place:

```
/teach Rust, in learning/rust
```

```
/teach the basics of sourdough baking
```

If you do not name a directory, the skill uses your current directory. Once a workspace exists for a topic, keep using the same command and the same directory. The skill remembers the path and does not ask again.

## What a session does

1. **It asks why.** On the first run for a topic, the skill interviews you about your goal. It writes the answer to `MISSION.md`. Every later lesson traces back to this file.
2. **It writes one lesson.** A lesson is a short markdown file in `./lessons/`, sized to one sitting and one clear result. You open it in Obsidian and read it.
3. **It tests you in conversation, not in the file.** The skill writes a private rubric first, then asks you questions one at a time and grades each answer against a target it wrote down in advance. This is why the questions stay sharp through a long session — the skill is not free to soften a target after it hears your answer.
4. **It writes up the session.** When your answers cover the rubric, the skill records what you now know, extends a reference document you can search later, and offers three or four concrete next lessons.

## A workspace, after several sessions

Here is the shape of a workspace once a few lessons exist, for a topic named "Rust":

```
learning/rust/
├── MISSION.md              # the goal: ship a small CLI tool to a real team
├── NOTES.md                # the learner picture, teaching preferences, backlog
├── RESOURCES.md            # trusted sources: the book, the reference, a style guide
├── lessons/
│   ├── 0001-ownership-and-borrowing.md
│   ├── 0002-error-handling-with-result.md
│   └── 0003-traits-and-generics.md
├── learning-records/
│   ├── 0001-move-vs-copy-semantics.md
│   ├── 0002-the-question-mark-operator.md
│   └── ...
├── reference/
│   ├── glossary.md
│   └── common-patterns.md
├── assets/
│   └── ownership-diagram.md
└── .rubric/                 # private grading notes, one file per lesson
```

Each lesson stayed narrow on purpose: ownership and borrowing in lesson one, error handling in lesson two, traits and generics in lesson three. Each one gave one tangible result the learner could use before the next session.

The lessons also carried the mission into the material directly. A lesson on ownership is abstract on its own. This workspace's `MISSION.md` named a concrete goal — a CLI tool the learner's team would actually run — so each lesson tied the general rule to that goal: which part of the tool it applies to, and what breaks if it is wrong. That is what a strong mission gives you: every lesson answers "why does this matter to me," not just "what is true."

## Continuing a topic

Once a workspace exists, a bare `/teach` in that directory picks up the next lesson. You can also name the lesson directly:

```
/teach the next lesson
```

```
/teach error handling with Result
```

The skill reads `NOTES.md` and the learning records first, so it pitches the next lesson at the level you have already reached. It does not re-teach what an earlier session established, and it does not skip ahead of what the rubric only cleared shakily.

## Ground a topic in your own material

You may already own material on the topic: a set of notes, a paper, a book you have as a file. Name it when you ask to learn the topic, or in a later session. The material can stay where it already is — it does not need to move into the workspace.

This changes three things. The skill reads the material before it writes a lesson that depends on it, and treats it as outranking its own general knowledge on anything the two both cover. Lessons cite it, the same way a lesson cites a link to a web page. And it is recorded once, in `RESOURCES.md`, so a later session already knows it exists.

## Files this skill produces

- `MISSION.md` — see [MISSION-FORMAT.md](./MISSION-FORMAT.md)
- `RESOURCES.md` — see [RESOURCES-FORMAT.md](./RESOURCES-FORMAT.md)
- `./lessons/*.md` — see [LESSON-FORMAT.md](./LESSON-FORMAT.md)
- `./learning-records/*.md` — see [LEARNING-RECORD-FORMAT.md](./LEARNING-RECORD-FORMAT.md)
- `./reference/*.md` — a glossary follows [GLOSSARY-FORMAT.md](./GLOSSARY-FORMAT.md)
- `./.rubric/*.md` — the grading protocol is [PROBING.md](./PROBING.md)

Read [SKILL.md](./SKILL.md) for the full protocol.
