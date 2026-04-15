# Guide: Markdown to PDF with Pandoc and LuaLaTeX

## Installation

### 1. Install Pandoc

```bash
brew install pandoc
```

### 2. Install LuaLaTeX via BasicTeX

BasicTeX is a minimal TeX distribution (~100MB) that includes lualatex:

```bash
brew install --cask basictex
```

After installation, reopen your terminal so that `tlmgr` and `lualatex` are available in your PATH.

### 3. Install missing LaTeX packages

BasicTeX does not include all packages. If pandoc reports a missing `.sty` file, install the package via `tlmgr`:

```bash
sudo tlmgr update --self
sudo tlmgr install lualatex-math
```

---

## Converting Markdown to PDF

### Working command

```bash
pandoc "$HOME/Documents/invoices/2026/INV-2026-001.md" \
  -o "$HOME/Documents/invoices/2026/INV-2026-001.pdf" \
  --pdf-engine=lualatex \
  -V mainfont="Arial Unicode MS"
```

### Why these options?

| Option | Reason |
|---|---|
| `--pdf-engine=lualatex` | The default pdflatex engine does not support Unicode characters like ✓ |
| `-V mainfont="Arial Unicode MS"` | The default LaTeX font is missing characters like ✓; Arial Unicode MS has full Unicode coverage |

---

## Common errors

### `Unicode character ✓ not set up for use with LaTeX`
Use `--pdf-engine=lualatex` instead of the default engine.

### `File lualatex-math.sty not found`
Install the missing package:
```bash
sudo tlmgr install lualatex-math
```

### `The font "X" cannot be found`
Check which fonts are available on your system:
```bash
fc-list | grep -v '^\s*\.' | awk -F: '{print $2}' | sort -u
```
`Arial Unicode MS` is available by default on macOS and supports all Unicode characters.

### Path with spaces not working
Use `$HOME` instead of `~` and wrap the path in double quotes:
```bash
# Wrong
pandoc ~/Documents/My\ Folder/file.md ...

# Correct
pandoc "$HOME/Documents/My Folder/file.md" ...
```

---

## General template

```bash
pandoc "$HOME/path/to/file.md" \
  -o "$HOME/path/to/file.pdf" \
  --pdf-engine=lualatex \
  -V mainfont="Arial Unicode MS"
```
