# Contributing to MAIO

Thank you for your interest in contributing to the MAIO platform! This document provides guidelines and instructions for contributing to the project.

---

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Making Changes](#making-changes)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Testing](#testing)
- [Documentation](#documentation)
- [Reporting Issues](#reporting-issues)

---

## 🤝 Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inspiring community for all. We value:

- **Respect**: Treat all community members with respect
- **Inclusivity**: Welcome contributions from people of all backgrounds
- **Professionalism**: Maintain a professional and courteous tone
- **Collaboration**: Work together to improve the project

### Unacceptable Behavior

The following behaviors are unacceptable:

- Harassment or discrimination
- Offensive comments
- Personal attacks
- Unwanted advances
- Doxing or publishing private information

**Violation Reports**: Contact [conduct@maio-health.com](mailto:conduct@maio-health.com)

---

## 🚀 Getting Started

### Prerequisites

- **Git**: Version control
- **Node.js**: v18 or higher
- **npm or yarn**: Package manager
- **GitHub Account**: For forking and submitting PRs

### Fork & Clone

1. **Fork the Repository**

   - Click "Fork" button on GitHub
   - Creates your copy of the project

2. **Clone Your Fork**

   ```bash
   git clone https://github.com/YOUR_USERNAME/MAIO.git
   cd MAIO
   ```

3. **Add Upstream Remote**
   ```bash
   git remote add upstream https://github.com/original-repo/MAIO.git
   ```

---

## 🛠️ Development Setup

### Backend Setup

```bash
cd MAIO-Backend
npm install

# Create .env file
cp .env.example .env

# Edit .env with your configuration
# Then start the server
npm start
```

### Frontend Setup

```bash
cd MAIO-front
npm install

# Create .env.local file
cp .env.example .env.local

# Edit .env.local with your configuration
# Then start dev server
npm run dev
```

### Admin Dashboard Setup

```bash
cd maiodashboard
npm install

# Create .env.local file
cp .env.example .env.local

# Edit .env.local with your configuration
# Then start dev server
npm run dev
```

---

## 💻 Making Changes

### Create a Feature Branch

```bash
# Update your local main
git fetch upstream
git checkout main
git merge upstream/main

# Create feature branch
git checkout -b feature/your-feature-name
```

### Branch Naming Conventions

```
feature/feature-name          # New feature
bugfix/bug-description        # Bug fix
docs/documentation-update     # Documentation
refactor/refactoring-task     # Code refactoring
perf/performance-improvement  # Performance optimization
test/test-additions          # Test additions
```

### Make Your Changes

1. **Edit Files**: Make your improvements to the codebase
2. **Test Locally**: Ensure changes work correctly
3. **Follow Standards**: Adhere to coding guidelines
4. **Update Docs**: If applicable, update documentation

---

## 📝 Commit Guidelines

### Commit Message Format

```
type(scope): subject

body

footer
```

### Types

- **feat**: A new feature
- **fix**: A bug fix
- **docs**: Documentation only changes
- **style**: Changes that don't affect code meaning (formatting, etc.)
- **refactor**: Code change that neither fixes a bug nor adds a feature
- **perf**: Code change that improves performance
- **test**: Adding or updating tests
- **chore**: Changes to build process, dependencies, etc.

### Examples

```
feat(auth): add two-factor authentication

- Implement TOTP-based 2FA
- Add backup codes functionality
- Update user settings UI

Closes #123
```

```
fix(api): resolve appointment creation race condition

Fixed a race condition where multiple simultaneous appointment
creation requests could result in duplicate bookings.

Closes #456
```

### Best Practices

- Use present tense ("add" not "added")
- Use imperative mood ("move cursor to..." not "moves cursor to...")
- Limit subject line to 50 characters
- Wrap body at 72 characters
- Reference issues and pull requests liberally
- One logical change per commit

---

## 🔄 Pull Request Process

### Before Submitting

1. **Rebase Your Branch**

   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Run Tests**

   ```bash
   npm test
   ```

3. **Run Linter**

   ```bash
   npm run lint
   ```

4. **Build Check**
   ```bash
   npm run build
   ```

### Submit Pull Request

1. **Push Your Branch**

   ```bash
   git push origin feature/your-feature-name
   ```

2. **Create Pull Request**

   - Go to GitHub and create PR
   - Use PR template if provided
   - Link related issues

3. **PR Title Format**

   ```
   type(scope): description

   Example: feat(appointments): add reschedule functionality
   ```

4. **PR Description Template**

   ```markdown
   ## Description

   Brief description of changes

   ## Type of Change

   - [ ] Bug fix (non-breaking)
   - [ ] New feature (non-breaking)
   - [ ] Breaking change
   - [ ] Documentation update

   ## Related Issues

   Closes #123

   ## Testing

   How to test these changes

   ## Checklist

   - [ ] Code follows style guidelines
   - [ ] Self-review completed
   - [ ] Comments added for complex logic
   - [ ] Documentation updated
   - [ ] Tests added/updated
   - [ ] No new warnings generated
   - [ ] Changes tested locally
   ```

### Review Process

- Maintainers will review your PR
- Changes may be requested
- Once approved, your PR will be merged

---

## 📐 Coding Standards

### Backend (Node.js/Express)

```javascript
// Use consistent indentation (2 spaces)
function calculateTotal(items) {
  return items.reduce((sum, item) => {
    return sum + item.price;
  }, 0);
}

// Use meaningful variable names
const userEmailAddress = user.email;

// Add comments for complex logic
// Calculate discount based on user loyalty status
const discount = user.loyaltyMonths > 12 ? 0.1 : 0.05;

// Use async/await
async function fetchUser(id) {
  try {
    const user = await User.findById(id);
    return user;
  } catch (error) {
    logger.error("Failed to fetch user:", error);
    throw error;
  }
}

// Error handling
if (!email || !password) {
  return res.status(400).json({
    success: false,
    message: "Email and password required",
  });
}
```

### Frontend (React/TypeScript)

```typescript
// Use functional components with hooks
interface UserCardProps {
  user: User;
  onSelect?: (userId: string) => void;
}

export const UserCard: React.FC<UserCardProps> = ({ user, onSelect }) => {
  const handleClick = () => {
    onSelect?.(user.id);
  };

  return (
    <div className="card" onClick={handleClick}>
      <h3>{user.name}</h3>
      <p>{user.email}</p>
    </div>
  );
};

// Use custom hooks for logic
function useUserData(userId: string) {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const fetchUser = async () => {
      try {
        const data = await api.getUser(userId);
        setUser(data);
      } catch (error) {
        console.error("Failed to fetch user:", error);
      } finally {
        setLoading(false);
      }
    };

    fetchUser();
  }, [userId]);

  return { user, loading };
}
```

### General Rules

- **Naming**: Use camelCase for variables/functions, PascalCase for components/classes
- **Indentation**: 2 spaces (not tabs)
- **Quotes**: Single quotes for JS, double quotes for JSX attributes
- **Semicolons**: Always use semicolons
- **Line Length**: Max 100 characters
- **Comments**: Use meaningful comments, not obvious ones
- **Functions**: Keep functions small and focused
- **Variables**: Declare close to usage

---

## 🧪 Testing

### Backend Tests

```bash
cd MAIO-Backend
npm test
```

### Frontend Tests

```bash
cd MAIO-front
npm test
```

### Test Coverage

- Aim for >80% coverage for critical features
- Write tests for bug fixes
- Use descriptive test names

### Testing Checklist

- [ ] Unit tests for functions
- [ ] Integration tests for features
- [ ] Component tests for UI
- [ ] E2E tests for user flows
- [ ] Manual testing in browser
- [ ] Cross-browser testing

---

## 📖 Documentation

### When to Update Documentation

- Adding new features
- Changing existing behavior
- API endpoint modifications
- Configuration changes
- New setup requirements

### Documentation Style

- Use clear, concise language
- Provide examples
- Include diagrams when helpful
- Keep TOC updated
- Update related docs

### Examples

````markdown
## Feature Name

Brief description of the feature.

### Prerequisites

- Requirement 1
- Requirement 2

### Usage

```javascript
// Code example
```
````

### Configuration

| Option    | Type    | Default | Description |
| --------- | ------- | ------- | ----------- |
| `option1` | string  | 'value' | Description |
| `option2` | boolean | true    | Description |

```

---

## 🐛 Reporting Issues

### Before Creating an Issue

- Search existing issues
- Check documentation
- Update to latest version
- Verify the behavior

### Issue Template

**Title**: Clear description of the issue

**Description**:
```

## Bug Description

Clear description of what happened

## Expected Behavior

What should happen

## Actual Behavior

What actually happens

## Steps to Reproduce

1. First step
2. Second step
3. Final step

## Environment

- Node.js version
- npm/yarn version
- OS and version
- Browser (if frontend issue)

## Additional Context

Any other relevant information

## Code Snippet

```javascript
// Relevant code
```

```

### Issue Labels

- **bug**: Something isn't working
- **enhancement**: New feature or improvement
- **documentation**: Documentation update
- **good first issue**: Good for newcomers
- **help wanted**: Seeking assistance
- **question**: Question about usage

---

## 🎯 What We're Looking For

### High Priority Areas

- Bug fixes
- Performance improvements
- Security enhancements
- Documentation improvements
- Test coverage

### Before Starting Major Work

1. Check open issues and PRs
2. Discuss in issue first for large changes
3. Get feedback from maintainers
4. Plan your implementation

### Code Review Checklist

- [ ] Code is clean and readable
- [ ] No console.log statements (except intentional)
- [ ] No commented-out code
- [ ] Follows project style guide
- [ ] Tests are included
- [ ] Documentation is updated
- [ ] No new warnings
- [ ] Performance is acceptable

---

## 🚀 After Your PR is Merged

- Your code is live!
- Monitor for any issues
- Be available for discussions
- Help others with similar contributions

---

## 💬 Getting Help

- **GitHub Issues**: Ask questions via issues
- **Discussion**: Use GitHub Discussions
- **Email**: community@maio-health.com
- **Slack**: Join our community channel

---

## 📚 Additional Resources

- [Git Documentation](https://git-scm.com/doc)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)
- [React Best Practices](https://react.dev/learn)
- [Express.js Guide](https://expressjs.com/en/guide/routing.html)

---

## 📋 Project-Specific Guidelines

### Backend

- Use async/await over callbacks
- Implement proper error handling
- Write unit tests for all utilities
- Document API endpoints
- Follow RESTful conventions

### Frontend

- Use React hooks
- Implement proper error boundaries
- Optimize performance with React.memo
- Use TypeScript for type safety
- Write component tests

### Admin Dashboard

- Use Next.js app router
- Implement proper loading states
- Use Tailwind CSS classes
- Follow Next.js conventions
- Optimize for SEO when applicable

---

## 🙏 Thank You!

Your contributions make MAIO better for everyone. We appreciate your effort and enthusiasm!

---

**Last Updated**: January 2026 | **Version**: 1.0.0
```
