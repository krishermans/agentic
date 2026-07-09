---
name: validate-chapter
description: Check an existing AsciiDoc chapter file against the course quality rules and report any violations as a PASS/FAIL table. Use this skill whenever the user asks to check, review, validate, audit, or verify a chapter — or asks whether a file follows the course rules. Examples "does this chapter comply?", "review my adoc file", "check chapter quality", "validate the new section", "is this file correct?", "run a quality check on this chapter".
---

# validate-chapter

Audit an existing AsciiDoc chapter file against the course quality rules and produce a PASS/FAIL report.

## Input

The user provides a file path, or the file is currently open/selected in the IDE. If no file is specified and none is clearly implied, ask the user which file to check before proceeding.

If the file does not exist at the given path, report that immediately and stop — do not attempt the checks.

Read the full file content before running any checks.

Determine the chapter's language from its path: files under `Course/nl/...` are Dutch, files under `Course/en/...` are English. Several checks below depend on this.

## Checks to perform

Run every check below. For each one, report PASS or FAIL with a short explanation of what was found.

### 1. Standard document header
- First line is `= {Course Title}`
- Second line is the program name (consistent with sibling chapters in the same language root)
- All required attributes are present: `:doctype:`, `:source-language:`, `:imagesdir:`, `:icons:`, `:sectnums:`, `:toc:`, `:toc-title:`, `:toclevels:`, `:nofooter:`, `:sectlinks:`
- `:toc-title:` matches the file's language: `Inhoudsopgave` for `nl`, `Table of contents` for `en`

### 2. Discrete headings
- Module name is a `[discrete]` `==` heading
- Chapter title is a `[discrete]` `===` heading immediately after

### 3. Opening sentence
- The first paragraph after the chapter title starts with `In dit hoofdstuk leer je` (Dutch) or `In this chapter, you will learn` (English), matching the file's language

### 4. Thematic break and TOC
- A `'''` line appears before `toc::[]`

### 5. Body language
- Body text matches the file's language root: Dutch under `nl`, English under `en` (spot-check: flag any paragraph written in the wrong language, with the line number)

### 6. Spelling
- Scan body text (excluding code blocks) for obvious spelling errors in the file's language — list any misspelled words with the suggested correction. If none found, mark PASS.

### 7. Code blocks tagged
- Every code block uses an explicit `[source,<lang>]` tag — no untagged fences or bare `----` blocks

### 8. No foreign identifiers in code
- Spot-check code blocks: flag any non-English variable names, method names, or identifiers (code is always English, regardless of the chapter's language)

### 9. External links
- Every external `http://` or `https://` link ends with the `^` modifier inside `[...]`

### 10. Summary section
- File ends with a summary section followed by a bullet list: `== In het kort` (Dutch) or `== Summary` (English), matching the file's language
- Skip this check (mark N/A) if:
  - the chapter title contains "Labo" or "Lab", or
  - the file is a module objectives/overview file (filename starts with `00-`)

### 11. File and folder naming
- File name is kebab-case, English words only, with a numeric prefix (e.g. `03-exception-handling.adoc`)
- File lives inside `Course/<lang>/Modules/<module-folder>/`, where `<lang>` is `nl` or `en`

### 12. COURSE.md registration
- Read `COURSE.md` and confirm this chapter file is listed with the correct module folder and title, and that the status column for this chapter's language is not blank

### 13. Language pairing
- Check whether the counterpart chapter file exists at the same path under the other language root (swap `nl` ↔ `en`, same module folder, same filename)
- If missing, this is not necessarily a FAIL (the counterpart may not be written yet) — report it as a note, and suggest running `/translate-chapter` to create it
- If both exist, do a light structural comparison (same `==`/`===` heading count and order); flag drift as a note, not a FAIL, since prose length naturally differs between languages

## Output format

Print a Markdown table:

| Check | Result | Notes |
|-------|--------|-------|
| Standard header | PASS/FAIL | ... |
| Discrete headings | PASS/FAIL | ... |
| Opening sentence | PASS/FAIL | ... |
| Thematic break + TOC | PASS/FAIL | ... |
| Body language | PASS/FAIL | ... |
| Spelling | PASS/FAIL | ... |
| Code blocks tagged | PASS/FAIL | ... |
| No foreign identifiers | PASS/FAIL | ... |
| External links (^) | PASS/FAIL | ... |
| Summary section | PASS/FAIL/N/A | ... |
| File naming | PASS/FAIL | ... |
| COURSE.md entry | PASS/FAIL | ... |
| Language pairing | INFO | ... |

After the table, list only the FAILs with a brief, actionable fix suggestion for each.

If all checks pass (no FAILs), say so clearly.

## COURSE.md status update

After printing the report, **ask the user** whether to update this chapter's status in COURSE.md for the language just checked:
- If there are no FAILs → offer to set that language's status to `done`
- If there are FAILs → offer to set that language's status to `failed`

Only update COURSE.md if the user confirms.
