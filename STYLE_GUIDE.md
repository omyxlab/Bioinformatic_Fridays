# Bioinformatic Fridays — Authoring Style Guide

*The house style for all lessons and modules. Follow it exactly so the course stays consistent no matter who (or which AI assistant) writes the next module.*

---

## 0. How to use this guide

If you are a **human author**: read §1–§3, then copy the skeleton in §12 to start a new lesson, and run the checklist in §13 before you commit.

If you are using an **AI assistant (LLM)** to draft lessons: paste this entire file into the conversation as context, then give the assistant the module and lesson you want. A ready-made instruction is in §14 — copy it verbatim.

This guide is prescriptive on purpose. When in doubt, match Modules 0 and 1 and the existing Linux, GitHub, and Conda modules (Modules 2, 3, and 4) — they are the reference for the house style. Do **not** imitate the older Omics or Project modules' tone; they predate this guide and will be revised to match it.

---

## 1. Audience and voice

- **Audience:** life scientists and bioinformatics beginners. Assume biological literacy but **no** command-line, programming, or statistics background unless an earlier module taught it.
- **Voice:** plain, direct, and second person ("you run", "you will see"). Warm but not chatty.
- **No hype.** Avoid grandiose framing ("unlock the power of", "industry-standard", "the Big Four", "zero to hero" inside lessons). State what a thing is and why it matters, then show it.
- **Define before you use.** The first time a technical term appears in a lesson, define it in one clause and link it to the glossary (§8). Never use an acronym before spelling it out once.
- **Short sentences. Short paragraphs.** One idea per paragraph.

---

## 2. No emoji in lesson or module content

Lessons and module READMEs contain **no emoji** and no decorative symbols in headings. (Plain Markdown only.) This is a deliberate reversal of the older modules' style, for consistency and accessibility.

---

## 3. File and folder naming

- **Modules:** `Module_<N>_<ShortName>/` where `<N>` starts at `0`. Example: `Module_0_Getting_Ready/`, `Module_1_Bioinformatics_Foundations/`.
- **Lessons:** `Lesson_<N>_<Title_In_Title_Case>.md`, `<N>` starts at `1`. Example: `Lesson_2_Text_Processing_and_Pipes.md`. Use underscores, not spaces or hyphens.
- **Parallel tracks:** append the track: `Lesson_3_Reading_Data_Python_Track.md`, `Lesson_3_Reading_Data_R_Track.md`.
- **Supporting files (fixed names):** `README.md`, `Exercises.md`, `Solutions.md`, `GLOSSARY.md`, `File_Formats_Reference.md`.

---

## 4. Required lesson structure

Every lesson uses these sections, in this order. Omit a section only if it genuinely does not apply.

1. `# Lesson <N> — <Title>` (one H1, em dash).
2. `## Learning Objectives` — 4–6 bullets, each starting with a verb ("Navigate…", "Explain…", "Run…"). These must match what the lesson actually teaches.
3. `## Conceptual Overview` — the "why" and the ideas, before any commands. Prose, not bullets where prose reads better.
4. **Compute note** (when steps differ between WSL and TLJH) — the callout in §7.
5. `## Worked Examples` — numbered steps, each: a one-line explanation, the command block, then the expected output block (§5–§6).
6. `## Exercises` — numbered, graduated from easy to challenge. Phrase as tasks or questions, not "do example 3 again".
7. `## Solutions` — one per exercise, matching numbers. (Placement rule in §9.)

Module `README.md` files use: `# Module <N>: <Title>`, a short overview, `## Learning objectives`, a `## Lessons` list or table, and a `> Note:` or toolbox line as needed. Keep them to one screen.

---

## 5. Code blocks

