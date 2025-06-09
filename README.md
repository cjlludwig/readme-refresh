# readme-refresh

CLI tool to refresh README automatically with up to date information based on code contents, documents, and external sources like Confluence. Can be used as part of CI processes to ensure up to date docs in large organizations.

## Description

The readme-refresh tool automates the process of keeping README files current by:

1. **Analyzing your codebase** - Uses gitingest to extract project structure and code context
2. **Processing with AI** - Leverages OpenAI's API to understand and improve documentation
3. **Integrating external sources** - Can pull in context from Confluence and other documentation sources
4. **Maintaining consistency** - Applies standardized formatting and structure

## Getting Started

### Dependencies

**Required System Tools:**
```shell
# Context gathering tool
pip install gitingest

# Markdown formatting (choose one method)
npm install -g markdownlint-cli    # Recommended: npm global install
# OR
brew install markdownlint-cli      # Alternative: Homebrew (macOS/Linux)
```

**For pyenv users:**
```shell
# Install in current pyenv environment
python -m pip install gitingest
pyenv rehash

# Ensure pyenv shims take precedence (add to ~/.zshrc)
export PATH="$HOME/.pyenv/shims:$PATH"
```

**Environment Variables:**
- `OPENAI_API_KEY` - Your OpenAI API key for processing README content

**Optional Setup:**
- Confluence MCP integration for external documentation sources

**Troubleshooting Dependencies:**
- Run `npm run check` to verify all tools are installed correctly
- For markdownlint issues, try the npm version: `npm install -g markdownlint-cli`

### Installation

```shell
# Install project dependencies
npm install

# Check if all required tools are available
npm run dev -- --check
```

## Usage

### Basic Usage

```shell
# Run the complete README refresh workflow
npm run dev
```

### Advanced Options

```shell
# Run with interactive mode (pause between steps)
npm run dev -- --interactive

# Show detailed command output
npm run dev -- --verbose

# Continue processing even if some steps fail
npm run dev -- --continue

# Keep gitingest context files after completion
npm run dev -- --keep-context

# Check dependencies only
npm run dev -- --check

# Show help
npm run dev -- --help
```

### Workflow Steps

The tool executes the following automated workflow:

1. **Dependency Check** - Verifies all required tools are installed
2. **Context Generation** - Runs gitingest to analyze your codebase
3. **AI Processing** - Processes README through 3 AI prompts:
   - Step 1: Standardizes and cleans existing README structure
   - Step 2: Integrates external documentation sources
   - Step 3: Updates content based on current codebase analysis
4. **Formatting** - Applies consistent markdown formatting
5. **Cleanup** - Removes temporary files (unless `--keep-context` is used)

### Manual Workflow (Alternative)

If you prefer manual control, you can run the individual steps:

```shell
# 1. Generate context files
gitingest -s 50000 -i src/,README.md,package.json -e "*.snap,*generated*" -o gitingest-output.txt
gitingest -s 50000 -i tf/,k8s-tf/,deployment_manifest.yaml,package.json -e ".tf*" -o gitingest-output-tf.txt

# 2. Process prompts manually in OpenAI
# - Use prompts/1_prep_readme.txt
# - Use prompts/2_external_sources.txt  
# - Use prompts/3_gitingest.txt

# 3. Format final result
markdownlint -f README.md
```

## Architecture

The tool is built using:

- **Google ZX** - Node.js CLI script framework for shell operations
- **OpenAI SDK** - AI processing of documentation content
- **Gitingest** - Code context extraction and analysis
- **TypeScript** - Type-safe development with modern JavaScript features

### Project Structure

```
readme-refresh/
├── script.ts              # Main CLI application
├── prompts/               # AI prompt templates
│   ├── 1_prep_readme.txt  # README standardization
│   ├── 2_external_sources.txt # External docs integration
│   └── 3_gitingest.txt    # Codebase analysis integration
├── templates/             # Output templates
└── package.json           # Dependencies and scripts
```

## Help

**Common Issues:**

- **Missing dependencies**: Run `npm run dev -- --check` to identify missing tools
- **OpenAI API errors**: Ensure `OPENAI_API_KEY` is set and has sufficient credits
- **Permission errors**: Ensure you have write access to the README.md file
- **Large repositories**: Gitingest has size limits; adjust include/exclude patterns if needed

**Tips:**

- Use `--interactive` mode to review changes at each step
- Use `--verbose` to see detailed command output for debugging
- Backup important README files before running (tool creates automatic backups)
- The tool works best with structured codebases that follow standard conventions

## References

- [Google ZX Documentation](https://google.github.io/zx/)
- [OpenAI API Documentation](https://platform.openai.com/docs)
- [Gitingest Documentation](https://github.com/cyclotruc/gitingest)
- [Markdownlint CLI](https://github.com/igorshubovych/markdownlint-cli)
