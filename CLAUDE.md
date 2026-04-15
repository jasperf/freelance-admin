# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

A self-hosted toolkit for generating professional invoices and quotes as PDFs. Markdown files are converted to PDF via Pandoc + LuaLaTeX. There is no application code, no package manager, and no test suite.

## Dependencies

```bash
brew install pandoc
brew install --cask basictex
# Reopen terminal after basictex installation
sudo tlmgr update --self
sudo tlmgr install lualatex-math
```

## Converting Markdown to PDF

```bash
pandoc "$HOME/path/to/invoice.md" \
  -o "$HOME/path/to/invoice.pdf" \
  --pdf-engine=lualatex \
  -V mainfont="Arial Unicode MS"
```

## Directory Layout

```
invoices/YYYY/IMZ-YYYY-NNNN.md
quotes/YYYY/QT-YYYY-NNNN.md
templates/
examples/invoice-example.md
```

## Key Constraints

- Always use `--pdf-engine=lualatex` — the default pdflatex does not support Unicode characters (e.g., `✓`).
- Use `$HOME` instead of `~` in paths; wrap paths containing spaces in double quotes.
- Font `Arial Unicode MS` is required for full Unicode coverage and is available by default on macOS.

## Troubleshooting

| Error | Fix |
|-------|-----|
| `Unicode character ✓ not set up for use with LaTeX` | Add `--pdf-engine=lualatex` |
| `File lualatex-math.sty not found` | `sudo tlmgr install lualatex-math` |
| Font not found | `fc-list \| grep -v '^\s*\.' \| awk -F: '{print $2}' \| sort -u` |
