# CVForge Skill

A portable coding-agent skill for creating, editing, building, and validating CVForge resumes. It helps agents work with `cv.yaml` files, generate ATS-friendly PDFs with the `cvforge` CLI, troubleshoot Typst/YAML errors, and run ATS checks.

Compatible with coding agents that support Agent Skills or skill-style folders, including Codex, Claude Code, Pi Coding Agent, Gemini CLI, OpenCode, and similar tools.

## What This Skill Does

- Guides agents through CVForge resume YAML creation and edits.
- Keeps resume content factual and avoids invented employers, dates, credentials, or metrics.
- Documents CVForge commands, fields, fonts, photo options, and ATS validation.
- Teaches agents to build PDFs with `cvforge` and verify them with `cvforge ats-check`.
- Keeps detailed reference material in `references/cvforge-reference.md` so the main `SKILL.md` stays short.

## Installation

Clone this repo directly into the skill directory used by your coding agent.
Use `cvforge` as the target folder name so it matches the skill name in
`SKILL.md`.

### Codex

Project skill:

```bash
mkdir -p .agents/skills
git clone https://github.com/SoAp9035/cvforge-skill.git .agents/skills/cvforge
```

### Pi Coding Agent

Project skill:

```bash
mkdir -p .agents/skills
git clone https://github.com/SoAp9035/cvforge-skill.git .agents/skills/cvforge
```

### Claude Code

Project skill:

```bash
mkdir -p .claude/skills
git clone https://github.com/SoAp9035/cvforge-skill.git .claude/skills/cvforge
```

### Gemini CLI

Shared Agent Skills layout:

```bash
mkdir -p .agents/skills
git clone https://github.com/SoAp9035/cvforge-skill.git .agents/skills/cvforge
```

Native Gemini CLI layout:

```bash
mkdir -p .gemini/skills
git clone https://github.com/SoAp9035/cvforge-skill.git .gemini/skills/cvforge
```

### OpenCode

Native OpenCode layout:

```bash
mkdir -p .opencode/skills
git clone https://github.com/SoAp9035/cvforge-skill.git .opencode/skills/cvforge
```

Claude-compatible layout:

```bash
mkdir -p .claude/skills
git clone https://github.com/SoAp9035/cvforge-skill.git .claude/skills/cvforge
```

### GitHub Copilot and VS Code Agent Mode

Project skill:

```bash
mkdir -p .github/skills
git clone https://github.com/SoAp9035/cvforge-skill.git .github/skills/cvforge
```

## Setup

Install CVForge in the environment where your agent runs commands:

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

Ask your coding agent to work with CVForge resumes, for example:

```text
Create a CVForge cv.yaml for my resume and generate an ATS-friendly PDF.
```

```text
Review this cv.yaml for ATS quality, improve the bullets without inventing facts, build the PDF, and run cvforge ats-check.
```

```text
Fix the CVForge build error and explain what was wrong in the YAML.
```

The skill will tell the agent to inspect the YAML, preserve factual content, build with CVForge, and validate the output PDF.

## File Structure

```text
cvforge-skill/
  SKILL.md                          # Agent trigger metadata and workflow
  references/
    cvforge-reference.md            # Commands, schema, fonts, ATS guidance, troubleshooting
  README.md                         # Installation and usage instructions
  .gitignore                        # Local generated files to ignore
```

## CVForge

CVForge is a CLI for building clean, ATS-friendly PDF resumes from YAML with Typst.

- Package: https://pypi.org/project/cvforge/
- Repository: https://github.com/SoAp9035/cvforge
