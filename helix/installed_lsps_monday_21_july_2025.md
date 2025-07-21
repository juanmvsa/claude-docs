# Installed Language Servers for Helix

This document lists all the Language Server Protocol (LSP) servers that have been installed and configured for use with Helix editor.

## 1. texlab (LaTeX)

**Version:** 5.23.1  
**Installation Method:** Homebrew  
**Command Used:**
```bash
brew install texlab
```

**Features:**
- Build on save and open
- Automatic linting with chktex
- LaTeX completion, diagnostics, and formatting
- Supports `.tex` files

**Configuration:** Already configured in `languages.toml`

---

## 2. Julia Language Server

**Version:** Julia 1.11.6 + LanguageServer.jl v4.5.1  
**Installation Method:** Homebrew + Julia Package Manager  
**Commands Used:**
```bash
# Install Julia
brew install julia

# Install LanguageServer.jl package
julia -e 'using Pkg; Pkg.add("LanguageServer")'
```

**Features:**
- Code completion
- Syntax highlighting
- Error diagnostics
- Go to definition
- Symbol search
- Code formatting
- Supports `.jl` files

**Configuration:** Already configured in `languages.toml`

---

## 3. yaml-language-server

**Version:** Latest from npm  
**Installation Method:** npm (Node Package Manager)  
**Command Used:**
```bash
npm install -g yaml-language-server
```

**Features:**
- Schema validation
- Auto-completion
- Error diagnostics
- Formatting
- Hover information
- Supports `.yaml` and `.yml` files

**Configuration:** Already configured in `languages.toml`

---

## 4. marksman (Markdown)

**Version:** 1.0.0-2024-12-18  
**Installation Method:** Homebrew  
**Command Used:**
```bash
brew install marksman
```

**Features:**
- Markdown completion and diagnostics
- Link validation
- Document outline
- Cross-references
- Supports `.md` files

**Configuration:** Already configured in `languages.toml` (mentioned in comments)

---

## 5. jq-lsp (jq Query Language)

**Version:** 0.1.13  
**Installation Method:** Homebrew  
**Command Used:**
```bash
brew install jq-lsp
```

**Features:**
- jq syntax highlighting and validation
- Completion for jq functions
- Error diagnostics
- Supports `.jq` files

**Configuration:** Needs to be added to `languages.toml`:
```toml
[language-server.jq-lsp]
command = "jq-lsp"

[[language]]
name = "jq"
scope = "source.jq"
file-types = ["jq"]
language-servers = ["jq-lsp"]
```

---

## Previously Configured LSPs

The following LSPs were already configured in your `languages.toml` file:

### superhtml-lsp (HTML)
- **Command:** `superhtml lsp`
- **File types:** `.html`

### pylsp + ruff (Python)
- **Commands:** `pylsp`, `ruff server --preview`
- **File types:** `.py`
- **Features:** Type checking, linting, formatting

### tinymist (Typst)
- **Installation:** `cargo install --git https://github.com/Myriad-Dreamin/tinymist --locked tinymist`
- **File types:** `.typ`

### TypeScript Language Server + Tailwind CSS
- **Commands:** `typescript-language-server`, `tailwindcss-ls`
- **File types:** `.jsx`, `.tsx`, `.ts`, `.js`

---

## Verification Commands

To verify all LSPs are working correctly:

```bash
# Check installations
texlab --version
julia -e 'using LanguageServer; println("Julia LSP ready")'
yaml-language-server --help
marksman --version
jq-lsp --version

# Check paths
which texlab
which julia
which yaml-language-server
which marksman
which jq-lsp
```

---

## Notes

- All LSPs will automatically activate when opening files with their respective extensions in Helix
- Configuration details are in `/Users/juan/.config/helix/languages.toml`
- Some LSPs (like Julia's) may take a moment to start up on first use due to compilation
