# Lesson Format

Lessons live in `./lessons/`, one markdown file each, sequentially numbered: `0001-dash-case-name.md`, `0002-...`. Scan the directory for the highest existing number and increment by one.

They are read in Obsidian. That makes them markdown first, and HTML only where markdown cannot express something.

## Skeleton

```md
---
lesson: 3
topic: {the strand this sits in}
time: ~10 minutes
title: {The thing being taught — not "Lesson 3"}
tags:
  - teach/{workspace-slug}
---
## {First section}

{The teaching, in a handful of short sections.}

> [!question] 💬 Bring your questions to the conversation
> {the agent is their teacher; probing happens in chat, not on the page}

## Sources

- {the primary source, linked}
- {anything else cited above}

> [!note]- Further reading (optional)
> - {parked depth, collapsed}

---

Next: [[0004-slug|Title →]]
```

Three things every lesson carries, wherever they sit in it:

- **A primary source** — the highest-quality, highest-trust thing found on the topic, for the user to go and read or watch.
- **A reminder to ask followups**, because the lesson is one half of a session and the conversation is the other.
- **Links out** to the lessons and reference documents it relates to, so the workspace accumulates into a linked graph rather than a set of unconnected files.

## Obsidian constructs

Prefer these over hand-rolled HTML: the user's theme styles them, they render in both editing and reading view, and they survive the file being moved or renamed.

- **Callouts** for every boxed aside — definitions, key points, misconceptions, context blocks. `> [!tip] Key point` on the first line, `>` on each body line after. Only the built-in types render without a CSS snippet: `note abstract info todo tip success question warning failure danger bug example quote`. The title after the type is free text, so a custom title on a built-in type (`> [!info] 💼 Work context`) gets a bespoke-looking block with no styling to maintain. A trailing `-` (`> [!tip]-`) starts it collapsed — right for optional further reading, wrong for anything the user has to read.
- **Wikilinks** — `[[0002-technical-barriers|Next: Technical Barriers]]` — for anything inside the vault, including source material outside the workspace. They give backlinks and graph edges. Use markdown links for external URLs.
- **Mermaid** code blocks for diagrams, `$...$` and `$$...$$` for maths, tables, and `[^1]` footnotes. All native.
- **Frontmatter** for lesson metadata. It renders as a properties panel, so it replaces both a header strip and an `# H1` in the body — the title is a property, and body headings start at `##`.
- **Embeds** — `![[assets/some-block]]` — to pull a shared component into several lessons.

## HTML

For what markdown can't say: inline `<svg>`, a two-column layout, a coloured span. Three constraints, all of which fail silently:

- **Markdown isn't parsed inside an HTML block.** `<div>**bold**</div>` renders the asterisks. Write the whole block in HTML or none of it.
- **Style with inline `style="..."` attributes.** External stylesheets aren't loaded and `<style>` blocks are unreliable. Vault-wide styling lives in a CSS snippet under `.obsidian/snippets/`, which is the user's to enable and not yours to assume.
- **`<script>` never runs.** Reading view strips it. Anything interactive is a separate file — see [Assets](./SKILL.md#assets).

Leave a blank line either side of an HTML block, or it gets absorbed into the surrounding paragraph.

## Consistency across lessons

What makes the lessons read as one course rather than a set of unrelated documents is a consistent vocabulary: the same callout type for the same job in every lesson, the same section order, the same frontmatter keys. Record the vocabulary in `RESOURCES.md` as it settles, and hold to it.

A lesson that boxes a definition in `[!quote]` when the other six use `[!abstract]` is the inconsistency to watch for. It renders fine, so nothing catches it but you — read a previous lesson before writing a new one.
