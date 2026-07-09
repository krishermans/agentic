---
name: new-chapter
description: Scaffold a new AsciiDoc chapter file that complies with the course structure, in one or both languages, and register it in COURSE.md. Use this skill whenever the user asks to create, add, write, or start a new chapter, section, or lesson — even if they don't say "scaffold" or "AsciiDoc". Examples "add a chapter about exceptions", "create a new section on APIs", "start chapter 3 in module 5", "write the intro chapter for loops".
---

# new-chapter

Create a new AsciiDoc chapter file that follows the course structure and writing style, for Dutch (`nl`), English (`en`), or both.

## Steps

1. **Consult COURSE.md** — read `COURSE.md` to find the correct module folder, numeric prefix for the new chapter file, and the exact chapter title. Never invent a number or title that contradicts COURSE.md. Module/chapter structure is shared across languages, so this step only needs to happen once regardless of which language(s) you scaffold.

2. **Determine target language(s)** — if the user's request names a language (or the request is clearly scoped to one language root, e.g. a path under `Course/en/...`), scaffold only that language. Otherwise ask the user whether to create the Dutch version, the English version, or both. Default to **both** when the user simply says "create a chapter" without qualification, since every chapter is expected to eventually exist in both languages.

3. **Determine the file path(s)** — for each target language, construct the path as:
   `Course/<lang>/Modules/<module-folder>/<nn>-<kebab-title>.adoc`
   - `<lang>` is `nl` or `en`
   - use the next available numeric prefix in the module (same number in both languages)
   - filename must be kebab-case, English words only, identical between `nl` and `en` versions of the same chapter

4. **Ensure the images folder exists** — for each target language, if `Course/<lang>/Modules/<module-folder>/images/` does not exist, create it (place a `.gitkeep` inside so it is tracked by git).

5. **Write the file(s)** — each file MUST start with the header for its language (fill in Course Title, Program Name, Module Name, and Chapter Title).

   Dutch header (`Course/nl/...`):

   ```adoc
   = <Course Title>
   <Program Name>
   :doctype: article
   :source-language: csharp
   :imagesdir: images
   :icons: font
   :sectnums:
   :toc: macro
   :toc-title: Inhoudsopgave
   :toclevels: 3
   :nofooter:
   :sectlinks:

   [discrete]
   == <Module Name>
   [discrete]
   === <Chapter Title>
   In dit hoofdstuk leer je ...

   '''

   toc::[]

   == <Eerste sectietitel>
   ```

   English header (`Course/en/...`):

   ```adoc
   = <Course Title>
   <Program Name>
   :doctype: article
   :source-language: csharp
   :imagesdir: images
   :icons: font
   :sectnums:
   :toc: macro
   :toc-title: Table of contents
   :toclevels: 3
   :nofooter:
   :sectlinks:

   [discrete]
   == <Module Name>
   [discrete]
   === <Chapter Title>
   In this chapter, you will learn ...

   '''

   toc::[]

   == <First section title>
   ```

   `<Program Name>` is the official program name in that language (e.g. the Dutch degree title and its official English equivalent). Ask the user once if it isn't already established elsewhere in the course, and reuse the same value across chapters within a language.

   Writing rules:
   - Complete the opening sentence (`In dit hoofdstuk leer je ...` / `In this chapter, you will learn ...`) with a concrete statement about what the reader will learn
   - Body text is written in the language of the file: Dutch (`je`-form) under `nl`, English (direct "you") under `en` — professional but approachable in both
   - Structure: introduction → explanation → example → practical usage — identical structure in both languages
   - Code blocks use `[source,<lang>]` (e.g. `csharp`, `json`, `bash`) with English variable names and English comments in **both** language versions — code never changes between `nl` and `en`
   - External links must include the `^` modifier: `https://example.com[https://example.com^]`
   - Unless this is a labo/lab chapter (title contains "Labo" or "Lab") or a module objectives/overview file (`00-`), end the file with a summary section followed by a short bullet list summarising the key takeaways: `== In het kort` (Dutch) or `== Summary` (English)

6. **Draft starter content** — after the header, write at least the first section with a short orientation paragraph and one concrete example (code block if appropriate), in each target language. Leave a `// TODO` comment where further sections are expected so the author knows where to continue. When scaffolding both languages, keep the section structure and examples identical between them — only the prose differs.

7. **Update COURSE.md** — add a row for the new chapter in the correct position (once, not per language). Set the status column(s) for the language(s) just scaffolded to `in progress`; leave the other language's status as `planned` if it wasn't scaffolded. Use the same column format as existing rows:
   `| <#> | <folder> | <Module title> | <filename> | <Chapter title> | <Status (NL)> | <Status (EN)> |`

8. **Update pdf.adoc** — for each target language, open `Course/<lang>/Modules/<module-folder>/pdf.adoc` and add an entry for the new chapter:
   - Append `<<<` as a page break separator
   - Add the section heading (in that language) matching the chapter's first top-level section title
   - Add the include directive: `include::<filename>[leveloffset=+1,lines=24..-1]`
   - Insert the entry after the last existing numbered chapter entry, maintaining numeric order
   - If `pdf.adoc` does not yet exist for that module/language, create it using the standard template from the PDF assembly instructions

9. **Report** — tell the user which language file(s) were created (file paths), and confirm the COURSE.md row and pdf.adoc entry were added. If only one language was scaffolded, remind the user that `/translate-chapter` can create the counterpart later.
