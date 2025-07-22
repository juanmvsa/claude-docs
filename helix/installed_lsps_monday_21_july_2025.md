
---

# Language Server Installation Log

This document lists the commands used to install language servers for Haskell and JSON in the Helix editor configuration.

## Haskell Language Server (HLS)

### Installation Command
```bash
brew install haskell-language-server
```

### Why This Approach
- **Homebrew**: Used Homebrew instead of other methods because it handles dependencies automatically
- **haskell-language-server**: This is the official LSP for Haskell that provides:
  - Type checking and inference
  - Code completion
  - Go-to-definition
  - Refactoring support
  - Error reporting
- **Version**: Installed version 2.11.0.0_1 with support for GHC versions 9.8.4, 9.10.2, 9.12.2
- **Configuration**: Uses `haskell-language-server-wrapper` command with `--lsp` argument for proper LSP communication

### Configuration Added to languages.toml
```toml
[language-server.haskell-language-server]
command = "haskell-language-server-wrapper"
args = ["--lsp"]

[[language]]
name = "haskell"
language-servers = ["haskell-language-server"]
file-types = ["hs", "lhs"]
auto-format = true
```

## JSON Language Server

### Installation Command
```bash
brew install vscode-langservers-extracted
```

### Why This Approach
- **First Attempt**: Tried `npm install -g vscode-langservers-extracted` but encountered permission issues
- **Permission Error**: Got EACCES error trying to write to `/usr/local/lib/node_modules/`
- **Homebrew Solution**: Switched to Homebrew which handles permissions properly and installs system-wide
- **vscode-langservers-extracted**: This package contains multiple language servers extracted from VS Code:
  - JSON Language Server
  - HTML Language Server  
  - CSS Language Server
  - ESLint Language Server
- **Version**: Installed version 4.10.0 with all dependencies handled automatically

### Configuration Added to languages.toml
```toml
[language-server.vscode-json-language-server]
command = "vscode-json-language-server"
args = ["--stdio"]

[[language]]
name = "json"
language-servers = ["vscode-json-language-server"]
file-types = ["json"]
auto-format = true
```

## Key Benefits

1. **Homebrew Consistency**: Both installations use Homebrew, ensuring consistent dependency management
2. **System Integration**: Properly installed at system level with correct permissions
3. **Auto-formatting**: Both language servers configured with `auto-format = true` for better code quality
4. **Standard LSP Protocol**: Both use standard LSP communication (`--lsp` and `--stdio`)
5. **File Type Coverage**: Covers common file extensions (`.hs`, `.lhs` for Haskell; `.json` for JSON)

## Bash Language Server

### Installation Command
```bash
npm install -g bash-language-server
```

### Why This Approach
- **npm Global Install**: Used npm for global installation as this is the recommended method for bash-language-server
- **Permission Success**: Unlike the earlier JSON LSP attempt, this succeeded because npm permissions were working correctly
- **bash-language-server**: Official LSP for Bash that provides:
  - Syntax checking and validation
  - Code completion for commands and variables
  - Documentation on hover
  - Go-to-definition for functions
  - Error diagnostics
- **No Auto-format**: Set to `false` because bash scripts often have specific formatting requirements

### Configuration Added to languages.toml
```toml
[language-server.bash-language-server]
command = "bash-language-server"
args = ["start"]

[[language]]
name = "bash"
language-servers = ["bash-language-server"]
file-types = ["sh", "bash"]
auto-format = false
```

## Installation Verification

All language servers are now available in the system PATH and will be automatically started by Helix when editing files of the corresponding types.

---

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
