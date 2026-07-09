---
description: "Use when creating or updating Course/<lang>/Modules/*/pdf.adoc files that aggregate module chapters into one PDF source."
applyTo: "Course/*/Modules/*/pdf.adoc"
---

# PDF Assembly For Module Chapters

Use these rules when building a `pdf.adoc` file inside a module folder.

Each language root (`Course/nl/`, `Course/en/`) has its own `pdf.adoc` per module — build them independently, only combining chapter files from the same language root.

## Doel

A module `pdf.adoc` combines all chapter files from the same module and the same language root, in the correct order.

## Required File Selection

- Include only chapter files whose filename starts with a number (`^[0-9]`).
- Exclude `00-objectives.adoc` (learning objectives do not belong in the chapter bundle).
- Exclude `pdf.adoc` itself.
- Ignore non-numbered files such as `extra.adoc`, `labo.adoc`, `oefeningen.adoc`, or any file without a numeric prefix.

## Order

- Sort selected chapter files in ascending order by numeric prefix (for example `01-...`, `02-...`, `10-...`).
- Add a page break `<<<` for each included chapter.

## Include Rules

- For each chapter, use an include with `leveloffset=+1`.
- The `lines=` value must always start at the line of the first section title after the document TOC in that chapter file.
- Use this include shape:

[source,adoc]
----
== <chapter-title>
include::<chapter-file>.adoc[leveloffset=+1,lines=<start-line>..-1]
----

## Determining The Start Line

- In each chapter file, find the first section title (`== ...`) that appears after the header attributes and `toc::[]`.
- Use the line number of that section title as `<start-line>` in the include.
- Do not hardcode fixed line numbers without checking each file.

## Checklist

- All numbered chapter files (except `00-objectives.adoc`) are included.
- No non-numbered chapter files are included.
- Every include uses `leveloffset=+1`.
- Every include starts at the first section title after the TOC in the chapter file.