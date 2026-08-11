# Making changes to the project

## Main process

Several people are involved in the process of making changes to a module:

- **Contributor** — directly makes the changes.
- **Maintainer** — is responsible for the quality of the module — reviews the changes and releases a new version of the package.

## Commit formatting

**The **Contributor must consider the following requirements when formatting commits:

- **The commit name must comply with [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/).** Allowed prefixes: `chore:`, `fix:`, `feat:`, `deps:`, `fixup!`.
- **A commit must contain complete functionality.** The module must remain in a working state within each commit (not just within the entire pull request).
- **A commit must contain a single functionality.** If a pull request modifies multiple functionalities, they must be split into separate commits.
- When fixing comments on a pull request, the **contributor** creates additional commits with the prefix `fixup!` and the sha of the commit being fixed.

## Pull request formatting 

**The **Contributor must consider the following requirements when formatting a pull request:

- **The pull request name must reflect the essence of the changes being made.** If the pull request consists of a single commit, the pull request name is the commit name without the conventional prefix. 
- The pull request contains an additional explanation of the changes being made.
  - In the case of fixing a bug — a link to the corresponding issue or a description of the bug.
  - In the case of adding functionality — a description of the functionality, a link to the related commit in the documentation.
  - In the case of visual changes — a screenshot or video before/after.
- After the **maintainer** accepts the pull request, if commits with the prefix `fixup!` were created, a manual rebase with the flag `--autosquash` must be performed to merge the fixes into the original commits.