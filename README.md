# DIY Admin - Freelancer Billing & Quotes Tools

A simple, self-hosted toolkit for freelancers to manage billing and generate professional quotes. Convert Markdown invoices and quotes to PDFs using Pandoc and LuaLaTeX.

## Features

- **Invoice Generation**: Create invoices in Markdown, convert to PDF
- **Quote/Proposal Management**: Generate professional quotes for clients
- **Unicode Support**: Full Unicode character support (checkboxes, symbols, etc.)
- **Minimal Dependencies**: Lightweight setup with Pandoc and BasicTeX

## Quick Start

### 1. Install Dependencies

```bash
# Install Pandoc
brew install pandoc

# Install BasicTeX (minimal LaTeX distribution)
brew install --cask basictex
```

Reopen your terminal after BasicTeX installation to update PATH.

### 2. Install Required LaTeX Packages

```bash
sudo tlmgr update --self
sudo tlmgr install lualatex-math
```

## Usage

### Create an Invoice

1. Create a Markdown file for your invoice (e.g., `invoices/2026/IMZ-2026-0002.md`)
2. Use the conversion command:

```bash
pandoc "$HOME/path/to/invoice.md" \
  -o "$HOME/path/to/invoice.pdf" \
  --pdf-engine=lualatex \
  -V mainfont="Arial Unicode MS"
```

### Create a Quote

Same process as invoices - create a Markdown file with your quote details and convert to PDF.

## Project Structure

```
diy-admin/
├── examples/
│   └── invoice-example.md
├── invoices/
│   └── 2026/
│       └── INV-2026-001.md
├── quotes/
│   └── 2026/
│       └── QT-2026-0001.md
├── templates/
│   └── invoice-template.md
└── README.md
```

See `examples/invoice-example.md` for a complete example you can use as a template.

## Markdown Template Example

```markdown
# Invoice IMZ-2026-0002

**From:** Your Name  
**To:** Client Name  
**Date:** 2026-04-15  
**Due:** 2026-05-15

---

## Services

| Description | Hours | Rate | Amount |
|-------------|-------|------|--------|
| Web Development | 10 | $75 | $750 |
| Consulting | 2 | $75 | $150 |

---

**Subtotal:** $900  
**Tax:** $0  
**Total:** $900

---

**Payment Terms:** Net 30  
**Payment Methods:** Bank Transfer

✓ Thank you for your business!
```

## Tips

- Use `$HOME` instead of `~` in paths to avoid issues with spaces
- Always wrap paths with spaces in double quotes
- `Arial Unicode MS` font supports all Unicode characters (including ✓)
- LuaLaTeX engine is required for proper Unicode rendering

## Troubleshooting

### Unicode Character Not Found
```
Error: Unicode character ✓ not set up for use with LaTeX
```
**Fix:** Use `--pdf-engine=lualatex` instead of the default pdflatex.

### Missing LaTeX Package
```
Error: File lualatex-math.sty not found
```
**Fix:** Install the missing package: `sudo tlmgr install lualatex-math`

### Font Not Available
List available fonts on macOS:
```bash
fc-list | grep -v '^\s*\.' | awk -F: '{print $2}' | sort -u
```

## Resources

- [Pandoc Documentation](https://pandoc.org/documentation.html)
- [BasicTeX Overview](https://www.tug.org/mactex/morepackages.html)

## License

MIT License - Feel free to use and modify for your own freelance business.
