---
description: "Use when creating new modules, chapters, code examples, exercises, admonitions, hyperlinks, images, or updates to course content in AsciiDoc format"
applyTo: "Course/**/*.adoc"
---

# Course Authoring Instructions

## Purpose

This repository contains course material written in AsciiDoc.
Agents working in this repository MUST produce content that matches the existing course structure and writing style.

The goal is to create complete course material as a set of modules and chapters.

## Scope

These instructions apply to all content created under `Course/`.

Use these rules when you:

- create a new module
- create a new chapter
- update an existing chapter
- propose file or folder names inside the course root
- add code examples, exercises, notes, warnings, tables, or images to a chapter

## Repository Structure

- the course is written in two languages: Dutch (`nl`) and English (`en`)
- each language has its own root: `Course/nl/` and `Course/en/`
- module and chapter structure — folder names, numeric prefixes, and chapter filenames — MUST be identical across both language roots; only the file content, in-file titles, and prose differ
- a course contains multiple modules
- every module is a separate subfolder inside `Course/<lang>/Modules/`
- every module starts with a `00-objectives.adoc` file
- every module contains one or more additional chapter files
- every chapter is a separate `.adoc` file
- module assets belong inside the module folder
- chapter images belong in the local `images/` folder of that module, inside the matching language root — duplicate an image per language when it contains localized text (e.g. a screenshot with UI labels); shared, text-free diagrams may simply be copied to both
- code solutions, demos, or sample projects MAY be stored in a local `source/` folder when needed; code identifiers and comments stay in English regardless of language root, so this folder's content is usually identical between `nl` and `en`

Example:

```text
Course/
	nl/
		Modules/
			05-minimal-api/
				00-objectives.adoc
				01-intro.adoc
				02-results.adoc
				images/
				source/
	en/
		Modules/
			05-minimal-api/
				00-objectives.adoc
				01-intro.adoc
				02-results.adoc
				images/
				source/
```

## Naming Rules

Agents MUST use kebab-case for all file and folder names inside `Course/`:

- lowercase letters only
- English words only — no Dutch or other languages
- words separated by hyphens; no spaces, no underscores
- keep the existing numeric prefix pattern for order
- do not rename existing files or folders unless explicitly asked

Examples: `03-api` (valid), `04-labo-template.adoc` (valid), `03_API` (invalid), `04 Labo Template.adoc` (invalid)

## Writing Style

Chapter content language depends on the language root the file lives in:

- files under `Course/nl/...` MUST be written in Dutch, using the `je` form consistently
- files under `Course/en/...` MUST be written in English, addressing the reader directly ("you")

Both language versions of a chapter MUST:

- keep the tone educational, professional but approachable
- start with a short orientation sentence, then build the explanation step by step
- prefer short, readable paragraphs with concrete examples
- keep each chapter short and focused: introduction → explanation → example → practical usage
- use AsciiDoc elements when useful: bullet lists, numbered lists, tables, NOTE blocks, CAUTION blocks
- keep terminology consistent across chapters and align with the existing course progression
- cover the same sections, examples, and code blocks as the counterpart chapter in the other language root — the two versions MUST stay structurally in sync, even though the prose is independently written per language
- Avoid AI artifacts: curly quotes (' " "), emdashes (—), and filler phrases ("In this section we will discuss...", "Why this is important:").
- Avoid overuse of bold-bullet-point lists in the pattern "Term: explanation".

Use `/translate-chapter` to create or resync the counterpart of a chapter in the other language.

## Admonitions

When obvious tips or pitfalls exist, make them visible with an admonition block:

- use `[TIP]` for best practices — things a student should do to work effectively
- use `[WARNING]` for bad practices — things a student should avoid because they cause problems

AsciiDoc admonition block pattern:

```adoc
[TIP]
====
Tip text here.
====

[WARNING]
====
Warning text here.
====
```

Agents MUST NOT bury best-practice or bad-practice advice in plain paragraph text when an admonition block would make it stand out.

## Code Example Rules

- code examples use English variable names
- code comments are written in English
- code blocks always use an explicit AsciiDoc source tag with the correct language (`csharp`, `json`, `bash`, `powershell`, or `text`)
- code must be minimal but realistic and support the surrounding Dutch explanation
- code should reflect current .NET and ASP.NET Core practices where relevant
- if a code example is intentionally incomplete, mark it with a `TODO` label in the text or code

AsciiDoc code block pattern:

```adoc
[source,csharp]
----
public class InvoiceService
{
    private readonly Calculator _calculator;

    public InvoiceService(Calculator calculator)
    {
        _calculator = calculator;
    }
}
----
```

Agents MUST NOT:

- mix Dutch variable names into code examples
- use untagged code fences where an AsciiDoc source block is required
- add oversized listings when a smaller example explains the concept better

## Hyperlinks

All external hyperlinks MUST open in a new browser tab.
In AsciiDoc, add `^` at the end of the link text to achieve this:

```adoc
https://example.com[https://example.com^]
```

By default, the link text is equal to the link URL.
Only use a different link text when there is a clear reason (e.g. the URL is too long to display meaningfully).

Agents MUST NOT write external links without the `^` modifier.

## Images And Assets

- store images in the module-local `images/` folder
- use kebab-case file names
- `:imagesdir: images` is active in every chapter header

## Diagrams

Mermaid is the preferred format for diagrams in chapter content (flowcharts, sequence diagrams, class diagrams, etc.).

AsciiDoc mermaid block pattern:

```adoc
[mermaid]
....
graph TD
    A[Request] --> B[Controller]
    B --> C[Service]
    C --> D[Database]
....
```

- keep diagrams small and focused on the concept being explained; do not diagram trivial flows
- diagram labels and text follow the same language rule as the surrounding chapter (Dutch in `nl`, English in `en`)
- when both language versions of a chapter need the same diagram, keep the structure identical and translate only the labels

Agents MUST NOT add, generate, or modify a diagram on their own initiative, under any circumstance. This applies whether a diagram is missing, outdated, or could simply improve a section. Whenever a diagram seems useful, stop and ask the user whether to create or update it together before writing any mermaid code. Only add or change a diagram after the user has agreed on its content in that conversation.

## Course Content Plan

The full list of modules and chapters for this course is maintained in `COURSE.md` at the repository root.

Consult `COURSE.md` before:

- creating a new module or chapter
- deciding on module or chapter numbering
- choosing a title or topic for new content

`COURSE.md` is the single source of truth for which modules exist or are planned, their numeric prefixes, chapter order, and status. It tracks module/chapter structure once — shared by both languages — with a separate status column per language (`Status (NL)`, `Status (EN)`). Update the relevant status column(s) when content is added or completed in that language.

Agents MUST NOT invent module numbers, folder names, or chapter titles that contradict `COURSE.md`.

## Skills

Use these skills for structured tasks:

- `/new-chapter` — scaffold a new chapter file (in one or both languages) with the correct header and register it in `COURSE.md`
- `/translate-chapter` — create or resync a chapter's counterpart in the other language
- `/validate-chapter` — check an existing chapter against all course quality rules and get a PASS/FAIL report
