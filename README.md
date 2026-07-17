<p align="center">
  <img width="350" alt="olm" src="https://github.com/user-attachments/assets/6dc40aea-4719-4e2e-a57b-585e2ef5ec49" />
</p>

**Olm** is a compiler that takes a text file and spits out an MCP server. Write your tools as one-liners, get a working Python or TypeScript server on the other end.

No boilerplate. No wrappers. Just `name:command` and go.

## Features

- Declarative tool definitions: `name:command` pairs
- Parameters extracted automatically from `{placeholders}`
- Generates Python (`FastMCP`) or TypeScript (`@modelcontextprotocol/sdk`)
- Inline or standalone descriptions via the `#!` prefix

## Installation

```bash
pip install onelinemcp
```

## Usage

### 1. Write a `tools.txt`

```text
#! List files in a directory
ls:ls -la {path}

#! Check system uptime
uptime:uptime

#! Run a custom bash command
bash: /usr/bin/env bash -c "{command}"
```

### 2. Compile

Python:
```bash
olm --mcp tools.txt --lang python > tools.py
```

TypeScript:
```bash
olm --mcp tools.txt --lang typescript > tools.ts
```

## Command Line Arguments

| Argument    | Short | Required | Description                         |
|-------------|-------|----------|-------------------------------------|
| `--mcp`     |       | Yes      | Path to the spec file               |
| `--lang`    |       | Yes      | `python` or `typescript`            |
| `--output`  | `-o`  | No       | Output file (defaults to stdout)    |

## Spec Format

- **Tool**: `name:command`
- **Parameters**: `{like_this}` in the command string becomes a tool input
- **Descriptions**:
  - Inline: `name:command #! Description here`
  - Standalone: `#! Description here` on the line before the tool
- **Comments**: Lines starting with `#` (but not `#!`) are ignored

## Generated Code Requirements

Python: `mcp` (FastMCP)

TypeScript: `@modelcontextprotocol/sdk`, Node.js with `child_process` and `util`
