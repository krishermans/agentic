# Agentic courses

Skills, agents & instructions for agentic courses

## Getting started

### APM - Agent Package Manager

- install [https://microsoft.github.io/apm/](https://microsoft.github.io/apm/)

### Create an APM project

```
apm init
```

### Install

#### Instructions

```
apm install krishermans/agentic/instructions/course-authoring.instructions.md
apm install krishermans/agentic/instructions/pdf-adoc-assembly.instructions.md
```

#### Skills

```
apm install krishermans/agentic/skills/new-chapter
apm install krishermans/agentic/skills/translate-chapter
apm install krishermans/agentic/skills/validate-chapter
apm install krishermans/agentic/skills/generate-objectives
apm install krishermans/agentic/skills/generate-questions
```

### Update

Updates to skills, agents & instructions can easily be installed afterwards:

```
apm update
```

### COURSE.md

- Create a `COURSE.md` file in the root directory of your project
- Use the template below as a starting point
- Fill in the name and description of your course

> [!TIP]
> You can ask Claude to fill in this file based on an existing course 😉

> [!NOTE]
> This template assumes a course in two languages (Dutch and English), under `Course/nl/` and `Course/en/`.
> Module and chapter structure is tracked once; only the status column is separate per language.

```markdown
# Content Plan

This file is the single source of truth for the module and chapter structure of this course.
Agents (Claude, GitHub Copilot) MUST consult this file before creating or numbering any module or chapter.

The course is written in two languages, Dutch (`nl`) and English (`en`), under `Course/nl/` and `Course/en/`.
Module and chapter structure (folders, numbering, filenames) is shared across both languages — this table lists it once, with a separate status column per language.

## Course Overview

- **Title**: ... 
- **Description**: ...

## Status values

| Symbol | Meaning |
|--------|---------|
| planned | not yet started |
| in progress | being written |
| done | completed WITHOUT fails |
| failed | completed but WITH fails |

## Modules and Chapters

| #  | Folder | Module title | Chapter file | Chapter title | Status (NL) | Status (EN) |
|----|--------|--------------|--------------|---------------|--------------|--------------|

```

## Prompts

### From scratch

You can now write a simple prompt to create a new chapter:

```text
create a new chapter in module 1 called "introduction". the chapter must contain a brief summary of the course with a detailed planning.
```

By default, the chapter is created in both languages. If you only want one language, say so explicitly:

```text
create the English version of the chapter about loops in module 2 first, I'll translate it to Dutch later.
```

Use `/translate-chapter` afterwards to generate the other language version based on an existing chapter.

### From COURSE.md

You can also add content to the `COURSE.md` file yourself and then ask Claude to generate these chapters.

## .gitignore

Use the `.gitignore` file to exclude unnecessary files
