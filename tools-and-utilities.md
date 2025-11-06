# Tools and Utilities

This guide covers essential tools and utilities that can help you work more efficiently as a developer. These tools are generic and applicable to most projects.

## Essential Git Tools

### Git CLI Commands

The command line is the most powerful way to use Git:

```bash
# Essential commands you'll use daily
git status          # See what's changed
git add .           # Stage changes
git commit -m "msg" # Commit changes
git push            # Push to remote
git pull            # Pull from remote
git log             # View history
git branch          # List branches
git checkout        # Switch branches
```

### Git GUIs

At MetaBotX, we recommend using **GitHub Desktop** for a graphical Git interface.

**GitHub Desktop**
- Simple, user-friendly interface
- Free and open source
- Excellent GitHub integration
- Good for basic and intermediate Git operations
- Cross-platform (Windows, macOS, Linux)
- Built-in merge conflict resolution
- Visual branch management

**Download**: [GitHub Desktop](https://desktop.github.com/)

**VS Code Git Integration**
- Built into VS Code
- Source control panel
- GitLens extension for advanced features
- Good for developers who prefer staying in their editor

### Git Aliases and Shortcuts

Create shortcuts for common Git commands:

```bash
# Add to ~/.gitconfig

[alias]
  st = status
  co = checkout
  br = branch
  ci = commit
  unstage = reset HEAD --
  last = log -1 HEAD
  visual = !gitk
  lg = log --oneline --graph --decorate --all
  
# Usage
git st    # instead of git status
git co    # instead of git checkout
git lg    # pretty log view
```

## Code Quality Tools

### Linters

**ESLint** (JavaScript/TypeScript)
```bash
npm install --save-dev eslint
# Configure via .eslintrc.js
```

**Flake8** (Python)
```bash
pip install flake8
# Configure via .flake8 or setup.cfg
```

**RuboCop** (Ruby)
```bash
gem install rubocop
# Configure via .rubocop.yml
```

### Formatters

**Prettier** (JavaScript/TypeScript/CSS/HTML)
```bash
npm install --save-dev prettier
# Configure via .prettierrc
```

**Black** (Python)
```bash
pip install black
# Format code: black .
```

**autopep8** (Python)
```bash
pip install autopep8
# Format code: autopep8 --in-place --aggressive --aggressive file.py
```

### Pre-commit Hooks

Automatically run checks before commits:

**pre-commit** (Python)
```bash
pip install pre-commit
pre-commit install
# Configure via .pre-commit-config.yaml
```

**Husky** (Node.js)
```bash
npm install --save-dev husky
# Configure via package.json
```

### IDE Integrations

Most IDEs have built-in support for:
- Linting
- Formatting
- Git integration
- Code completion
- Debugging

Configure your IDE to:
- Auto-format on save
- Show linting errors inline
- Run tests from IDE
- Use Git integration

## Development Tools

### Debugging Tools

**Browser DevTools**
- Chrome DevTools
- Firefox Developer Tools
- Safari Web Inspector

**IDE Debuggers**
- VS Code debugger
- IntelliJ debugger
- PyCharm debugger

**Command Line Debuggers**
- `pdb` (Python)
- `debugger` (Node.js)
- `gdb` (C/C++)

### API Testing Tools

**Postman**
- GUI for API testing
- Save requests and collections
- Environment variables
- Free tier available

**Insomnia**
- REST client
- GraphQL support
- Free and open source

**curl / httpie**
- Command-line tools
- Quick API testing
- Scriptable

```bash
# curl example
curl -X GET https://api.example.com/users \
  -H "Authorization: Bearer token"

# httpie example (more readable)
http GET api.example.com/users Authorization:"Bearer token"
```

### Database Management Tools

**pgAdmin** (PostgreSQL)
- GUI for PostgreSQL
- Query editor
- Database management

**DBeaver**
- Universal database tool
- Supports many databases
- Free and open source

**TablePlus**
- Modern database GUI
- Multiple database support
- Paid but has free tier

**Command Line**
```bash
# PostgreSQL
psql -U username -d database_name

# MySQL
mysql -u username -p database_name

# MongoDB
mongo
```

## Collaboration Tools

### Issue Tracking

**GitHub Issues**
- Built into GitHub
- Project boards
- Milestones and labels

**Jira**
- Enterprise issue tracking
- Agile boards
- Advanced reporting

### Communication Platforms

**Slack**
- Team communication
- Channels and threads
- Integrations with Git tools

**Microsoft Teams**
- Team collaboration
- Video calls and chat
- Integration with Office 365

**Discord**
- Community chat
- Voice and video
- Free for teams

### Documentation Tools

**Markdown**
- Simple documentation format
- Used in README files
- GitHub renders it nicely

**Notion**
- Collaborative documentation
- Rich formatting
- Free tier available

**Confluence**
- Enterprise wiki
- Advanced features
- Integration with Jira

**GitBook**
- Documentation platform
- Version control
- Free for public docs

## Useful Browser Extensions

### Git-Related

**GitHub Extensions**
- Enhanced GitHub UI
- Better code review tools
- PR/issue management

**Octotree**
- File tree for GitHub
- Easier navigation
- Better code browsing

### Development

**Web Developer Tools**
- Various browser extensions
- Color pickers
- Responsive design tools

**JSON Formatter**
- Pretty-print JSON
- Syntax highlighting
- Better readability

## Terminal Tools

### Better Terminal

**iTerm2** (macOS)
- Better terminal emulator
- Split panes
- Better customization

**Windows Terminal** (Windows)
- Modern terminal
- Multiple tabs
- Better customization

**Alacritty**
- Fast terminal emulator
- Cross-platform
- GPU-accelerated

### Shell Enhancements

**Oh My Zsh** (Zsh)
```bash
sh -c "$(curl -fsSL https://ohmyz.sh/install.sh)"
# Themes and plugins for better terminal experience
```

**Powerlevel10k**
- Zsh theme
- Fast and customizable
- Git integration

**Starship**
- Cross-shell prompt
- Fast and customizable
- Works with bash, zsh, fish

### Command Line Utilities

**fzf** (Fuzzy Finder)
```bash
# Install
brew install fzf  # macOS
# or
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf

# Use for searching files, commands, history
```

**ripgrep** (Better grep)
```bash
# Install
brew install ripgrep  # macOS
# or
cargo install ripgrep

# Fast search in files
rg "search term"
```

**bat** (Better cat)
```bash
# Install
brew install bat  # macOS
# or
cargo install bat

# Syntax highlighting for files
bat file.js
```

**exa** (Better ls)
```bash
# Install
brew install exa  # macOS
# or
cargo install exa

# Better file listing
exa -la
```

## Productivity Tools

### Time Management

**Pomodoro Technique**
- 25-minute work sessions
- 5-minute breaks
- Various apps available

### Note Taking

**Obsidian**
- Markdown-based notes
- Local files
- Graph view

**Notion**
- All-in-one workspace
- Notes, tasks, databases
- Free tier available

### Password Management

**1Password**
- Secure password storage
- Team sharing
- Browser integration

**LastPass**
- Free password manager
- Browser integration
- Mobile apps

## Quick Reference

### Essential Tools Checklist

- [ ] Git CLI or GUI installed
- [ ] Code editor/IDE configured
- [ ] Linter/formatter configured
- [ ] Pre-commit hooks installed
- [ ] API testing tool (Postman/Insomnia)
- [ ] Database tool (if working with databases)
- [ ] Browser extensions installed
- [ ] Terminal enhancements (optional)

### Recommended Tools by Category

**Git:**
- Git CLI (required)
- GitHub Desktop (recommended GUI)

**Code Quality:**
- ESLint/Flake8 (linter)
- Prettier/Black (formatter)
- Pre-commit hooks

**Development:**
- VS Code or preferred IDE
- Postman or Insomnia
- Database GUI tool

**Productivity:**
- Terminal enhancements
- Browser extensions
- Note-taking app

## Tips

1. **Start simple**: Don't install everything at once
2. **Learn one tool well**: Better than many tools poorly
3. **Customize to your workflow**: Adapt tools to your needs
4. **Keep tools updated**: Regular updates for security and features
5. **Learn keyboard shortcuts**: Much faster than using mouse
6. **Use aliases**: Create shortcuts for common commands
7. **Automate repetitive tasks**: Scripts and tools can save time

---

**Next Steps**: Review [Best Practices](best-practices.md) to learn coding standards and principles.

