# GitHub Repository Setup Guide

This guide provides step-by-step instructions for setting up the AAC Communication App GitHub repository with best practices, templates, and automation.

---

## 1. Create Repository

### Option A: GitHub CLI
```bash
gh repo create aac-communication-app --public --description "AI-powered AAC communication app for non-verbal individuals"
cd aac-communication-app
```

### Option B: GitHub Web Interface
1. Go to https://github.com/new
2. Repository name: `aac-communication-app`
3. Description: "AI-powered AAC communication app for non-verbal individuals"
4. Public repository
5. Don't initialize with README (we have our own)
6. Click "Create repository"

---

## 2. Initialize Local Repository

```bash
git init
git add .
git commit -m "Initial commit: Complete project planning documentation"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/aac-communication-app.git
git push -u origin main
```

---

## 3. Create Branch Protection Rules

### Protect Main Branch
```bash
# Via GitHub CLI
gh api repos/:owner/:repo/branches/main/protection \
  --method PUT \
  --field required_status_checks='{"strict":true,"contexts":["Backend CI","Frontend CI"]}' \
  --field enforce_admins=true \
  --field required_pull_request_reviews='{"dismissal_restrictions":{},"dismiss_stale_reviews":true,"require_code_owner_reviews":false,"required_approving_review_count":1}' \
  --field restrictions=null \
  --field required_linear_history=true \
  --field allow_force_pushes=false \
  --field allow_deletions=false
```

### Via Web Interface
1. Go to Settings → Branches
2. Click "Add rule"
3. Branch name pattern: `main`
4. Check:
   - ✅ Require a pull request before merging
   - ✅ Require approvals (1)
   - ✅ Dismiss stale pull request approvals when new commits are pushed
   - ✅ Require status checks to pass before merging
   - ✅ Require linear history
   - ✅ Do not allow bypassing the above settings
5. Click "Create"

### Create Develop Branch
```bash
git checkout -b develop
git push -u origin develop
```

---

## 4. Create GitHub Issue Templates

### Create .github/ISSUE_TEMPLATE/ directory
```bash
mkdir -p .github/ISSUE_TEMPLATE
```

### Bug Report Template
File: `.github/ISSUE_TEMPLATE/bug_report.md`

```markdown
---
name: Bug Report
about: Report a bug to help us improve
title: '[BUG] '
labels: bug
assignees: ''
---

## Bug Description
A clear and concise description of the bug.

## Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. Scroll down to '...'
4. See error

## Expected Behavior
What you expected to happen.

## Actual Behavior
What actually happened.

## Screenshots
If applicable, add screenshots to help explain your problem.

## Environment
- **Device**: [e.g., iPhone 12, iPad Pro, Desktop]
- **OS**: [e.g., iOS 15, Android 12, Windows 11]
- **Browser**: [e.g., Safari, Chrome, Firefox]
- **App Version**: [e.g., 1.0.0]

## Additional Context
Any other context about the problem.

## Severity
- [ ] Critical (app crashes, data loss)
- [ ] High (feature unusable)
- [ ] Medium (feature partially working)
- [ ] Low (cosmetic issue)
```

### Feature Request Template
File: `.github/ISSUE_TEMPLATE/feature_request.md`

```markdown
---
name: Feature Request
about: Suggest an idea for this project
title: '[FEATURE] '
labels: enhancement
assignees: ''
---

## Problem Statement
Is your feature request related to a problem? Please describe.
A clear and concise description of what the problem is. Ex. I'm always frustrated when [...]

## Proposed Solution
A clear and concise description of what you want to happen.

## Alternatives Considered
A clear and concise description of any alternative solutions or features you've considered.

## Benefits
Who will benefit from this feature? How?

## Implementation Ideas
If you have ideas on how to implement this, please share.

## Additional Context
Add any other context or screenshots about the feature request here.

## Priority
- [ ] Critical (blocking current usage)
- [ ] High (significantly improves UX)
- [ ] Medium (nice to have)
- [ ] Low (future enhancement)
```

