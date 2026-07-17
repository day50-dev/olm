<p align="center">
  <img width="300" alt="olm" src="https://github.com/user-attachments/assets/6dc40aea-4719-4e2e-a57b-585e2ef5ec49" />
</p>

**Olm** is a program that takes a simple text file and spits out a full blown MCP server. 

Write your tools as one-liners, get a working Python or TypeScript server on the other end.

The comment above the command becomes the description field for the tool

```text
#! List files in a directory
ls:ls -la {path}

#! Run in a sandbox
sandbox_run:docker exec -it {container} "{command}"

#! Run a custom bash command
bash: /usr/bin/env bash -c "{command}"
```

## Features

- Declarative tool definitions: `name:command` pairs
- Parameters extracted automatically from `{placeholders}`
- Generates Python (`FastMCP`) or TypeScript (`@modelcontextprotocol/sdk`)
- Inline or standalone descriptions via the `#!` prefix

## Quick Start

```bash
python <(olm example.olm)
```


### 2. Compile

Python:
```bash
olm tools.txt -l py > tools.py
```

TypeScript:
```bash
olm tools.txt -l ts > tools.ts
```

## Command Line Arguments

| Argument    | Short | Required | Description                         |
|-------------|-------|----------|-------------------------------------|
| `spec`      |       | Yes      | Path to the spec file               |
| `--lang`    | `-l`  | No       | `py` or `ts` (default: py)          |
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
