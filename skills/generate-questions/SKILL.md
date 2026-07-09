---
name: generate-questions
description: Use when creating or updating module question imports for Blackboard from Course/<lang>/Modules/* content and requiring auto-gradable tab-delimited questions.tsv files.
---

# generate-questions

Create or update Blackboard question import files from module content.

## Scope

Use this skill for content under `Course/nl/Modules/*` and `Course/en/Modules/*`, and generate `Course/<lang>/Modules/*/questions.tsv` — one question bank per module **per language**.

Determine the language from the path (`Course/nl/...` or `Course/en/...`) before generating. If the user asks for a question bank without specifying, ask which language(s) to generate, or default to generating both if question banks already exist for the module in both languages.

Read the module's existing chapter content first, in the target language, especially:

- `Course/<lang>/Modules/*/00-objectives.adoc`
- `Course/<lang>/Modules/*/*.adoc` chapter files

Derive the questions from the actual module content in that language. The `nl` and `en` question banks are independent files — they don't need to be literal translations of each other, but should test the same underlying facts where the two language versions of the chapter cover the same content.

## Required Output File

- File name must be questions.tsv in each module folder.
- File must be tab-delimited (TSV).
- Do not include a header row.
- Do not include blank lines.
- Put exactly one question on each row.
- Use English answer markers only: correct, incorrect, true, false.
- Avoid open questions entirely in this workflow; use multiple choice or true/false only.

## Helper Examples

Use [examples/questions-template.tsv](examples/questions-template.tsv) as a starter pattern when you want a copyable Blackboard-ready layout.

The example file shows:

- one multiple choice row
- one true/false row

## Blackboard Row Formats

### Multiple Choice

Format:

MC<TAB>question text<TAB>answer 1<TAB>correct|incorrect<TAB>answer 2<TAB>correct|incorrect [...]

Example:

MC	Wat is phishing?	Een frauduleuze poging om gegevens te stelen	correct	Een type cloudopslag	incorrect	Een Windows-instelling	incorrect

### True/False

Format:

TF<TAB>question text<TAB>true|false

Example:

TF	Een sterk wachtwoord bevat verschillende tekentypes.	true

### Open questions are not supported here

Do not generate FIB rows for this workflow. If the source content would lead to an open question, rewrite it as multiple choice or true/false.

[WARNING]
====
Open questions are hard to auto-grade reliably in Blackboard. Keep this skill restricted to MC and TF rows.
====

## Mapping Rules from Module Content

- Multiple Choice questions based on module content map to MC rows.
- True/False questions based on module content map to TF rows.
- Open questions must not be generated.
- Rewrite any prompt that would become an open question into MC or TF instead.

## Question Design Rules

- Base each question on a concrete fact, concept, procedure, or distinction that is clearly present in the module content.
- Prefer questions that can be answered unambiguously from the module text.
- Prefer multiple choice questions when the module contains a definition, comparison, or best-practice distinction.
- Prefer true/false questions for simple factual checks that have a clear binary answer.
- Do not use fill-in-the-blank for this auto-graded workflow.
- Avoid guessing from tone or from examples that are not explicitly taught in the module.
- Keep distractors plausible but clearly incorrect according to the module content.

## Normalization Rules

- Keep question and answer text in the module's target language (Dutch for `Course/nl/...`, English for `Course/en/...`).
- Keep Blackboard control words in English regardless of language (correct, incorrect, true, false).
- Preserve the logical order from the module content when choosing answer options.
- Ensure exactly one correct option for MC rows unless the source explicitly requires multiple answers.
- Escape or rewrite text that contains tabs so each field stays valid.

## Validation Checklist

Before finalizing a questions.tsv file, verify:

1. File extension is .tsv.
2. Delimiter is TAB, not comma or semicolon.
3. No header row exists.
4. No empty rows exist.
5. Every row starts with a valid question type token (MC or TF only).
6. Every MC row has at least two answer options and at least one correct marker.
7. Every TF row ends with true or false in lowercase.

## Recommended Workflow

1. Read the module objectives and chapter content.
2. Extract a small set of assessable facts, definitions, procedures, and distinctions from the module.
3. Draft one TSV row per question using the format table above, using MC or TF only.
4. Save as questions.tsv in the same module folder.
5. Run a quick scan for tabs, blank lines, and control words.
6. Import into Blackboard and verify no row-level import errors.

## Common Mistakes

- Using .csv extension for tab-delimited content.
- Using localized markers such as juist/onjuist instead of correct/incorrect.
- Adding explanatory lines between rows.
- Leaving open questions in the source material without rewriting them into MC or TF.
