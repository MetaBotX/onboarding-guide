# Project Setup Checklist

Use this checklist to ensure your development environment is properly configured when joining a MetaBotX project.

## Initial Setup Steps

### Repository Access and Permissions

- [ ] Repository access granted
- [ ] SSH keys configured (or HTTPS credentials)
- [ ] Two-factor authentication enabled (if required)
- [ ] Repository cloned locally
- [ ] Remotes configured correctly

### Cloning the Repository

```bash
# Clone via SSH (if SSH keys configured)
git clone git@github.com:organization/repository.git

# Clone via HTTPS
git clone https://github.com/organization/repository.git

# Navigate to repository
cd repository
```

### Setting Up SSH Keys

```bash
# Generate SSH key (if not exists)
ssh-keygen -t ed25519 -C "your_email@example.com"

# Add SSH key to ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard
cat ~/.ssh/id_ed25519.pub | pbcopy  # macOS
cat ~/.ssh/id_ed25519.pub | xclip    # Linux

# Add to GitHub: Settings → SSH Keys (MetaBotX GitHub account)
```

### Configuring Git

```bash
# Set your name and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default editor (optional)
git config --global core.editor "code --wait"  # VS Code
git config --global core.editor "vim"           # Vim
git config --global core.editor "nano"          # Nano

# Set default branch name
git config --global init.defaultBranch main

# Set pull strategy (optional)
git config --global pull.rebase false  # merge (default)
git config --global pull.rebase true   # rebase

# Verify configuration
git config --list
```

## Environment Setup

### Required Tools and Versions

Check project README for specific requirements:

- [ ] **Git** (version 2.30+ recommended)
  ```bash
  git --version
  ```

- [ ] **Node.js** (if working with JavaScript/TypeScript)
  ```bash
  node --version
  npm --version
  # or
  nvm install <version>
  ```

- [ ] **Python** (if working with Python)
  ```bash
  python --version
  # or
  python3 --version
  ```

- [ ] **Docker** (if using containers)
  ```bash
  docker --version
  docker-compose --version
  ```

- [ ] **Database** (PostgreSQL, MySQL, MongoDB, etc.)
  ```bash
  # Check if database is running
  # Verify connection
  ```

- [ ] **Other project-specific tools**
  - Check project README for complete list

### IDE/Editor Setup

- [ ] **Editor installed** (VS Code, IntelliJ, Vim, etc.)
- [ ] **Extensions installed**:
  - Language support extensions
  - Git integration
  - Linting/formatting extensions
  - Project-specific extensions
- [ ] **Editor configured**:
  - Settings synced or configured
  - Key bindings configured
  - Workspace settings (if applicable)

### Recommended VS Code Extensions

```json
{
  "recommendations": [
    "editorconfig.editorconfig",
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint",
    "ms-python.python",
    "ms-python.black-formatter",
    "eamodio.gitlens",
    "github.vscode-pull-request-github"
  ]
}
```

### Linting and Formatting Tools

- [ ] **Pre-commit hooks installed**
  ```bash
  # For Python projects
  pip install pre-commit
  pre-commit install

  # For Node.js projects
  npm install
  # Hooks usually auto-install via package.json
  ```

- [ ] **Linters configured**:
  - ESLint (JavaScript/TypeScript)
  - Flake8/Black (Python)
  - RuboCop (Ruby)
  - Other project-specific linters

- [ ] **Formatters configured**:
  - Prettier (JavaScript/TypeScript)
  - Black (Python)
  - Other project-specific formatters

## Project-Specific Setup

### Environment Variables

- [ ] **Environment file created**
  ```bash
  # Copy example file
  cp .env.example .env
  
  # Or
  cp .env.template .env
  ```

- [ ] **Variables configured**:
  - API keys
  - Database credentials
  - Service URLs
  - Feature flags
  - Other project-specific variables

- [ ] **Sensitive data handling**:
  - Never commit `.env` files
  - Use secrets management tools
  - Follow project security guidelines

### Database Setup

- [ ] **Database installed** (if local development)
- [ ] **Database created**:
  ```bash
  # Example for PostgreSQL
  createdb project_name_dev
  ```

- [ ] **Migrations run**:
  ```bash
  # Example commands (varies by project)
  npm run migrate
  # or
  python manage.py migrate
  # or
  alembic upgrade head
  ```

- [ ] **Seed data loaded** (if applicable):
  ```bash
  npm run seed
  # or
  python manage.py loaddata seed.json
  ```

- [ ] **Connection verified**:
  - Test database connection
  - Verify tables/collections exist

### Local Services/Dependencies

- [ ] **Docker services running** (if using Docker):
  ```bash
  docker-compose up -d
  ```

- [ ] **Local services started**:
  - Redis
  - RabbitMQ
  - Elasticsearch
  - Other required services

