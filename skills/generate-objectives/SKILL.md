---
name: generate-objectives
description: Use when creating or updating a 00-objectives.adoc file for a course module so it matches the repository structure, writing style, and measurable objective phrasing — in Dutch or English depending on the language root.
---

# generate-objectives

Create or update a `00-objectives.adoc` chapter for a module using the standard course format and objective phrasing, in the language of the file's location.

## Scope

Use this skill for files under `Course/nl/Modules/*/00-objectives.adoc` (Dutch) and `Course/en/Modules/*/00-objectives.adoc` (English).

Determine the language from the path before writing anything: `Course/nl/...` → Dutch, `Course/en/...` → English. If the user asks for objectives without specifying a language or path, ask whether to generate the Dutch version, the English version, or both — module learning objectives should exist in both languages, but they are two independently-phrased files, not a literal translation of each other (see [[translate-chapter]] if a translation pass is wanted instead of independent phrasing).

## Required Output Structure

The file should follow this exact section order:

1. Standard AsciiDoc header
2. Discrete module title (`== <Module Name>`)
3. Discrete subsection `=== Doelstellingen` (Dutch) / `=== Objectives` (English)
4. One short orientation sentence (Dutch: `In dit hoofdstuk leer je wat je na het afronden van deze module kunt doen.` / English: `In this chapter, you'll find out what you'll be able to do after completing this module.`)
5. The separator line (`'''`)
6. `toc::[]`
7. `== Overzicht` (Dutch) / `== Overview` (English) with a concise module summary
8. `== Leerdoelstellingen` (Dutch) / `== Learning Objectives` (English)
9. Objective list introduced by `Na het afronden van deze module kan je:` (Dutch) / `After completing this module, you will be able to:` (English)

## Header Template

```adoc
= <Course Title>
<Program Name>
:doctype: article
:source-language: csharp
:imagesdir: images
:icons: font
:sectnums:
:toc: macro
:toc-title: <Inhoudsopgave (nl) / Table of contents (en)>
:toclevels: 3
:nofooter:
:sectlinks:
```

## Objective Phrasing Rules — Dutch (`Course/nl/...`)

- Write all prose in Dutch and use the `je` form.
- Formulate each objective from student behavior (implicit form: `je kan ...`; attitude goals: `je wil ...`).
- Ensure each bullet is grammatically correct when read directly after `Na het afronden van deze module kan je:`.
- Prefer the Dutch pattern `object/complement + infinitive` (for example: `de rol van ... beschrijven`, `een app opstarten`, `configuratie terugvinden`).
- Start each objective with an action-oriented infinitive verb (`uitleggen`, `vergelijken`, `aanmaken`, `instellen`, `bouwen`, `beschrijven`, `opzetten`, `registreren`, `gebruiken`, `integreren`).
- Use observable action verbs only. Avoid vague verbs such as `kennen`, `begrijpen`, `inzien`, `weten`.
- Keep objectives concrete and assessable: each item should describe observable behavior.
- Keep each objective single-action (one observable handeling per bullet).
- Make content specific and unambiguous (avoid broad placeholders like `de microscoop hanteren` without context).
- Prefer domain-specific wording over vague statements (`correct inzetten`, `thread-safe ... garanderen`, `de juiste keuze maken voor een gegeven context`).
- Keep a consistent level of detail across items.
- Use one bullet per objective.
- Add conditions or minimum performance criteria only when they are instructionally relevant and measurable.
- Keep code identifiers and framework types in English where relevant (for example `NavigationManager`, `EventCallback`, `EditForm`, `IDbContextFactory<T>`).

### Dutch Grammar Guardrails (mandatory)

- Reject nominalized forms that break the sentence after `kan je`, such as:
	- `beschrijven van ...`
	- `opstarten van ...`
	- `terugvinden van ...`
	- `toepassen van ...`
- Rewrite those to valid forms:
	- `de rol van ... beschrijven`
	- `een app opstarten`
	- `platformspecifieke configuratie terugvinden`
	- `basis-XAML-syntax toepassen`
- During review, read every bullet aloud with the lead-in sentence to validate fluency and grammar.

## Objective Phrasing Rules — English (`Course/en/...`)

- Write all prose in English, addressing the reader directly ("you").
- Formulate each objective from student behavior (`you can ...` / `you will be able to ...`, implicit before the bullet).
- Ensure each bullet is grammatically correct when read directly after `After completing this module, you will be able to:`.
- Use the pattern `base-form verb + object/complement` (for example: `describe the role of ...`, `start up an app`, `look up platform-specific configuration`).
- Start each objective with a base-form (infinitive-without-"to") action verb (`explain`, `compare`, `create`, `configure`, `build`, `describe`, `set up`, `register`, `use`, `integrate`).
- Use observable action verbs only. Avoid vague verbs such as `know`, `understand`, `be aware of`, `learn about`.
- Keep objectives concrete and assessable: each item should describe observable behavior.
- Keep each objective single-action (one observable behavior per bullet).
- Make content specific and unambiguous (avoid broad placeholders like `use the tool` without context).
- Prefer domain-specific wording over vague statements (`apply correctly`, `guarantee thread-safe ...`, `choose the right approach for a given context`).
- Keep a consistent level of detail across items.
- Use one bullet per objective.
- Add conditions or minimum performance criteria only when they are instructionally relevant and measurable.
- Keep code identifiers and framework types as-is (for example `NavigationManager`, `EventCallback`, `EditForm`, `IDbContextFactory<T>`).

### English Grammar Guardrails (mandatory)

- Reject gerund (`-ing`) or noun-form openings that break the sentence after `you will be able to`, such as:
	- `describing ...`
	- `starting up ...`
	- `looking up ...`
	- `the application of ...`
- Rewrite those to valid base-form forms:
	- `describe the role of ...`
	- `start up an app`
	- `look up platform-specific configuration`
	- `apply basic XAML syntax`
- During review, read every bullet aloud with the lead-in sentence to validate fluency and grammar.

## Quality Checklist

Before finalizing, verify:

- The filename is exactly `00-objectives.adoc`, under the correct `Course/<lang>/Modules/<module-folder>/` path.
- The module name in the discrete title matches the module folder topic.
- The intro sentence matches the file's language and starts with the required lead-in.
- The overview section is present and concise.
- The learning objectives section contains clear, measurable bullet points.
- Every objective is phrased as observable student behavior, correctly following the lead-in sentence for that language.
- Every objective is grammatically correct after the lead-in sentence (no nominalization in Dutch, no gerund/noun opening in English).
- Every objective uses an observable action verb (not a vague verb like `kennen`/`begrijpen` or `know`/`understand`).
- Every objective is single-action and concrete in content.
- No objective is duplicated or overly broad.
- Terminology is consistent with nearby chapters in the same module and language.
- If a counterpart file exists in the other language, its objectives cover the same ground (same number and scope of objectives), even though phrased independently.

## Notes

- Keep this file as a temporary skill draft in the repository root.
- If promoted to a reusable skill, move it to a dedicated skill folder with filename `SKILL.md`.
