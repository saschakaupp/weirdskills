# Security Inspector

A basic security scan skill that will work on a given repository.

Currently tailored to Java/Spring Boot, Node.JS/TypeScript and Rust.

## Usage

```
$securityinspector Perform a comprehensive security
audit of this repository.

Include source code, dependencies, authentication,
authorization, secret handling, infrastructure
configuration and CI/CD.

Prioritize exploitable vulnerabilities and provide
exact file references and remediation steps.

Do not modify any files.
```

## Installation

This skill is designed for **OpenAI Codex CLI** and follows the standard Agent Skills directory structure.

### Prerequisites

- OpenAI Codex CLI installed and configured.
- A `SKILL.md` file containing the skill instructions.

### Global Installation (Recommended)

Install the skill globally to make it available across all projects.

```bash
mkdir -p ~/.agents/skills/<skill-name>
cp SKILL.md ~/.agents/skills/<skill-name>/
```

The resulting directory structure should look like this:

```text
~/.agents/
└── skills/
    └── <skill-name>/
        └── SKILL.md
```

### Project-Specific Installation

To make the skill available only within a particular project, install it in the project's `.agents/skills/` directory:

```bash
mkdir -p .agents/skills/<skill-name>
cp SKILL.md .agents/skills/<skill-name>/
```

Directory structure:

```text
project-root/
├── .agents/
│   └── skills/
│       └── <skill-name>/
│           └── SKILL.md
└── ...
```

### Installation from a ZIP Archive

If the skill is distributed as a ZIP archive containing the `<skill-name>/` directory:

```bash
mkdir -p ~/.agents/skills
unzip <skill-name>.zip -d ~/.agents/skills/
```

For project-specific installation:

```bash
mkdir -p .agents/skills
unzip <skill-name>.zip -d .agents/skills/
```

### Usage

Restart Codex CLI after installation to ensure the skill is discovered.

Invoke the skill explicitly:

```text
$<skill-name> Analyze this project.
```

Alternatively, describe the task in natural language and let Codex select the appropriate skill when supported.

### Verification

Check that the skill is installed correctly:

```bash
ls ~/.agents/skills/<skill-name>/SKILL.md
```

For project-specific installations:

```bash
ls .agents/skills/<skill-name>/SKILL.md
```

If Codex does not recognize the skill:

1. Verify the directory structure and the exact filename `SKILL.md`.
2. Ensure that `SKILL.md` contains valid Agent Skills metadata, including the required `name` and `description` fields.
3. Restart Codex CLI.
4. Confirm that the skill is installed in a directory searched by your Codex version.

### Updating

To update an existing installation, replace its `SKILL.md` file with the latest version and restart Codex CLI.

### Uninstallation

For a global installation:

```bash
rm -r ~/.agents/skills/<skill-name>
```

For a project-specific installation:

```bash
rm -r .agents/skills/<skill-name>
```

Only remove the directory belonging to the skill you want to uninstall.
