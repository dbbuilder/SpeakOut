# Contributing to SpeakOut AAC App

Thank you for considering contributing to SpeakOut! This document provides guidelines for contributing to this meaningful project.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Code Style Guidelines](#code-style-guidelines)
- [Pull Request Process](#pull-request-process)
- [Testing Requirements](#testing-requirements)
- [Accessibility Guidelines](#accessibility-guidelines)

## Code of Conduct

This project and everyone participating in it is governed by our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check existing issues. When creating a bug report, include:

- **Clear title and description**
- **Steps to reproduce** the problem
- **Expected vs actual behavior**
- **Screenshots** if applicable
- **Environment details** (device, OS, browser)
- **Severity** (Critical, High, Medium, Low)

Use the bug report template when creating an issue.

### Suggesting Features

Feature suggestions are welcome! Please:

- Use the feature request template
- Explain the **problem** you're trying to solve
- Describe your **proposed solution**
- Consider **accessibility implications**
- Think about how it benefits **non-verbal users**

### Code Contributions

We love pull requests! Here's the process:

1. **Fork the repository**
2. **Create a feature branch** from `develop`
3. **Make your changes** with tests
4. **Ensure all tests pass**
5. **Submit a pull request**

## Development Setup

### Prerequisites

- Python 3.11+
- Node.js 18+
- PostgreSQL 14+
- Azure account (for testing Computer Vision)

### Backend Setup

```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env
# Edit .env with your configuration
alembic upgrade head
pytest
```

### Frontend Setup

```bash
cd frontend
npm install
cp .env.example .env
# Edit .env with your configuration
npm run dev
npm run test
```

## Code Style Guidelines

### Python (Backend)

- **Style**: Follow PEP 8
- **Formatter**: Use `black` (line length: 100)
- **Linter**: Use `flake8`
- **Type Hints**: Required for all functions
- **Docstrings**: Google style for classes and public methods

```python
def suggest_verbs(object_id: int, context: dict) -> list[Verb]:
    """Suggest contextually appropriate verbs for an object.

    Args:
        object_id: ID of the selected object
        context: Context dict with time_of_day, recent_verbs, etc.

    Returns:
        List of suggested Verb objects ordered by relevance
    """
    # Implementation
```

**Check before committing:**
```bash
black app/
flake8 app/
mypy app/
```

### JavaScript/Vue (Frontend)

- **Style**: Airbnb JavaScript Style Guide
- **Formatter**: Prettier
- **Linter**: ESLint
- **Comments**: JSDoc for complex functions

```javascript
/**
 * Construct a sentence from selected components
 * @param {Object} object - Selected object
 * @param {Object} verb - Selected verb
 * @param {Object} modifier - Optional modifier
 * @returns {string} Grammatically correct sentence
 */
function constructSentence(object, verb, modifier = null) {
  // Implementation
}
```

**Check before committing:**
```bash
npm run lint
npm run format
```

### Commit Messages

Use [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: add emotion selection component
fix: resolve camera permission on iOS
docs: update API documentation
test: add tests for verb suggestion logic
refactor: simplify sentence construction
chore: update dependencies
```

## Pull Request Process

### Before Submitting

- [ ] Code follows style guidelines
- [ ] All tests pass locally
- [ ] New tests added for new features
- [ ] Documentation updated
- [ ] No new warnings introduced
- [ ] Accessibility checked (WCAG AAA)
- [ ] Self-review completed

### PR Template Checklist

When you create a PR, fill out the template completely:

- **Description**: Clear summary of changes
- **Issue**: Link to related issue
- **Type of change**: Bug fix, feature, etc.
- **Testing**: How you tested the changes
- **Screenshots**: For UI changes
- **Checklist**: All items checked

### Review Process

1. At least **one approval** required
2. All **CI checks must pass**
3. **No unresolved conversations**
4. Branch must be **up to date** with develop
5. Maintainers may request changes

### Merging

- PRs are merged via **squash and merge**
- Commit message will be PR title
- Delete branch after merge

## Testing Requirements

### Coverage

- **Backend**: Aim for 80%+ coverage
- **Frontend**: Aim for 70%+ coverage
- **Critical paths**: 100% coverage required

### Test Types

**Backend:**
```bash
# Unit tests
pytest tests/unit/

# Integration tests
pytest tests/integration/

# All tests with coverage
pytest --cov=app --cov-report=html
```

**Frontend:**
```bash
# Unit tests
npm run test:unit

# E2E tests
npm run test:e2e

# Coverage
npm run test:unit -- --coverage
```

### Writing Tests

**Backend (pytest):**
```python
def test_suggest_verbs_for_food():
    """Test that food objects get appropriate verb suggestions"""
    object_id = create_test_object(category="food")
    verbs = suggest_verbs(object_id, {})

    verb_texts = [v.text for v in verbs]
    assert "eat" in verb_texts
    assert "drink" in verb_texts
    assert "want" in verb_texts
```

**Frontend (Vitest):**
```javascript
describe('SentenceBuilder', () => {
  it('constructs correct sentence from components', () => {
    const sentence = constructSentence(
      { name: 'water' },
      { text: 'want' },
      { text: 'please' }
    )
    expect(sentence).toBe('I want water please')
  })
})
```

## Accessibility Guidelines

**This is critical** - all contributions must meet WCAG AAA standards.

### Visual

- **Contrast**: 7:1 ratio minimum
- **Touch targets**: 60px × 60px minimum
- **Text size**: Adjustable, default 16px minimum
- **Color**: Never use color alone to convey information

### Keyboard Navigation

- All interactive elements must be keyboard accessible
- Logical tab order
- Visible focus indicators
- No keyboard traps

### Screen Readers

- Semantic HTML (`<button>`, `<nav>`, etc.)
- ARIA labels where needed
- Alt text for images
- Form labels properly associated

### Testing Accessibility

**Automated:**
```bash
# Run axe accessibility tests
npm run test:a11y
```

**Manual:**
- Test with screen reader (NVDA, JAWS, VoiceOver)
- Test keyboard-only navigation
- Test with high contrast mode
- Test with text zoom at 200%

### Resources

- [WCAG AAA Guidelines](https://www.w3.org/WAI/WCAG2AAA-Conformance)
- [WebAIM](https://webaim.org/)
- [A11y Project](https://www.a11yproject.com/)

## Questions?

- Open a [Discussion](https://github.com/dbbuilder/SpeakOut/discussions)
- Join our [community chat] (if available)
- Email: [contact email]

## Recognition

Contributors will be recognized in:
- README.md contributors section
- Release notes
- Annual contributor spotlight

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for helping make communication accessible to everyone!** ❤️
