# Weird skills - a collection for agentic development

Agents can be so preoccupied with how they view the world - stupid little agents!

To improve working with coding agents and make working with local models easier, this is a bunch of skills that can be used with coding agents. I have tested these skills with OpenAI/Codex, Qwen2.5-Coder and Qwen3 from inside OpenCode.

## Agentic Coding

### Context Builder

Read a repository and generate context to allow agents with small context windows to work on complex tasks.

### GDPR Inspector

Analyze a directory regarding privacy and GDPR issues - not just technically! It also analyzes the kind of application and is aware whether personal data are being stored or not.

### Security Inspector

Look at a repository, find problematic code, outdated libraries and unsafe secrets handling.

### ToDoTorial

Was meant to be for humans who want to learn something. Is very effective in planning out tasks for agents, too.

## Creative tasks

### Song generator

I wanted to test various local models regarding their ability for creative tasks. To have more or less comparable results, I based the song writing on specifig sets of quotes. Place your collection of quotes inside an input/ directory as markdown files and name them accordingly. The results are ouput to the directory dist/

- quote-to-song: Takes style request and a source of quotes, then generates lyrics and style prompt for song generation tools.
  - Usage: ```$quote-to-song Slapping 70s funk, danceable, source:lordoftherings```
- quotes-to-album: Similar to the above - just that it will by default generate 5 different lyrics/styles prompts.

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
