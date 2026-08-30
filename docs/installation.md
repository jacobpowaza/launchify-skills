# Installation

## Claude Code

### Via Plugin (Recommended)

```bash
/plugin install launchify@launchify-skills
```

Or manually:

```bash
# Clone the repo
git clone git@github.com:jacobpowaza/launchify-skills.git

# Copy into your project
cp -r launchify-skills/.claude-plugin /path/to/your/project/
cp -r launchify-skills/.claude /path/to/your/project/
cp -r launchify-skills/.launchify /path/to/your/project/
```

### Verify

After installation, run:

```
/launchify-verify
```

If the build passes and reports generate, the skill is installed correctly.

---

## OpenCode

### Via Plugin

```bash
opencode2 plugin add launchify-skills
```

Or add to your `opencode.json`:

```json
{
  "plugins": ["launchify-skills"]
}
```

### Manual

```bash
# Clone the repo
git clone git@github.com:jacobpowaza/launchify-skills.git

# Copy into your project
cp -r launchify-skills/.opencode /path/to/your/project/
cp -r launchify-skills/.launchify /path/to/your/project/
```

### Verify

Run `/launchify-verify` in OpenCode. Reports should generate in `docs/launchify/`.

---

## Codex

### Via Marketplace

```bash
codex plugin marketplace add launchify-skills
codex plugin add launchify
```

### Manual

```bash
# Clone the repo
git clone git@github.com:jacobpowaza/launchify-skills.git

# Copy into your project
cp launchify-skills/AGENTS.md /path/to/your/project/
cp -r launchify-skills/.launchify /path/to/your/project/
cp -r launchify-skills/.codex-plugin /path/to/your/project/
cp -r launchify-skills/.agents /path/to/your/project/
```

### Verify

Run `/launchify-verify` in Codex. Reports should generate in `docs/launchify/`.

---

## Requirements

Launchify does not require any additional packages or runtimes. It operates entirely through your AI coding agent's built-in tools:

- File reading and writing
- Shell command execution
- Search and grep
- Git operations (read-only by default)

### Optional but recommended

- `gitleaks` — for secrets scanning during `/launchify-security-secrets`
- Build toolchain (npm, cargo, go, etc.) — for `/launchify-verify` to run actual builds
- Test framework — for `/launchify-verify` to run tests
- Docker — for container security checks in `/launchify-security-infrastructure`

---

## First Run

After installation, start with a full security audit:

```
/launchify-security-audit
```

This runs all 24 categories in audit-only mode. No code is changed. You get a complete picture of your security posture.

Then, when ready:

```
/launchify-security
```

This runs the full audit and fixes what it can safely fix.
