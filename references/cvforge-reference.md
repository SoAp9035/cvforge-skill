# CVForge Reference

CVForge builds ATS-friendly PDF resumes from YAML using Typst.

## Commands

```bash
cvforge init
cvforge init <directory>
cvforge <file>.yaml
cvforge build <file>.yaml
cvforge fonts
cvforge ats-check <file>.pdf
```

Notes:

- Passing a `.yaml` or `.yml` path directly is equivalent to `cvforge build`.
- Builds write the PDF next to the YAML with the same base name.
- `cvforge init` writes `cv.yaml` and refuses to overwrite an existing file.
- Use `uv run cvforge ...` inside the repository if the package is not
  installed globally.

## YAML Schema

Common top-level fields:

- `language`: optional, `en` or `tr`; controls section headings only.
- `font`: optional; run `cvforge fonts` for supported keys.
- `name`: required full name.
- `role`: required professional role.
- `email`: required email address.
- `phone`, `location`, `website`, `linkedin`, `github`: optional contact
  fields.
- `website-text`, `linkedin-text`, `github-text`: optional display text for
  links.
- `photo`: optional local image path.
- `photo-width`: optional Typst length, defaults to `2.5cm`.
- `summary`: optional paragraph or block scalar.
- `skills`: list of categories with `Category` and `Items`.
- `experience`: list of jobs with `company`, `role`, `date`, optional
  `location`, and `description` bullets.
- `education`: list with `school`, `degree`, `date`, optional `location`,
  `gpa`, and optional `description` bullets.
- `projects`: list with `name`, `date`, optional `url`, `url-text`, `role`, and
  `description` bullets.
- `certifications`, `awards`, `languages`, `interests`: optional sections.

Inline bold:

```yaml
summary: "Built __high-throughput APIs__ for production workloads."
```

Skills shape:

```yaml
skills:
  - Category: "Programming Languages"
    Items: ["Python", "TypeScript", "Go"]
```

Experience shape:

```yaml
experience:
  - company: "Company Name"
    role: "Software Engineer"
    date: "2022 - Present"
    location: "City, Country"
    description:
      - "Shipped a user-facing feature using Python and Typst."
```

## Fonts

Use `cvforge fonts` before selecting a font. Supported keys currently include:

`noto`, `roboto`, `liberation`, `dejavu`, `inter`, `lato`, `montserrat`,
`raleway`, `ubuntu`, `opensans`, `sourcesans`, `arial`, `times`, `calibri`,
`georgia`, `garamond`, and `trebuchet`.

If an unknown font is configured, CVForge warns and falls back to `noto`.

## ATS Guidance

Prefer:

- Plain text content, standard sections, and conventional headings.
- One or two pages when possible.
- Standard contact links and parseable bullet lists.
- Conservative fonts from `cvforge fonts`.

Avoid:

- Tables or image-only content for important resume facts.
- Invented metrics or exaggerated claims.
- Overly dense formatting that makes extracted text hard to read.

After building, run:

```bash
cvforge ats-check <file>.pdf
```

Treat `Excellent` and `Good` as passing results. Review `Fair`, `Needs
Improvement`, or `Not a CV` with the user.

## Troubleshooting

- Missing input: confirm the YAML path exists and has a `.yaml` or `.yml`
  suffix.
- YAML syntax errors: fix indentation, quotes, list markers, and mappings.
- Missing photo: resolve `photo` relative to the YAML file directory.
- Typst errors: inspect the field that was just edited, especially malformed
  Typst lengths like `photo-width`.
- Missing command: use `uvx cvforge ...`, or install the
  package with `uv tool install cvforge` or `pip install cvforge`.
