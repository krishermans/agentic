# Agentic courses

Skills, agents & instructions for agentic courses

## Getting started

### APM - Agent Package Manager

- installeer [https://microsoft.github.io/apm/](https://microsoft.github.io/apm/)

### APM project aanmaken

```
apm init
```

### Installeer

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

Updates van skills, agents & instructies kunnen achteraf heel eenvoudig geïnstalleerd worden:

```
apm update
```

### COURSE.md

- Maak een `COURSE.md` bestand aan in de root-directory van je project
- Gebruik onderstaande template als beginpunt
- Vul de naam en omschrijving van je cursus in

> [!TIP]
> Je kan copilot vragen om dit bestand aan te vullen op basis van een reeds bestaande cursus 😉

> [!NOTE]
> Deze template gaat uit van een cursus in twee talen (Nederlands en Engels), onder `Course/nl/` en `Course/en/`.
> Module- en hoofdstukstructuur wordt één keer bijgehouden; enkel de statuskolom is per taal apart.

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

Je kan nu een eenvoudige prompt schrijven om een nieuw hoofdstuk aan te maken:

```text
create a new chapter in module 1 called "introductie". the chapter must contain a brief summary of the course with a detailed planning.
```

Standaard wordt het hoofdstuk in beide talen aangemaakt. Wil je maar één taal, zeg dat er expliciet bij:

```text
create the English version of the chapter about loops in module 2 first, I'll translate it to Dutch later.
```

Gebruik `/translate-chapter` om nadien de andere taalversie te genereren op basis van een bestaand hoofdstuk.

### From COURSE.md

Je kan ook zelf inhoud toevoegen aan het `COURSE.md`-bestand en daarna vragen aan copilot om deze hoofdstukken te genereren.

## .gitignore

Gebruik het `.gitignore`-bestand om overbodige bestanden uit te sluiten
