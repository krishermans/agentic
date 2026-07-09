---
name: translate-chapter
description: Create or resync the Dutch/English counterpart of an existing chapter file so both language versions stay structurally in sync. Use this skill whenever the user asks to translate a chapter, create the other-language version, sync languages, or catch up a chapter that only exists in one language. Examples "translate this chapter to English", "create the Dutch version of this chapter", "sync the en and nl versions of chapter 3", "this chapter is missing in English".
---

# translate-chapter

Create or update the counterpart of a chapter file in the other language root (`Course/nl/` ↔ `Course/en/`), keeping structure identical while writing independent, natural prose per language.

## Input

The user provides a source file path (or it's open/selected in the IDE), or names a chapter well enough to locate it under `Course/nl/Modules/` or `Course/en/Modules/`. If ambiguous, ask which chapter and which direction (nl→en or en→nl) before proceeding.

Determine the source language from the file's path (`Course/nl/...` or `Course/en/...`) and the target language as the other one.

## Steps

1. **Read the source file** in full.

2. **Compute the target path** by swapping the language segment: `Course/nl/Modules/<module>/<file>.adoc` ↔ `Course/en/Modules/<module>/<file>.adoc`. The filename, module folder, and numeric prefix MUST stay identical — only the language segment changes.

3. **Check whether the target already exists**:
   - If it doesn't exist, this is a **fresh translation** — proceed to step 4 for the whole file.
   - If it already exists, this is a **resync** — diff the two files section by section (by `==`/`===` heading structure, not prose). Report which sections are missing, extra, or reordered in the target, and ask the user to confirm before overwriting existing translated prose. Never silently discard existing translated content — only fill gaps or fix structural drift unless the user explicitly asks for a full re-translation.

4. **Produce the target content**:
   - Header: use the language-appropriate template from the `new-chapter` skill (`:toc-title:` and the program-name line change; keep the same `<Course Title>` and `<Module Name>`/`<Chapter Title>` translated appropriately)
   - Opening sentence: translate `In dit hoofdstuk leer je ...` ↔ `In this chapter, you will learn ...`, keeping the same concrete claim about what the reader learns
   - Body prose: written independently and naturally in the target language — not a literal word-for-word translation — but covering the **same sections, same examples, and same claims** in the **same order**
   - Code blocks: copy unchanged. Code identifiers and code comments are always English in both language versions, regardless of translation direction
   - Admonitions (`[TIP]`, `[WARNING]`): translate the text, keep the block structure
   - External links: keep the same URL and the `^` modifier; translate link text only if the source used custom (non-URL) link text
   - `// TODO` comments: carry over untranslated (they're authoring notes, not reader-facing content) unless the user asks to translate them too
   - Summary section: `== In het kort` ↔ `== Summary`, translate the bullet list, keep the same number of takeaways covering the same points

5. **Write the target file.**

6. **Update COURSE.md** — set the target language's status column for this chapter to `in progress` (or `done` if the user confirms it's a finished translation, not a draft).

7. **Update pdf.adoc** — if the source chapter is already included in its language's `pdf.adoc` but the target chapter is missing from the target language's `pdf.adoc`, add the corresponding entry there too, following the PDF assembly instructions.

8. **Report** — tell the user the target file path, and flag anything you weren't confident translating (idioms, domain terms without an obvious equivalent) so they can review it.

## Notes

- This skill produces a **draft** translation for human review, not a final publish-ready text — tell the user to proofread it, especially technical terminology.
- Never translate code identifiers, method names, or file paths that appear inside code blocks.
- If the source chapter fails `/validate-chapter`, mention this to the user — fixing the source first usually saves a re-translation later.
