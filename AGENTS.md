# AI Agent Development Guide

## Project Overview

**checkstyle-config** — Shared Checkstyle configuration for all iQKV Foundation Java projects. Published to Maven Central as `com.iqkv:checkstyle-config` and consumed by every service via `maven-checkstyle-plugin`.

**Key characteristics:**

- No Java source — configuration XML and suppressions only
- Changes here affect every downstream Java project (`foundation-iam-service`, `foundation-cms-service`, etc.)
- Published to Maven Central via the `maven-central` Maven profile
- Node.js tooling (pnpm + Husky) for commit hooks and formatting only

## Project Structure

```
src/main/
├── idea/
│   └── IDEA-Checkstyle-Defaults.xml        # IDE import config for IntelliJ
└── resources/
    ├── maven-project-common-checkstyle.xml  # Main ruleset — consumed by all services
    ├── checkstyle-suppressions.xml          # Global suppressions (SuppressionFilter)
    ├── checkstyle-xpath-suppressions.xml    # XPath-based suppressions
    └── README-Checkstyle.md                 # Rule reference documentation
```

## Design Rules

### What belongs here

- Checkstyle rule modules and their properties (`maven-project-common-checkstyle.xml`)
- Suppression patterns that apply across all projects (`checkstyle-suppressions.xml`)
- IDE integration config (`IDEA-Checkstyle-Defaults.xml`)

### What does NOT belong here

- Project-specific suppressions — those go in the consuming project's own `checkstyle-suppressions.xml`
- Java source code
- Spring or Maven plugin configuration

### Rule change impact

A rule addition or tightening is a **breaking change** for all consuming services. Before tightening any rule:

1. Check that the change compiles cleanly on at least one service (`./mvnw validate -Dcheckstyle.skip=false`)
2. List affected services in the PR description
3. Coordinate the version bump in `boot-parent-pom` (`iqkv.checkstyle.version`)

A suppression addition is safe — it only relaxes enforcement.

## Execution Discipline

- Read the existing rule file and suppressions before editing.
- A tightened rule fails every downstream service — verify impact before proposing.
- After two identical failures without new evidence, change approach — do not retry blindly.
- No speculative rule additions — add only what is directly requested and justified.

## Security

- No credentials, tokens, or internal paths in configuration files or suppressions.
- Never bypass `--no-verify` unless explicitly requested.

## AI Agent Guidelines

- **Ask before applying**: show the proposed XML diff and list which rules change.
- **Approval phrases**: "Yes", "Proceed", "Apply", "Do it", "Looks good"
- **Never create** summary or review markdown files automatically.
- Rule tightenings need downstream verification proof in the PR.

## Commit Standards

Format: `type(scope): subject`

- Subject: imperative, lowercase, no trailing period, ≤ 72 chars
- Types: `feat`, `fix`, `improvement`, `refactor`, `docs`, `chore`, `ci`, `revert`
- Scope: affected file or rule area (e.g., `checkstyle`, `suppressions`, `xpath`, `line-length`, `imports`, `deps`)
- For `fix`: symptom + trigger, not the XML change
  - ✅ `fix(suppressions): generated mapper files fail VisibilityModifier check`
  - ❌ `fix(suppressions): add suppression for generated files`

Examples:

- `feat(checkstyle): add MissingJavadocMethod rule for public methods`
- `fix(suppressions): Lombok-generated constructors trigger FinalClass violation`
- `improvement(line-length): raise limit from 190 to 220 for generated code patterns`
- `chore(deps): update checkstyle to 14.3.0`

## Development Commands

```bash
# Validate POM and package the config jar
./mvnw verify

# Skip Checkstyle self-check (this repo does not apply Checkstyle to itself)
./mvnw verify -Dcheckstyle.skip=true
```
