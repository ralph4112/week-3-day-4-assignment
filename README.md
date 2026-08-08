# Week 3 Day 4 Assignment: Git Workflow

This repository contains the completed Git workflow assignment for Week 3, Day 4. It demonstrates branching, merging, conflict resolution, pull requests, and rebasing.

## Setup

Project folder initialized with:

```bash
mkdir week-3-day-4-assignment
cd week-3-day-4-assignment
git init
```

Two starter files were created:

- `index.html`: Basic HTML structure for the assignment page.
- `styles.css`: Starter CSS with body styles.

AI-generated code in this project includes comments above it explaining what it does.

## Task 1: Branching and Merging (25 points)

### Commits on `main`

1. `48332b6` Add index.html with basic structure
2. `a231551` Add styles.css with body styles
3. `11043e9` Add header section to HTML
4. `b126e41` Add hero section to HTML
5. `46f0b95` Style the header and hero in CSS

### Feature branch `feature/footer`

Created and checked out the branch:

```bash
git checkout -b feature/footer
```

Commits on `feature/footer`:

6. `51287aa` Add footer HTML
7. `dd124d0` Style the footer
8. `12c3f45` Add social media links to footer

### Merge back to `main`

```bash
git checkout main
git merge --no-ff feature/footer -m "Merge feature/footer into main"
```

Using `--no-ff` produced a merge commit so the branch structure is visible in the graph.

### Screenshot placeholder

> TODO: Replace this section with a screenshot of `git log --oneline --graph --all` showing all 8 feature commits plus the merge commit.

Expected graph:

```text
*   30fbf3a Merge feature/footer into main
|\
| * 12c3f45 Add social media links to footer
| * dd124d0 Style the footer
| * 51287aa Add footer HTML
|/
* 46f0b95 Style the header and hero in CSS
* b126e41 Add hero section to HTML
* 11043e9 Add header section to HTML
* a231551 Add styles.css with body styles
* 48332b6 Add index.html with basic structure
```

## Task 2: Merge Conflict Resolution (25 points)

Two branches were created from `main` and edited the same line in `styles.css`.

### Branch `feature/nav-v1`

```bash
git checkout -b feature/nav-v1
```

Changed `styles.css` line 1 to:

```css
body { background: #f0f0f0; }
```

Commit: `bfd841d` Set light gray background in styles.css

### Branch `feature/nav-v2`

```bash
git checkout main
git checkout -b feature/nav-v2
```

Changed `styles.css` line 1 to:

```css
body { background: #1a1a2e; }
```

Commit: `9b21465` Set dark navy background in styles.css

### Merge `feature/nav-v1` into `main`

```bash
git checkout main
git merge feature/nav-v1
```

This merge succeeded with a fast-forward.

### Merge `feature/nav-v2` into `main` — conflict

```bash
git merge feature/nav-v2
```

Output:

```text
Auto-merging styles.css
CONFLICT (content): Merge conflict in styles.css
Automatic merge failed; fix conflicts and then commit the result.
```

### Conflict markers in the file

Screenshot placeholder: insert the screenshot of `styles.css` containing the conflict markers here.

Text version of the conflict:

```css
<<<<<<< HEAD
body { background: #f0f0f0; }
=======
body { background: #1a1a2e; }
>>>>>>> feature/nav-v2
```

### Resolved file

I chose the dark navy background and removed all conflict markers.

Screenshot placeholder: insert the screenshot of the resolved `styles.css` here.

Final content:

```css
/* This stylesheet sets the page background color that was chosen during the merge conflict resolution exercise. */
body { background: #1a1a2e; }
```

Resolution commit:

```bash
git add styles.css
git commit -m "Resolve merge conflict: keep dark navy background"
```

Commit: `3dd0342` Resolve merge conflict: keep dark navy background

### Final merge graph

Screenshot placeholder: insert the screenshot of `git log --oneline --graph --all` after the conflict resolution here.

Text version of the graph around the conflict resolution:

```text
*   3dd0342 Resolve merge conflict: keep dark navy background
|\
| * 9b21465 Set dark navy background in styles.css
* | bfd841d Set light gray background in styles.css
|/
*   30fbf3a Merge feature/footer into main
```

## Task 3: Collaborative Workflow (20 points)

This task requires a GitHub account and a fork of a public repository. I documented the workflow below. The actual fork and pull request must be created on GitHub because this environment cannot authenticate to GitHub without a personal access token or SSH key.

### Steps to complete

