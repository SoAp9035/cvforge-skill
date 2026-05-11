---
name: cvforge
description: Create, edit, build, and troubleshoot CVForge resumes from YAML into ATS-friendly PDFs. Use when working with cv.yaml files, CVForge resume content, Typst resume generation, font/photo options, or ATS checks with the cvforge CLI.
license: MIT
compatibility: Requires CVForge CLI available as cvforge or uvx cvforge; shell access is needed for PDF build and ATS checks.
---

# CVForge

Use this skill when helping a user create, edit, generate, or validate a
CVForge resume.

## Workflow

1. Inspect the existing resume YAML before changing it. If none exists, create
   one with `cvforge init` or use the schema in
   [references/cvforge-reference.md](references/cvforge-reference.md).
2. Preserve factual resume content. Do not invent employers, schools, dates,
   credentials, links, metrics, or personal details. If content is missing,
   leave a clear placeholder or ask the user.
3. Keep YAML valid and compatible with CVForge. Prefer the documented fields
   and list shapes; do not add arbitrary top-level sections unless the user
   also wants CVForge template/code changes.
4. Build with `cvforge <file>.yaml` or `cvforge build <file>.yaml`.
5. Validate the generated PDF with `cvforge ats-check <file>.pdf` when a PDF is
   produced.
6. Report the output path and any ATS warnings or build errors that matter.

## Content Rules

- Treat resume data as private local content.
- Use concise, achievement-focused bullets with truthful scope.
- Prefer measurable outcomes only when the user supplied the numbers.
- Use `__text__` for inline bold emphasis in narrative fields.
- Keep section names and fields compatible with the CVForge schema.

## Reference

Read [references/cvforge-reference.md](references/cvforge-reference.md) when
you need command examples, YAML field details, fonts, ATS guidance, or build
troubleshooting.
