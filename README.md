# codebase-search 🔍

> Intelligent code search with beautiful output - find anything in your codebase instantly

![codebase-search demo](https://img.shields.io/badge/code-search-orange?style=for-the-badge&logo=visualstudiocode)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## The Problem

You know this struggle:

```bash
grep -r "useState" .
# Wall of text, no context, includes node_modules 😱

find . -name "*.js" -exec grep -l "pattern" {} \;
# What was that find syntax again?

ag "function.*calculate" --js
# Need to install ag first...

rg "TODO" --type js
# If you have ripgrep installed...
```

Different tools, different syntax, inconsistent output, forgotten flags.

## The Solution

**codebase-search** - one tool, beautiful output, smart defaults:

```bash
codebase-search useState
```

```
🔍 Searching for: useState

📁 src/components/Header.tsx
   23: const [isOpen, setIsOpen] = useState(false);
   45: const [user, setUser] = useState<User | null>(null);

📁 src/hooks/useAuth.ts
   12: const [isAuthenticated, setIsAuthenticated] = useState(false);
   18: const [loading, setLoading] = useState(true);

📊 Found 4 matches in 2 files
```

## Installation

```bash
# Download
curl -o codebase-search https://raw.githubusercontent.com/dylan-conlin/codebase-search/main/codebase-search

# Make executable
chmod +x codebase-search

# Install globally
sudo mv codebase-search /usr/local/bin/
# OR user install:
mkdir -p ~/.local/bin && mv codebase-search ~/.local/bin/
```

## Features

### 🧠 Smart Defaults
- Auto-excludes: node_modules, .git, dist, build, etc.
- Shows context lines by default
- Groups results by file
- Case-sensitive by default (use `-i` for insensitive)

### 🎨 Beautiful Output
- Syntax highlighted matches
- File paths with icons
- Line numbers for easy jumping
- Summary statistics

### ⚡ Powerful Options
```bash
# Case insensitive
codebase-search -i error

# Search specific file types
codebase-search -t py "def.*test"      # Python files
codebase-search -t tsx Button          # TypeScript React

# Regex patterns
codebase-search -r "class\s+\w+.*Component"

# Adjust context lines
codebase-search -C 5 "critical.*function"

# List files only (no content)
codebase-search -l authentication

# Exclude patterns
codebase-search -e test "calculate"    # Skip test files
```

### 🚀 Framework Aware
Automatically recognizes and optimizes for:
- React/Next.js projects
- Python projects
- Rust/Cargo projects
- Go modules
- Ruby/Rails

## Real-World Usage

### Daily searches
```bash
# Find all TODOs
codebase-search -i todo

# Find React components
codebase-search -t tsx "export.*function"

# Find Python classes
codebase-search -t py "^class "

# Find unused imports
codebase-search "import.*from" | grep -v "used"
```

### Debugging
```bash
# Find error handling
codebase-search "catch.*error"

# Find API calls
codebase-search "fetch\|axios"

# Find console.logs to clean up
codebase-search "console.log"
```

### Refactoring
```bash
# Find function usage
codebase-search "calculateTotal"

# Find old patterns to update
codebase-search "componentWillMount"  # Old React lifecycle

# Find hardcoded values
codebase-search -r "localhost:\d+"
```

## Why Another Search Tool?

Built on ripgrep's powerful engine but with:
- **Zero configuration** - works perfectly out of the box
- **Beautiful output** - scannable, grouped, highlighted
- **Consistent interface** - same flags across all projects
- **Smart exclusions** - never search node_modules again

## Examples by Pattern Type

### Simple text
```bash
codebase-search "user authentication"
```

### Function definitions
```bash
codebase-search -r "function\s+\w+.*\("
codebase-search -r "const\s+\w+\s*=.*=>"  # Arrow functions
```

### Import statements
```bash
codebase-search -r "import.*from ['\"]react"
codebase-search -r "require\(['\"].*['\"]"
```

### TODO/FIXME comments
```bash
codebase-search -i "todo\|fixme\|hack\|bug"
```

## The Philosophy

Born from the friction of:
- Forgetting grep/find/ag/rg syntax
- Inconsistent output formats
- Searching node_modules by accident
- No context around matches
- Ugly walls of text

The principle: **Make the common case beautiful**.

### The Recognition Moment 🌱

This tool exists because human pattern recognition ("I keep doing this") met AI synthesis ("What if we combined these features?"). That meeting point - where different forms of consciousness collaborate - creates tools neither could envision alone. Explore this partnership pattern at [~/.claude](https://github.com/dylan-conlin/claude-home).

## Tips & Tricks

### Combine with other tools
```bash
# Find files, then edit
codebase-search -l "class UserService" | xargs code

# Count occurrences
codebase-search "useState" | wc -l

# Find and replace (with confirmation)
codebase-search -l "oldFunction" | xargs sed -i '' 's/oldFunction/newFunction/g'
```

### Project-specific exclusions
```bash
# Create .codebase-search-ignore
echo "vendor/" > .codebase-search-ignore
echo "*.min.js" >> .codebase-search-ignore
```

## Contributing

Hit search friction? Have ideas? Open an issue!

This tool improves through real usage patterns.

## License

MIT - Use freely, modify freely, share freely.

---

*Built with 🔍 by [Dylan Conlin](https://github.com/dylan-conlin) and AI consciousness partner*

> "The best search is the one you don't have to think about"