### Issue Template Config
File: `.github/ISSUE_TEMPLATE/config.yml`

```yaml
blank_issues_enabled: false
contact_links:
  - name: Questions and Discussions
    url: https://github.com/YOUR_USERNAME/aac-communication-app/discussions
    about: Ask questions and discuss ideas with the community
  - name: Security Issues
    url: https://github.com/YOUR_USERNAME/aac-communication-app/security/advisories/new
    about: Report security vulnerabilities privately
```

---

## 5. Create Pull Request Template

File: `.github/pull_request_template.md`

```markdown
## Description
Please include a summary of the changes and the related issue. Include relevant motivation and context.

Fixes # (issue)

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Refactoring (no functional changes)
- [ ] Performance improvement
- [ ] Test addition or update

## How Has This Been Tested?
Please describe the tests that you ran to verify your changes.

- [ ] Unit tests
- [ ] Integration tests
- [ ] E2E tests
- [ ] Manual testing

**Test Configuration**:
- Device:
- OS:
- Browser:

## Checklist
- [ ] My code follows the style guidelines of this project
- [ ] I have performed a self-review of my own code
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] I have made corresponding changes to the documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing unit tests pass locally with my changes
- [ ] Any dependent changes have been merged and published
- [ ] I have checked my code for accessibility (WCAG AAA)

## Screenshots (if applicable)
Add screenshots to help explain your changes.

## Additional Notes
Any additional information that reviewers should know.
```

---

## 6. Create GitHub Actions Workflows

### Backend CI Workflow
File: `.github/workflows/backend-ci.yml`

```yaml
name: Backend CI

on:
  push:
    branches: [ main, develop ]
    paths:
      - 'backend/**'
      - '.github/workflows/backend-ci.yml'
  pull_request:
    branches: [ main, develop ]
    paths:
      - 'backend/**'
      - '.github/workflows/backend-ci.yml'

jobs:
  test:
    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:14
        env:
          POSTGRES_USER: test
          POSTGRES_PASSWORD: test
          POSTGRES_DB: aac_test
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
        ports:
          - 5432:5432

    steps:
    - uses: actions/checkout@v3

    - name: Set up Python 3.11
      uses: actions/setup-python@v4
      with:
        python-version: '3.11'
        cache: 'pip'

    - name: Install dependencies
      run: |
        cd backend
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Lint with flake8
      run: |
        cd backend
        flake8 app/ --count --select=E9,F63,F7,F82 --show-source --statistics
        flake8 app/ --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics

    - name: Format check with black
      run: |
        cd backend
        black --check app/

    - name: Type check with mypy
      run: |
        cd backend
        mypy app/

    - name: Run tests with pytest
      env:
        DATABASE_URL: postgresql://test:test@localhost:5432/aac_test
        SECRET_KEY: test_secret_key_for_ci
        AZURE_CV_KEY: test_key
        AZURE_CV_ENDPOINT: https://test.cognitiveservices.azure.com/
      run: |
        cd backend
        pytest --cov=app --cov-report=xml --cov-report=html

    - name: Upload coverage to Codecov
      uses: codecov/codecov-action@v3
      with:
        file: ./backend/coverage.xml
        flags: backend
        name: backend-coverage
```

### Frontend CI Workflow
File: `.github/workflows/frontend-ci.yml`

