# AGENTS.md

## Project Overview

Olm (`onelinemcp`) compiles a simple text-based tool spec into a working MCP server (Python or TypeScript).

- Spec format: `name:command` with `{placeholder}` parameters and `#!` descriptions
- Single dependency: `jinja2` (for code generation templates)
- Entry point: `olm` CLI → `olm:main`

## Setup

```bash
pip install -e .
```

## Usage

```bash
olm tools.txt -l py > server.py
olm tools.txt -l ts > server.ts
python <(olm tools.txt)
```

## Code Structure

- `olm/__init__.py` — all logic: CLI, spec parser, code generators
- `olm.py` — thin wrapper (unused, entry point is `olm:main`)
- `example.olm` — example spec file

## Code Style

- Python 3.10+, no type hints currently
- Single file for all logic (`olm/__init__.py`)
- Jinja2 templates inline as strings
- No tests yet

## Testing

No test suite. Verify changes manually:

```bash
olm example.olm -l py | python
olm example.olm -l ts | npx tsx
```