- [ ] **API keys obtained**:
  - Third-party service keys
  - Development API keys
  - Test credentials

### Testing Environment

- [ ] **Test database configured** (if separate)
- [ ] **Test data prepared**
- [ ] **Test environment variables set**
- [ ] **Test suite can run**:
  ```bash
  npm test
  # or
  pytest
  # or
  python manage.py test
  ```

## Verification

### Running the Application

- [ ] **Application starts successfully**:
  ```bash
  npm start
  # or
  python manage.py runserver
  # or
  docker-compose up
  ```

- [ ] **Application accessible**:
  - Frontend: http://localhost:3000 (or project port)
  - Backend API: http://localhost:8000 (or project port)
  - Health check endpoint responds

- [ ] **Basic functionality works**:
  - Can navigate application
  - Can perform basic operations
  - No obvious errors

### Running Tests

- [ ] **Tests can be executed**:
  ```bash
  npm test
  # or
  pytest
  # or
  python manage.py test
  ```

- [ ] **All tests pass** (or expected failures only)
- [ ] **Test output is readable**
- [ ] **Coverage reports generate** (if applicable)

### Verifying Linting/Formatting

- [ ] **Linter runs successfully**:
  ```bash
  npm run lint
  # or
  flake8 .
  # or
  rubocop
  ```

- [ ] **Formatter runs successfully**:
  ```bash
  npm run format
  # or
  black .
  # or
  prettier --write .
  ```

- [ ] **Pre-commit hooks work**:
  ```bash
  # Make a test commit
  git add .
  git commit -m "test: verify setup"
  # Hooks should run automatically
  ```

## Common Setup Issues and Solutions

### Issue: Can't Clone Repository

**Solutions:**
- Verify SSH keys are added to your MetaBotX GitHub account
- Check repository access permissions
- Try HTTPS instead of SSH
- Verify network connectivity

### Issue: Dependencies Won't Install

**Solutions:**
- Check Node.js/Python version matches requirements
- Clear cache: `npm cache clean` or `pip cache purge`
- Delete `node_modules`/`venv` and reinstall
- Check for proxy/firewall issues

### Issue: Database Connection Fails

**Solutions:**
- Verify database is running
- Check connection string in `.env`
- Verify database credentials
- Check firewall/network settings
- Verify database exists

### Issue: Tests Fail

**Solutions:**
- Check test database is set up
- Verify test data is loaded
- Check environment variables
- Review test output for specific errors
- Ask team for help

### Issue: Pre-commit Hooks Fail

**Solutions:**
- Verify hooks are installed: `pre-commit install`
- Check hook configuration
- Run hooks manually: `pre-commit run --all-files`
- Review hook output for specific errors

### Issue: Application Won't Start

**Solutions:**
- Check logs for errors
- Verify all services are running
- Check environment variables
- Verify dependencies are installed
- Check port availability
- Review project README for specific requirements

## Getting Help

If you encounter issues:

1. **Check project documentation**: README, setup guides, wiki
2. **Review error messages**: Read logs carefully
3. **Search existing issues**: Check MetaBotX GitHub issues
4. **Ask the team**: Don't hesitate to ask for help
5. **Check common issues**: Review this guide's troubleshooting section

## Quick Reference

### Setup Commands

```bash
# Clone repository
git clone <repository-url>
cd <repository-name>

# Install dependencies
npm install              # Node.js
pip install -r requirements.txt  # Python
bundle install           # Ruby

# Setup environment
cp .env.example .env
# Edit .env with your values

# Setup database
npm run migrate          # Node.js
python manage.py migrate # Python/Django
alembic upgrade head     # Python/SQLAlchemy

# Install pre-commit hooks
pre-commit install       # Python
npm install             # Node.js (usually auto)

# Run application
npm start               # Node.js
python manage.py runserver  # Python/Django
docker-compose up       # Docker

# Run tests
npm test                # Node.js
pytest                  # Python
python manage.py test   # Python/Django
```

### Verification Checklist

- [ ] Repository cloned
- [ ] Dependencies installed
- [ ] Environment variables configured
- [ ] Database set up and migrated
- [ ] Application starts
- [ ] Tests pass
- [ ] Linting/formatting works
- [ ] Pre-commit hooks work

## Tips

1. **Follow the README**: Project README usually has setup instructions
2. **Ask early**: Don't spend hours stuck on setup
3. **Document issues**: Note any project-specific setup quirks
4. **Keep environment updated**: Regularly update dependencies
5. **Version control config**: Use `.gitconfig` for local-only settings
6. **Use Docker**: If available, Docker simplifies setup significantly

---

**Next Steps**: Once setup is complete, review the [Development Workflow](development-workflow.md) to start contributing.