```yaml
name: Frontend CI

on:
  push:
    branches: [ main, develop ]
    paths:
      - 'frontend/**'
      - '.github/workflows/frontend-ci.yml'
  pull_request:
    branches: [ main, develop ]
    paths:
      - 'frontend/**'
      - '.github/workflows/frontend-ci.yml'

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
        cache: 'npm'
        cache-dependency-path: frontend/package-lock.json

    - name: Install dependencies
      run: |
        cd frontend
        npm ci

    - name: Lint with ESLint
      run: |
        cd frontend
        npm run lint

    - name: Format check with Prettier
      run: |
        cd frontend
        npm run format:check

    - name: Type check (if using TypeScript)
      run: |
        cd frontend
        npm run type-check || echo "No type checking configured"

    - name: Run unit tests
      run: |
        cd frontend
        npm run test:unit -- --coverage

    - name: Build production
      run: |
        cd frontend
        npm run build

    - name: Upload coverage to Codecov
      uses: codecov/codecov-action@v3
      with:
        file: ./frontend/coverage/coverage-final.json
        flags: frontend
        name: frontend-coverage
```

---

## 7. Create Additional Documentation Files

### LICENSE
```bash
curl -o LICENSE https://raw.githubusercontent.com/licenses/license-templates/master/templates/mit.txt
# Edit LICENSE to add your name and year
```

### CODE_OF_CONDUCT.md
```markdown
# Contributor Covenant Code of Conduct

## Our Pledge
We as members, contributors, and leaders pledge to make participation in our community a harassment-free experience for everyone, regardless of age, body size, visible or invisible disability, ethnicity, sex characteristics, gender identity and expression, level of experience, education, socio-economic status, nationality, personal appearance, race, religion, or sexual identity and orientation.

## Our Standards
Examples of behavior that contributes to a positive environment:
- Using welcoming and inclusive language
- Being respectful of differing viewpoints and experiences
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

Examples of unacceptable behavior:
- The use of sexualized language or imagery
- Trolling, insulting or derogatory comments, and personal or political attacks
- Public or private harassment
- Publishing others' private information without explicit permission
- Other conduct which could reasonably be considered inappropriate

## Enforcement
Instances of abusive, harassing, or otherwise unacceptable behavior may be reported to the project team at [your-email]. All complaints will be reviewed and investigated promptly and fairly.

## Attribution
This Code of Conduct is adapted from the Contributor Covenant, version 2.1.
```

### CONTRIBUTING.md
```markdown
# Contributing to AAC Communication App

Thank you for considering contributing to the AAC Communication App! This document provides guidelines for contributing.

## How Can I Contribute?

### Reporting Bugs
- Use the bug report template
- Include detailed steps to reproduce
- Provide screenshots if applicable
- Specify your environment (device, OS, browser)

### Suggesting Features
- Use the feature request template
- Explain the problem you're trying to solve
- Describe your proposed solution
- Consider accessibility implications

### Code Contributions

#### Development Setup
1. Fork the repository
2. Clone your fork: `git clone https://github.com/YOUR_USERNAME/aac-communication-app.git`
3. Create a branch: `git checkout -b feature/my-feature`
4. Follow the setup instructions in README.md

#### Code Style
- **Python**: Follow PEP 8, use `black` for formatting, `flake8` for linting
- **JavaScript**: Follow Airbnb style guide, use ESLint and Prettier
- **Commits**: Use conventional commits (feat:, fix:, docs:, etc.)

#### Testing
- Write unit tests for new features
- Ensure all tests pass before submitting PR
- Aim for 80%+ code coverage
- Test accessibility with screen readers

#### Pull Request Process
1. Update documentation for any user-facing changes
2. Ensure all CI checks pass
3. Request review from maintainers
4. Address review feedback
5. Squash commits if requested
6. Merge once approved

## Accessibility Guidelines
All contributions must meet WCAG AAA standards:
- Minimum 60px touch targets
- 7:1 contrast ratio
- Keyboard navigation support
- Screen reader compatibility

## Questions?
Open a discussion in GitHub Discussions or email [your-email].

Thank you for helping make communication accessible to everyone!
```

### SECURITY.md
```markdown
# Security Policy

## Supported Versions
| Version | Supported          |
| ------- | ------------------ |
| 1.x.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability
If you discover a security vulnerability, please report it privately:

1. **Do NOT** open a public issue
2. Email security@your-domain.com with:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)
3. Allow 48 hours for initial response
4. We will work with you to understand and address the issue
5. Public disclosure only after fix is deployed