- Fence every command in triple-backtick ```` ```bash ````, ```` ```python ````, or ```` ```r ```` as appropriate.
- **One concept per block.** Do not stack unrelated commands.
- **No leading prompt characters.** Write `ls Training`, not `$ ls Training` — so learners can copy-paste cleanly.
- **Every block must run as-is.** No stray characters (a stray backtick in a past lesson broke copy-paste — this is exactly what the checklist in §13 guards against). Test each command before committing.
- **Placeholders** go in angle brackets: `conda install -n <env_name> <tool>`. Tell the reader what to substitute.
- **Long commands** wrap with a trailing backslash `\` and continue on the next line, aligned for readability.
- Comments inside blocks are sparse and only where the command is not self-evident.

---

## 6. Showing expected output

After a command that produces output, show it:

```
Output:
```
```
<the expected output>
```

When a command succeeds silently, write: **"No output is expected when this command succeeds."** Do not invent output. If output varies by machine, say so ("version numbers will vary") and show a representative example.

---

## 7. The WSL / TLJH dual-environment callout

The course runs on **both** WSL (own machines) and **TLJH** (shared JupyterHub). When a step differs between them, use this exact callout format:

> **On WSL (your own machine):** `<instructions>`
>
> **On TLJH (shared server):** `<instructions, or "This is already set up for you — skip to the next step.">`

When a step is identical on both, write it once with no callout. Never assume one environment silently.

---

## 8. Glossary and cross-references

- **Glossary:** on first use of a key term in a lesson, link it: `[ortholog](../GLOSSARY.md#ortholog)`. Keep `GLOSSARY.md` entries to one line each, alphabetical, with an `## anchor` heading per term.
- **File formats:** link format mentions to the cheat-sheet: `[FASTQ](../File_Formats_Reference.md#fastq)`. Teach a format's full mechanics only once, at the point it is first produced; elsewhere, link.
- **Other modules:** reference by number and link: `[Module 5](../Module_5_Bash_Scripting/README.md)`. Do not hardcode a lesson's position if a link will do.

---

## 9. Where solutions live

- A **standalone lesson** with its own exercises ends with its own `## Solutions` section (as in the Linux module).
- A **module whose job is exercises** (recap, problem-solving) keeps exercises in `Exercises.md` and answers in a separate `Solutions.md`.

Pick the one that matches the lesson type; do not mix within a module.

---

## 10. Data, paths, and reproducibility

- The dataset lives on **Zenodo** and is downloaded in Module 0. Refer to it as "the `Training/` folder".
- **Never hardcode a personal path** like `/mnt/c/Users/WAVECU001/...`. Use a relative path from `Training/`, or set and use a variable:
  ```bash
  TRAINING=~/Bioinformatic_Fridays/Training
  ```
- **No hardcoded dates or deadlines** in lesson content. Write "by the date announced for your cohort", not "by 24 April 2025".
- Pre-stage or subset any download larger than a few hundred MB so live sessions do not stall; note the download size.

---

## 11. Admonitions

Use blockquotes with a bold label. Keep to these three:

> **Note:** background or clarification.

> **Tip:** an optional shortcut or good habit.

> **Warning:** something that can lose data or break things. Use for every destructive command (`rm`, overwrite, force-push), especially on WSL where `/mnt/c/...` is the learner's real Windows files.

---

## 12. Lesson skeleton (copy to start a new lesson)

```markdown
# Lesson <N> — <Title>

## Learning Objectives
- <verb> …
- <verb> …
- <verb> …

## Conceptual Overview
<Why this matters and the key ideas, in plain prose. Define and link key terms on first use.>

> **On WSL (your own machine):** <only if setup differs>
>
> **On TLJH (shared server):** <only if setup differs>

## Worked Examples

### 1) <what this step does>
<one-line explanation of the command and any flags>
```bash
<command>
```
Output:
```
<expected output, or: No output is expected when this command succeeds.>
```

### 2) <next step>
...

## Exercises
1) <easy task>
2) <medium task>
3) Challenge: <open-ended task>

## Solutions

### Solution 1
```bash
<command>
```
Output:
```
<expected output>
```
```

---

## 13. Pre-commit checklist

Before committing a new or revised lesson, confirm:

- [ ] Every command block runs **as-is** (copy-pasted and tested) — no stray characters.
- [ ] Every command that produces output shows the expected output; silent commands say so.
- [ ] Learning Objectives match what the lesson actually teaches.
- [ ] No personal/absolute paths; data referenced via `Training/` or `$TRAINING`.
- [ ] WSL **and** TLJH both addressed wherever a step differs.
- [ ] Every key term defined on first use and linked to `GLOSSARY.md`; file formats linked to the cheat-sheet.
- [ ] No emoji; headings are plain.
- [ ] No hardcoded dates or deadlines.
- [ ] Destructive commands carry a **Warning** callout.
- [ ] Exercises have matching, numbered solutions.

---

## 14. Ready-made instruction for an AI assistant

Paste this file as context, then paste the block below (fill in the brackets):

> You are writing a lesson for the Bioinformatic Fridays course. Follow `STYLE_GUIDE.md` (provided above) exactly: the required section order (§4), plain no-emoji voice for life-science beginners (§1–§2), copy-paste-safe command blocks with shown output (§5–§6), the WSL/TLJH dual callout where steps differ (§7), glossary and format links on first use (§8), no personal paths or hardcoded dates (§10), and Warning callouts on destructive commands (§11). Before finishing, self-check against the §13 checklist and fix anything that fails. Write **Module <N>, Lesson <N>: <title>**, covering: <topics>. The dataset is the `Training/` folder (downloaded from Zenodo in Module 0); the conda environment is `bioinfo`.

---

*End of style guide.*
