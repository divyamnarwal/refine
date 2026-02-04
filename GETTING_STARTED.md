# Getting Started - First Time Contributors Guide

Welcome to Refine! 🎉 This guide will walk you through making your first contribution to the Refine repository, step by step.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step 1: Fork and Clone the Repository](#step-1-fork-and-clone-the-repository)
- [Step 2: Install Dependencies](#step-2-install-dependencies)
- [Step 3: Understanding the Project Structure](#step-3-understanding-the-project-structure)
- [Step 4: Build the Project](#step-4-build-the-project)
- [Step 5: Make Your Changes](#step-5-make-your-changes)
- [Step 6: Test Your Changes](#step-6-test-your-changes)
- [Step 7: Commit Your Changes](#step-7-commit-your-changes)
- [Step 8: Create a Changeset](#step-8-create-a-changeset)
- [Step 9: Push and Create a Pull Request](#step-9-push-and-create-a-pull-request)
- [Getting Help](#getting-help)

## Prerequisites

Before you begin, make sure you have the following installed on your computer:

### Required Software

1. **Node.js** (version 18 or higher)
   - Download from: https://nodejs.org/
   - Check your version: `node --version`

2. **Git**
   - Download from: https://git-scm.com/
   - Check your version: `git --version`

3. **pnpm** (version 9 or higher)
   - Install with: `npm install -g pnpm`
   - Check your version: `pnpm --version`

4. **GitHub Account**
   - Sign up at: https://github.com/

5. **Code Editor** (recommended)
   - [Visual Studio Code](https://code.visualstudio.com/) with the [Biome extension](https://marketplace.visualstudio.com/items?itemName=biomejs.biome)

> **Windows Users:** You may also need [Microsoft Visual C++ Redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)

## Step 1: Fork and Clone the Repository

### 1.1 Fork the Repository

1. Go to the [Refine repository](https://github.com/refinedev/refine)
2. Click the **Fork** button in the top-right corner
3. This creates your own copy of the repository

### 1.2 Clone Your Fork

Now clone your fork to your local machine (replace `YOUR-USERNAME` with your GitHub username):

```bash
git clone https://github.com/YOUR-USERNAME/refine.git
cd refine
```

### 1.3 Add Upstream Remote

Add the original repository as an upstream remote to keep your fork updated:

```bash
git remote add upstream https://github.com/refinedev/refine.git
git remote -v
```

You should see:
- `origin` - your fork
- `upstream` - the original repository

## Step 2: Install Dependencies

Install all project dependencies using pnpm:

```bash
pnpm install
```

This command will:
- Install all dependencies for all packages
- Link local packages together
- Build all packages (this may take several minutes)

> **Quick Install:** If you want to skip building and just install dependencies, use: `pnpm install --ignore-scripts`

## Step 3: Understanding the Project Structure

Refine is a **monorepo** - a single repository containing multiple packages:

```
refine/
├── packages/          # Core Refine packages
│   ├── core/         # Main Refine package
│   ├── antd/         # Ant Design integration
│   ├── mui/          # Material UI integration
│   └── ...           # Other packages
├── examples/         # Example applications
├── documentation/    # Documentation website
├── cypress/          # End-to-end tests
└── scripts/          # Build and utility scripts
```

## Step 4: Build the Project

### Build All Packages

To build all packages:

```bash
pnpm build:all
```

### Build Specific Packages

To build only specific packages (faster for development):

```bash
# Build just the core package
pnpm build --scope @refinedev/core

# Build multiple packages
pnpm build --scope @refinedev/antd --scope @refinedev/core
```

### Development Mode (Watch Mode)

For active development, use watch mode to automatically rebuild on changes:

```bash
# Watch a package and an example together
pnpm dev --scope @refinedev/core --scope base-antd
```

This starts a development server that:
- Watches for file changes
- Automatically rebuilds on save
- Hot-reloads examples in the browser

## Step 5: Make Your Changes

### 5.1 Find or Create an Issue

1. Browse [existing issues](https://github.com/refinedev/refine/issues)
2. Look for issues labeled `good first issue` or `help wanted`
3. Comment on the issue to let others know you're working on it
4. If there's no issue for your change, create one first to discuss it

### 5.2 Create a New Branch

Always create a new branch for your changes:

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/bug-description
```

### 5.3 Make Your Changes

Now you can edit the code! Some tips:

- **Follow the existing code style** - we use Biome for linting and formatting
- **Keep changes focused** - one feature or fix per pull request
- **Add comments** only when necessary to explain complex logic
- **Test as you go** - use dev mode to see your changes in real-time

### 5.4 Running Linter

Check your code for style issues:

```bash
# Check for issues
pnpm lint

# Auto-fix issues
pnpm lint:fix
```

## Step 6: Test Your Changes

### Run Tests for Specific Package

```bash
# Test a specific package
pnpm test -- --scope @refinedev/core

# Test with coverage
pnpm test:coverage -- --scope @refinedev/core
```

### Run All Tests

```bash
pnpm test:all
```

### Write New Tests

If you're adding a new feature or fixing a bug:
- Add tests in the `test/` directory of the package
- Follow the existing test patterns
- Use Jest and React Testing Library

## Step 7: Commit Your Changes

### 7.1 Stage Your Changes

```bash
git add .
```

### 7.2 Commit with Conventional Commits

We use [Conventional Commits](https://www.conventionalcommits.org/) format:

```bash
git commit -m "feat(core): add new awesome feature"
# or
git commit -m "fix(antd): resolve button styling issue"
# or
git commit -m "docs: update getting started guide"
```

**Commit Types:**
- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation changes
- `style` - Code style changes (formatting, etc.)
- `refactor` - Code refactoring
- `test` - Adding or updating tests
- `chore` - Maintenance tasks

**Examples:**
```bash
git commit -m "feat(mui): add dark mode support"
git commit -m "fix(core): handle null values in useForm"
git commit -m "docs(readme): fix installation instructions"
```

## Step 8: Create a Changeset

Changesets describe your changes and help with versioning and changelog generation.

### 8.1 Run Changeset Command

```bash
pnpm changeset
```

### 8.2 Answer the Questions

The CLI will ask you:

1. **Which packages are affected?**
   - Use arrow keys and space to select
   - Press Enter when done

2. **What type of change is this?**
   - `major` - Breaking changes (avoid for first contribution)
   - `minor` - New features (backward compatible)
   - `patch` - Bug fixes

3. **Describe your changes**
   - Explain what changed
   - Include the issue number
   - Example: "feat: add dark mode support #1234"

### 8.3 Review the Changeset

A file is created in `.changeset/` directory. You can edit it to improve the description.

Example changeset:

```md
---
"@refinedev/core": minor
---

feat: add dark mode support #1234

Added support for dark mode themes in the core package.
Users can now toggle dark mode using the new `useDarkMode` hook.

Resolves #1234
```

### 8.4 Commit the Changeset

```bash
git add .changeset
git commit -m "chore: add changeset"
```

## Step 9: Push and Create a Pull Request

### 9.1 Push to Your Fork

```bash
git push origin feature/your-feature-name
```

### 9.2 Create Pull Request

1. Go to your fork on GitHub
2. Click **Compare & pull request** button
3. Fill in the pull request template:
   - **Title**: Clear, descriptive title
   - **Description**: Explain what and why
   - **Issue**: Link to related issue
   - **Screenshots**: If UI changes, include before/after

### 9.3 Wait for Review

- Maintainers will review your PR
- They may request changes
- Address feedback and push updates
- Your PR will be merged when approved! 🎉

## Getting Help

Stuck? Need help? We're here for you!

- **Discord**: Join our [Discord community](https://discord.gg/refine)
- **GitHub Discussions**: Ask questions in [Discussions](https://github.com/refinedev/refine/discussions)
- **Documentation**: Read the [full contributing guide](https://refine.dev/docs/contributing/)

## Quick Reference Commands

```bash
# Install dependencies
pnpm install

# Build all packages
pnpm build:all

# Build specific package
pnpm build --scope @refinedev/core

# Development mode
pnpm dev --scope @refinedev/core --scope base-antd

# Run linter
pnpm lint
pnpm lint:fix

# Run tests
pnpm test -- --scope @refinedev/core
pnpm test:all

# Create changeset
pnpm changeset

# Commit
git commit -m "feat(scope): description"

# Push
git push origin your-branch-name
```

## Additional Resources

- [Full Contributing Guide](https://refine.dev/docs/contributing/)
- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Documentation](https://refine.dev/docs/)
- [Examples](https://refine.dev/examples/)

---

**Thank you for contributing to Refine! 🚀**

We appreciate every contribution, no matter how small. Happy coding!