1. Fork a classmate's repository on GitHub, or use a simple public repo such as `first-contributions/first-contributions` or `freeCodeCamp/freeCodeCamp`.
2. Clone your fork (replace `YOUR-USERNAME` and `REPO`):

```bash
git clone https://github.com/YOUR-USERNAME/REPO.git
cd REPO
```

3. Create a new branch:

```bash
git checkout -b feature/your-name-contribution
```

4. Make a meaningful change, for example add a small documentation fix or a new example file. Add comments above any AI-generated code.

5. Commit with a clear message:

```bash
git add .
git commit -m "Add a clear description of your contribution"
```

6. Push the branch to your fork:

```bash
git push origin feature/your-name-contribution
```

7. Open a Pull Request on GitHub with:
   - A descriptive title
   - A description explaining what you changed and why
   - A screenshot of the change (if visual)

### Screenshot placeholder

> TODO: Insert a screenshot of the open Pull Request on GitHub here. The screenshot should show the PR title, description, and changed files.

### Link to open Pull Request

> TODO: Replace with the actual PR link, e.g. `https://github.com/OWNER/REPO/pull/123`

## Bonus Challenge: Rebase vs. Merge (+10 points)

### Rebase scenario

1. Created a new branch from `main` and made 3 commits:

```bash
git checkout -b feature/rebase-demo
```

Commits:

- `16780d1` Rebase demo: add initial feature file
- `e3b70af` Rebase demo: add second capability
- `8506e63` Rebase demo: finalize feature

2. Meanwhile, 2 more commits were made on `main`:

- `cf29835` Main update 1: add progress file
- `f36a44a` Main update 2: continue development

3. Rebased the feature branch onto `main`:

```bash
git checkout feature/rebase-demo
git rebase main
```

4. The feature branch was then merged into `main` with `--no-ff` to keep the demo visible.

### Graph comparison

#### Merge graph (from Task 1 — `feature/footer`)

```text
*   30fbf3a Merge feature/footer into main
|\
| * 12c3f45 Add social media links to footer
| * dd124d0 Style the footer
| * 51287aa Add footer HTML
|/
* 46f0b95 Style the header and hero in CSS
```

A merge keeps the original commit hashes and shows the exact branch history, including the merge commit.

#### Rebase graph (bonus — `feature/rebase-demo`)

```text
* 8506e63 Rebase demo: finalize feature
* e3b70af Rebase demo: add second capability
* 16780d1 Rebase demo: add initial feature file
* f36a44a Main update 2: continue development
* cf29835 Main update 1: add progress file
```

After rebase, the feature commits are replayed on top of `main`, producing a linear history. The original feature branch commit hashes are replaced with new ones.

### When to use rebase vs. merge

Use **merge** when you want to preserve the exact history of a feature branch, including when it was created and when it was integrated. Merge is safer for shared branches because it does not rewrite commit hashes, so collaborators do not have to force-pull rewritten history.

Use **rebase** when you want a clean, linear history before merging a feature branch. It is useful for cleaning up local commits or updating a feature branch against the latest `main` before opening a pull request. The tradeoff is that rebase rewrites commit hashes, which can cause confusion if the branch has already been shared with other people. Never rebase commits that have already been pushed to a shared branch.

## Final repository graph

```text
*   1694c3a Integrate rebase demo feature into main
|\
| * 3bf6812 Add explanatory comments to AI-generated code and demo files
| * 8506e63 Rebase demo: finalize feature
| * e3b70af Rebase demo: add second capability
| * 16780d1 Rebase demo: add initial feature file
|/
* f36a44a Main update 2: continue development
* cf29835 Main update 1: add progress file
*   3dd0342 Resolve merge conflict: keep dark navy background
|\
| * 9b21465 Set dark navy background in styles.css
* | bfd841d Set light gray background in styles.css
|/
*   30fbf3a Merge feature/footer into main
|\
| * 12c3f45 Add social media links to footer
| * dd124d0 Style the footer
| * 51287aa Add footer HTML
|/
* 46f0b95 Style the header and hero in CSS
* b126e41 Add hero section to HTML
* 11043e9 Add header section to HTML
* a231551 Add styles.css with body styles
* 48332b6 Add index.html with basic structure
```

## Submission checklist

- [ ] Repository pushed to GitHub as `week-3-day-4-assignment`
- [ ] README includes all required screenshots
- [ ] Task 3 Pull Request link added to README
- [ ] Link shared on Discord #assignments channel
