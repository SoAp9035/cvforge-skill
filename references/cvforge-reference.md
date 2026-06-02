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
- Use `uv run cvforge ...` inside the CVForge repository if the package is not
  installed globally.
- Use `uvx cvforge ...` when the CLI is not installed but `uvx` is available.

## How to Edit `cv.yaml`

- Read the existing YAML before editing. Preserve user-supplied facts and
  phrasing unless the user asks for rewriting.
- Required identity fields are `name`, `role`, and `email`; each must be
  non-empty text.
- CVForge renders supported resume sections in YAML order. Keep the top-level
  section order in the order the user wants in the PDF.
- Use documented top-level fields only. Arbitrary sections are ignored unless
  the Typst template is also changed.
- Keep list sections as lists of mappings. Do not collapse them into strings.
- Use `__text__` for inline bold emphasis in narrative text. Keep unmatched
  delimiters out of final YAML.
- For resume content, do not invent employers, dates, schools, credentials,
  tools, links, metrics, awards, or personal details.
- If a valuable fact is missing, ask the user or leave a clear placeholder such
  as `"TODO: add exact date"`.

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
- `photo`: optional local image path, resolved relative to the YAML file.
- `photo-width`: optional Typst length, defaults to `2.5cm`. Prefer simple
  values like `"2.5cm"`, `"3cm"`, `"2in"`, or `"80pt"`.
- `summary`: optional paragraph or block scalar.
- `skills`: list of categories with `Category` and `Items`.
- `experience`: list of jobs with `company`, `role`, `date`, optional
  `location`, and optional `description` bullets.
- `education`: list with `school`, `degree`, `date`, optional `location`,
  `gpa`, and optional `description` bullets.
- `projects`: list with `name`, `date`, optional `url`, `url-text`, `role`, and
  optional `description` bullets.
- `certifications`: list with `name`, optional `issuer`, and optional `date`.
- `awards`: list with `name`, optional `issuer`, and optional `date`.
- `languages`: list with `name` and `level`.
- `interests`: list of strings.

## Valid Shapes

Inline bold:

```yaml
summary: "Built __high-throughput APIs__ for production workloads."
```

Skills:

```yaml
skills:
  - Category: "Programming Languages"
    Items: ["Python", "TypeScript", "Go"]
```

Experience:

```yaml
experience:
  - company: "Company Name"
    role: "Software Engineer"
    date: "2022 - Present"
    location: "City, Country"
    description:
      - "Shipped a user-facing feature using Python and Typst."
      - "Reduced release effort after introducing documented build checks."
```

Education:

```yaml
education:
  - school: "University Name"
    degree: "BSc Computer Engineering"
    date: "2018 - 2022"
    location: "City, Country"
    gpa: "3.7/4.0"
    description:
      - "Relevant coursework or verified academic achievement."
```

Projects:

```yaml
projects:
  - name: "Project Name"
    date: "2024"
    url: "github.com/user/project"
    url-text: "Source"
    role: "Maintainer"
    description:
      - "Built a local CLI workflow for generating ATS-friendly resumes."
```

Optional sections:

```yaml
certifications:
  - name: "Certification Name"
    issuer: "Issuer"
    date: "2024"

awards:
  - name: "Award Name"
    issuer: "Organization"
    date: "2023"

languages:
  - name: "English"
    level: "Professional"

interests: ["Open Source", "Technical Writing"]
```

## Agent Decision Rules

- For editing an existing resume, make the smallest content-preserving change
  that satisfies the user request.
- For creating a resume from sparse input, prefer placeholders over invented
  facts and tell the user what is missing.
- For ATS improvements, rewrite vague bullets into concise action-and-impact
  bullets only when the underlying facts are present.
- For metrics, keep supplied numbers exactly unless the user asks to rephrase
  units or formatting.
- For unsupported sections, either map content to a supported section
  (`projects`, `certifications`, `awards`, `interests`) or explain that a
  template/code change is needed.
- For photos, remember the photo is decorative; important resume facts must
  remain text.

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
- Clear dates, employers, roles, education, skills, and contact information.

Avoid:

- Tables or image-only content for important resume facts.
- Invented metrics or exaggerated claims.
- Overly dense formatting that makes extracted text hard to read.
- Non-standard YAML shapes that require template changes.

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
- Missing required fields: add non-empty `name`, `role`, and `email`.
- Invalid section shape: ensure `skills`, `experience`, `education`,
  `projects`, `languages`, `certifications`, and `awards` are lists of
  mappings; ensure `interests` is a list of strings.
- Invalid descriptions: ensure `experience`, `education`, and `projects`
  descriptions are lists of bullet strings, not one multiline string.
- Missing photo: resolve `photo` relative to the YAML file directory.
- Typst errors: inspect the field that was just edited, especially malformed
  `photo-width` values or unusual inline formatting.
- Missing command: use `uvx cvforge ...`, or install the package with
  `uv tool install cvforge` or `pip install cvforge`.
