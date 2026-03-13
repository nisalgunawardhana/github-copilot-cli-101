# Module 03 — Development Workflows

**Estimated time:** 60–90 minutes


This module covers practical, real-world workflows where GitHub Copilot CLI saves time and reduces friction. Each section focuses on a specific task developers do regularly: reviewing code, debugging, writing tests, and working with Git.


---

## Workflow 1 — Code Review from the Terminal

![Code Review Swimlane](./images/code-review-swimlane-single.png)

When you want a quick review of a file or function before committing, you can pass code directly to Copilot for feedback.

### Reviewing a file

Use `cat` to pipe a file into Copilot's explain command:
```bash
cat auth.py | gh copilot explain
```

Or use a targeted suggest prompt:
```bash
gh copilot suggest "review this Python function for potential security issues: $(cat auth.py)"
```

### What to look for in a code review

When asking Copilot to review code, be specific about what you care about:

- **Security:** `"Are there any security vulnerabilities in this function?"`
- **Performance:** `"Could this query be written more efficiently?"`
- **Readability:** `"How could this function be made easier to understand?"`
- **Correctness:** `"Does this function handle edge cases correctly?"`

A vague prompt like "review this code" will produce a general response. Targeted questions produce more actionable feedback.

![Code Review Demo](./images/code-review-demo.gif)

---

## Workflow 2 — Debugging

![Debugging Swimlane](./images/debugging-swimlane-single.png)

When you have an error or unexpected behavior, Copilot CLI can help you think through the problem.

### Sharing an error message

```bash
gh copilot suggest "I'm getting this Python error: ModuleNotFoundError: No module named 'requests'. I have Python 3.11 installed and I'm running the script with python3."
```

### Explaining a stack trace

If you have a stack trace, describe it or paste the key lines:
```bash
gh copilot explain "ValueError: invalid literal for int() with base 10: '' at line 42 of my data parser"
```

### Debugging a bash script

When a shell script fails silently or produces unexpected output:
```bash
gh copilot suggest "my bash script runs without errors but the output file is empty. I'm using cat file.txt > output.txt in a loop."
```

### Debugging approach

Use Copilot CLI as a thinking partner, not just an answer machine. Ask it to:
1. Explain what the error means
2. List possible causes
3. Suggest which cause is most likely given your situation
4. Propose a fix

This step-by-step approach gives you better results than asking for a direct fix.

![Fix Bug Demo](./images/fix-bug-demo.gif)

---

## Workflow 3 — Writing Tests

![Test Generation Swimlane](./images/test-gen-swimlane-single.png)

Generating test cases is one of the most time-saving uses of Copilot CLI.

### Generating unit tests

Describe the function you want to test:
```bash
gh copilot suggest "write pytest unit tests for a Python function called calculate_discount(price, discount_percent) that returns the discounted price. Test normal cases, zero discount, and 100% discount."
```

### Identifying missing test cases

```bash
gh copilot suggest "what edge cases am I missing in tests for a function that parses dates from strings in multiple formats?"
```

### Generating test data

```bash
gh copilot suggest "generate 5 sample JSON objects for testing a user registration API. Include valid cases and one case with a missing required field."
```

### Integration test setup

```bash
gh copilot suggest "what do I need to set up to run integration tests for a Flask app that connects to a PostgreSQL database?"
```

![Test Generation Demo](./images/test-gen-demo.gif)

---

## Workflow 4 — Git Integration

![Git Integration Swimlane](./images/git-integration-swimlane-single.png)

Copilot CLI works well alongside Git to reduce the time spent on common operations.

### Writing commit messages

Instead of struggling to write a clear commit message, describe what you changed:
```bash
gh copilot suggest "write a commit message for changes that refactor the user authentication module to use JWT instead of session cookies, and add refresh token support"
```

The output will follow conventional commit format if you ask:
```bash
gh copilot suggest "write a conventional commit message for: added input validation to the registration form to prevent SQL injection"
```

### Writing pull request descriptions

```bash
gh copilot suggest "write a pull request description for changes that: added pagination to the products API endpoint, set default page size to 20, added page and per_page query parameters"
```

### Understanding a diff

When reviewing a large diff you are unfamiliar with:
```bash
gh copilot explain "$(git diff HEAD~1)"
```

### Finding the right Git command

```bash
gh copilot suggest "cherry-pick a commit from another branch without committing it yet"
gh copilot suggest "see all commits that touched a specific file"
gh copilot suggest "set up git to use my SSH key for a specific remote"
```

![Git Integration Demo](./images/git-integration-demo.gif)

---

## Workflow 5 — Working with Scripts and Automation

![Refactoring Swimlane](./images/refactoring-swimlane-single.png)

Copilot CLI helps you write automation scripts for repetitive tasks.

### Creating a deployment script

```bash
gh copilot suggest "write a bash script that pulls the latest changes from git, installs npm dependencies, builds the project, and restarts a systemd service called myapp"
```

### Automating file processing

```bash
gh copilot suggest "write a Python script that reads all CSV files in a directory, merges them into one file, and removes duplicate rows based on an ID column"
```

### Setting up cron jobs

```bash
gh copilot suggest "write a cron expression and the corresponding bash command to run a backup script every day at 2am and log the output to a file"
```

---

## How These Workflows Connect

![Specialized Workflows](./images/specialized-workflows.png)

Each workflow follows a similar pattern: describe the problem or task clearly, let Copilot generate a starting point, then refine based on what you actually need.

![Workflow Steps](./images/carpenter-workflow-steps.png)

The swimlane diagram below shows how the five workflows relate to each other and when to use each one.

![Workflows Swimlane](./images/five-workflows-swimlane.png)

---

## Exercise — Complete a Full Workflow

Choose one of the following scenarios and work through it using Copilot CLI. Take a screenshot of the most useful Copilot response you receive — you will need this for your submission.

**Scenario A — Debugging**
Find a real error message from a project you are working on (or use a common one like a pip installation failure). Use Copilot CLI to diagnose it and propose a fix.

**Scenario B — Test Generation**
Pick any function you have written recently. Use Copilot CLI to generate unit tests for it. Note how many edge cases it identifies that you had not thought of.

**Scenario C — Git Workflow**
Use Copilot CLI to write a commit message for your most recent commit, or to understand a complex `git log` or `git diff` output.

**Scenario D — Automation**
Describe a repetitive task you do manually. Use Copilot CLI to generate a script that automates it.

---

## Summary

In this module you:
- Used Copilot CLI to review code for specific concerns
- Approached debugging as a step-by-step conversation with Copilot
- Generated unit tests and identified edge cases
- Used Copilot to improve your Git workflow
- Practised writing automation scripts

Continue to [Module 04 — Custom Instructions and Agents](../04-advanced/README.md).
