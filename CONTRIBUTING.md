# Contributing to HashTrace

Thank you for your interest in contributing to HashTrace! This document provides guidelines and instructions for contributing to the project.

## Getting Started

### Prerequisites

- Git
- Node.js 18+
- Python 3.9+
- PostgreSQL 13+
- Redis 6+

### Setup Development Environment

```bash
git clone https://github.com/yourusername/hashtrace.git
cd hashtrace
npm install
docker-compose up -d
npm run dev
```

## Development Workflow

### 1. Create a Feature Branch

```bash
git checkout -b feature/your-feature-name
```

### 2. Make Your Changes

- Write clean, readable code
- Follow the project's code style
- Add tests for new features
- Update documentation

### 3. Commit Your Changes

Follow conventional commit format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**: feat, fix, docs, style, refactor, test, chore

**Example**:
```
feat(api): add event filtering endpoint

Add support for filtering events by type and time range.
Implement pagination for large result sets.

Closes #456
```

### 4. Push and Create Pull Request

```bash
git push origin feature/your-feature-name
```

## Code Style

### JavaScript/TypeScript

- Use ESLint: `npm run lint`
- Format with Prettier: `npm run format`

### Python

- Follow PEP 8
- Use pylint: `pylint src/`
- Format with black: `black src/`

## Testing

```bash
npm test                    # Run all tests
npm test -- tests/api       # Specific test file
npm test -- --coverage      # With coverage
npm run test:integration    # Integration tests
```

## Pull Request Process

1. Run tests: `npm test`
2. Check linting: `npm run lint`
3. Update documentation
4. Rebase on main: `git rebase main`
5. Create Pull Request with clear description

## Questions?

- Check [documentation](docs/)
- Search existing [issues](https://github.com/yourusername/hashtrace/issues)
- Open a new [discussion](https://github.com/yourusername/hashtrace/discussions)

---

Thank you for contributing to HashTrace!
