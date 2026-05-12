# CVForge Skill

A portable Agent Skill for creating, editing, building, and validating
CVForge resumes.

It helps coding agents work with `cv.yaml`, generate ATS-friendly PDFs with
the `cvforge` CLI, troubleshoot YAML or Typst errors, and run ATS checks.

## Features

- Create and edit CVForge resume YAML.
- Preserve factual resume content without inventing employers, dates, metrics,
  credentials, or tools.
- Build PDFs with `cvforge`.
- Validate output with `cvforge ats-check`.
- Use `references/cvforge-reference.md` for detailed CVForge commands, schema,
  fonts, photo options, ATS guidance, and troubleshooting.

## Installation

### Agents supporting `.agents/skills`

Use this shared project layout for Codex, Pi Coding Agent, Gemini CLI,
OpenCode, GitHub Copilot, and VS Code Agent Mode:

```bash
mkdir -p .agents/skills
git clone https://github.com/SoAp9035/cvforge-skill.git .agents/skills/cvforge-skill
```

### Claude Code

```bash
mkdir -p .claude/skills
git clone https://github.com/SoAp9035/cvforge-skill.git .claude/skills/cvforge-skill
```

## Setup

Install CVForge where your agent runs commands:

```bash
uv tool install cvforge
```

Alternative:

```bash
pip install cvforge
```

You can also run CVForge without installing it as a tool:

```bash
uvx cvforge --version
```

## Usage

Ask your agent to work with CVForge resumes:

```text
Create a CVForge resume and build the PDF.
```

```text
Review this cv.yaml for ATS quality and run ats-check.
```

```text
Fix this CVForge build error.
```

## CVForge

CVForge builds clean, ATS-friendly PDF resumes from YAML with Typst.

- Package: https://pypi.org/project/cvforge/
- Repository: https://github.com/SoAp9035/cvforge
