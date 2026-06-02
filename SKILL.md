---
name: cvforge-skill
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
3. Keep YAML valid and compatible with CVForge. Respect the documented section
   order because CVForge renders supported sections in YAML order.
4. Use only documented top-level fields unless the user also asks for template
   or code changes. Keep section list shapes exactly as documented.
5. Build with `cvforge <file>.yaml` or `cvforge build <file>.yaml`.
6. Validate the generated PDF with `cvforge ats-check <file>.pdf` when a PDF is
   produced.
7. Report the output path and any ATS warnings or build errors that matter.

## Content Rules

- Treat resume data as private local content.
- Use concise, achievement-focused bullets with truthful scope.
- Prefer measurable outcomes only when the user supplied the numbers.
- Use `__text__` for inline bold emphasis in narrative fields.
- Keep section names and fields compatible with the CVForge schema.
- If a user wants a new section type, explain that CVForge template/code changes
  are required before adding arbitrary YAML.

## Reference

Read [references/cvforge-reference.md](references/cvforge-reference.md) when
you need command examples, YAML field details, section examples, fonts, ATS
guidance, or build troubleshooting.