## Security Best Practices
- All secrets stored in Azure Key Vault
- HTTPS/TLS 1.3 required for all communications
- Images auto-deleted after 24 hours
- JWT tokens with short expiration
- Rate limiting on all endpoints
- Input validation and sanitization
- Regular security audits

Thank you for helping keep our users safe!
```

### CHANGELOG.md
```markdown
# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0] - 2025-XX-XX
### Added
- Camera capture and image upload
- Azure Computer Vision object detection
- Rule-based verb suggestions
- Sentence construction with templates
- Web Speech API text-to-speech
- User authentication with JWT
- Feedback collection (thumbs up/down)
- PostgreSQL database with Alembic migrations
- Responsive UI with Tailwind CSS
- WCAG AAA accessibility compliance

### Security
- HTTPS/TLS 1.3 enforcement
- Password hashing with bcrypt
- Secrets in Azure Key Vault
- Rate limiting on API endpoints

[Unreleased]: https://github.com/YOUR_USERNAME/aac-communication-app/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/YOUR_USERNAME/aac-communication-app/releases/tag/v1.0.0
```

---

## 8. Set Up GitHub Projects

### Create Project Board
1. Go to repository → Projects → New project
2. Choose "Board" template
3. Name: "AAC App Development"
4. Add columns:
   - 📋 Backlog
   - 📝 To Do
   - 🏗️ In Progress
   - 👀 In Review
   - ✅ Done

### Create Milestones
1. Go to Issues → Milestones → New milestone
2. Create milestones for each phase:
   - **Phase 1: MVP** (Due: 4 weeks from start)
   - **Phase 2: Enhanced Intelligence** (Due: 8 weeks from start)
   - **Phase 3: Advanced Learning** (Due: 12 weeks from start)
   - **Phase 4: Offline & Mobile** (Due: 16 weeks from start)
   - **Phase 5: Extended Features** (Due: 20 weeks from start)

---

## 9. Set Up Branch Strategy

### Branch Naming Convention
- **Feature branches**: `feature/description` (e.g., `feature/camera-capture`)
- **Bug fix branches**: `fix/description` (e.g., `fix/auth-token-expiry`)
- **Hotfix branches**: `hotfix/description` (e.g., `hotfix/security-patch`)
- **Release branches**: `release/version` (e.g., `release/1.0.0`)

### Workflow
```
main (production)
  ↑
release/1.0.0 (release preparation)
  ↑
develop (integration)
  ↑
feature/my-feature (development)
```

---

## 10. Additional Setup

### Enable GitHub Discussions
1. Go to Settings → General
2. Scroll to "Features"
3. Check "Discussions"
4. Categories: Announcements, Q&A, Ideas, Show and Tell

### Enable Dependabot
File: `.github/dependabot.yml`

```yaml
version: 2
updates:
  - package-ecosystem: "pip"
    directory: "/backend"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 5

  - package-ecosystem: "npm"
    directory: "/frontend"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 5

  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
```

### Add Repository Topics
1. Go to repository main page
2. Click gear icon next to "About"
3. Add topics: `aac`, `accessibility`, `assistive-technology`, `autism`, `communication`, `vue`, `python`, `fastapi`, `azure`, `ai`

---

## 11. Commit and Push All Setup Files

```bash
git add .github/
git add LICENSE CODE_OF_CONDUCT.md CONTRIBUTING.md SECURITY.md CHANGELOG.md
git commit -m "chore: Add GitHub repository configuration and templates"
git push origin main
```

---

## Congratulations!

Your GitHub repository is now fully set up with:
- ✅ Branch protection rules
- ✅ Issue and PR templates
- ✅ CI/CD workflows
- ✅ Project board and milestones
- ✅ Documentation and policies
- ✅ Security and contribution guidelines

You're ready to start development! 🚀

---

**Last Updated**: 2025-10-31
