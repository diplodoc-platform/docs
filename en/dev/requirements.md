# Rules for external contributors

The page describes what you need to do to get your changes accepted into the Diplodoc project.

{% note warning %}

Before starting work on changes to the CLI, study the file [AGENTS.md](https://github.com/diplodoc-platform/cli/blob/master/AGENTS.md) — it contains context about the project's structure and architecture.

{% endnote %}


## Code requirements {#code-requirements}

### Code style and linting

Write code in a consistent style. For checking, use the [package `@diplodoc/lint`](https://www.npmjs.com/package/@diplodoc/lint):

- ESLint — checking JavaScript/TypeScript code.
- Prettier — code formatting.
- Stylelint — checking CSS/SCSS.

Before submitting a pull request, run:

```bash
npm run lint
```

To automatically fix errors:

```bash
npm run lint:fix
```

### TypeScript

- Write all source code in TypeScript.
- Extend the shared configuration `@diplodoc/infra/tsconfig.json`.
- Check types with the command `npm run typecheck`.

### Documenting architectural changes (ADR)

If your changes affect the project's architecture, create an [ADR](*adr) file in Markdown format in the appropriate repository folder. In the file, specify:

- the problem context;
- the considered solution options;
- the accepted decision and its rationale.

## Testing {#test-requirements}

Cover your changes with tests — this is a mandatory condition for accepting a pull request.

### Test runner

The project uses Vitest. Other test runners, such as Jest, are not supported.

```bash
npm run test        # Running tests
npm run test:watch  # Running in watch mode
```

### Test structure

- Unit tests — place them next to the code being tested:

  - `src/**/*.test.ts`
  - `src/**/*.spec.ts`
  - `src/**/__tests__/`

- Integration tests — in the `test/` directory (not `tests/`):

  - `test/**/*.test.ts`

### Configuration

Create a `vitest.config.mjs` file in the package root:

```javascript
import {defineConfig} from 'vitest/config';

export default defineConfig({
    test: {
        include: ['src/**/*.test.ts', 'test/**/*.test.ts'],
        exclude: ['node_modules', 'build'],
    },
});
```

## Pull request requirements {#pr-requirements}

### Description of changes

Add to the pull request:

- Problem description — what you are fixing or adding.
- Solution description — how you solved the problem.
- Links — to related issues or documentation.

#|
|| **Type of changes** | **What to add** ||
|| Bug fix | Link to the issue or a description of the bug ||
|| New functionality | Description of the functionality, usage examples ||
|| Visual changes | Screenshots or videos before/after ||
|| API changes | Code examples before/after ||
|#

### Commit formatting

For detailed commit formatting requirements, see the section [**Making changes to the project**](./contribution.md).

## Requirements for Extensions {#extension-requirements}

### Using a template

When creating a new extension, use the official template from the [package-template](https://github.com/diplodoc-platform/package-template) repository.

### Consideration of multithreading

Documentation builds can run in multithreaded mode. Make sure your extension:

- does not use global state;
- works correctly when executed in parallel;
- does not create race conditions.

## Module infrastructure {#infrastructure}

### @diplodoc/lint

Use `@diplodoc/lint` for a unified linting infrastructure:

```bash
# Initializing a new package
npx @diplodoc/lint init

# Updating an existing package
npx @diplodoc/lint update
```

### Scripts in package.json

Define the following scripts in `package.json`:

#|
|| **Script** | **Purpose** ||
|| `build` | Full package build ||
|| `build:js` | JavaScript build (esbuild) ||
|| `build:declarations` | Generate TypeScript declarations ||
|| `typecheck` | Type check: `tsc --noEmit` ||
|| `test` | Run tests: `vitest run` ||
|| `test:watch` | Run tests in watch mode ||
|| `lint` | Code check: `lint update && lint` ||
|| `lint:fix` | Fix errors: `lint update && lint fix` ||
|| `prepublishOnly` | Pre-publish checks ||
|#

{% note tip %}

Use the `test:watch` script during development. It runs tests in watch mode and automatically restarts them when files are saved. This allows you to quickly verify code behavior without manually restarting.

{% endnote %}

### Watch mode

The `npm run watch` command starts the development environment: it builds packages, watches for changes, and automatically restarts the build. This lets you see the result of changes immediately without manually running build commands.

[More on GitHub](https://github.com/diplodoc-platform/diplodoc/blob/master/.agents/monorepo.md#watch-mode)

### Module files

Add to each module:

- `SECURITY.md` — security policy
- `CONTRIBUTING.md` — contributor guide
- `LICENSE` — project license
- `vitest.config.mjs` — Vitest configuration
- `.github/workflows/` — CI/CD workflows

### GitHub Workflows

Each package must contain standard workflows in the `.github/workflows/` directory.

Required workflows:

- `tests.yml` — main testing workflow (runs lint, typecheck, tests)
- `release.yml` — release workflow
- `release-please.yml` — release-please configuration
- `package-lock.yml` — package lock update
- `security.yml` — security scanning
- `update-deps.yml` — dependency update

Special workflows (keep if needed):

- E2E-specific workflows (e.g., `diplodoc-e2e-tests.yaml`)
- Custom workflows for package-specific needs

Workflows to remove (duplicates):

- `tests.yaml` (duplicate of `tests.yml`)

When configuring workflows:

1. Check existing workflows in `.github/workflows/`.
1. Remove duplicate workflows (`.yaml` vs `.yml`).
1. Make sure all standard workflows are present.
1. Keep special workflows if they perform a specific function.
1. Verify the correctness of workflow configuration.

[More in the documentation](https://github.com/diplodoc-platform/diplodoc/blob/master/.agents/dev-infrastructure.md#github-workflows)

## Unsupported tools {#unsupported}

Tools and packages that are not supported in the project. Use the recommended alternatives.

**Build**

- Webpack → use esbuild
- tsc for building JS → use esbuild, tsc only for declarations

**Deprecated packages**

- `@diplodoc/eslint-config → use @diplodoc/lint`
- `@diplodoc/prettier-config → use @diplodoc/lint`

## Checklist before submitting a PR {#checklist}

Before submitting a pull request, check:

- The code follows the project style (`npm run lint` passes without errors).
- Types are checked (`npm run typecheck` passes without errors).
- Tests are written and pass (`npm run test` passes without errors).
- The build works (`npm run build` passes without errors).
- The pull request contains a description of the changes.
- An ADR has been created for architectural changes.
- Screenshots have been added for visual changes.
- Commits follow [conventional commits](https://www.conventionalcommits.org/).
- Only supported tools are used (Vitest, esbuild).

## Additional resources

- [Requirements for contributing to the metapackage](https://github.com/diplodoc-platform/diplodoc/blob/master/.agents/metapackage-requirements.md)
- [Managing metapackages](https://github.com/diplodoc-platform/diplodoc/blob/master/.agents/monorepo.md)
- [Development infrastructure](https://github.com/diplodoc-platform/diplodoc/blob/master/.agents/dev-infrastructure.md)

[*adr]: Architecture Decision Records
