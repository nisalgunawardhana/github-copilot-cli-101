# Module 02 — Core Commands and Context

**Estimated time:** 45–60 minutes

In this module, you will go deeper into the commands available in GitHub Copilot CLI. You will learn how to work with shell commands, scripts, and Git operations, and how to give Copilot enough context to get useful responses.

---

## Understanding Context

![Colleague Context Analogy](./images/colleague-context-analogy.png)

One of the most important ideas when working with any AI assistant is context — the information the tool has available when generating a response.

GitHub Copilot CLI works within your terminal session. It does not automatically read your project files unless you provide them explicitly. The quality of suggestions you receive depends heavily on how clearly you describe your situation.

**Less useful prompt:**
```
How do I fix the error?
```

**More useful prompt:**
```
I'm getting a "permission denied" error when running my Python script on Ubuntu. The file is executable but I'm running it as a normal user.
```

Be specific about your operating system, the tool or language you are using, and any constraints you have.

![Codebase Understanding](./images/codebase-understanding.png)

---

## The `explain` Command in Depth

`gh copilot explain` accepts any shell command as input and returns a plain-language breakdown.

### Explaining a single command

```bash
gh copilot explain "chmod 755 script.sh"
```

### Explaining a piped command

```bash
gh copilot explain "find . -name '*.py' | xargs grep -l 'import os'"
```

### Explaining a flag you do not recognise

If you see a command in documentation with unfamiliar flags, paste the whole thing:
```bash
gh copilot explain "curl -fsSL https://example.com/install.sh | bash"
```

Copilot will break down each component, which helps you understand what you are running before executing it.

Here is what referencing a file in your context looks like:

![File Context Demo](./images/file-context-demo.gif)

---

## The `suggest` Command in Depth

`gh copilot suggest` generates shell commands from natural language descriptions.

### General shell tasks

```bash
gh copilot suggest "compress the images folder into a zip file excluding hidden files"
```

### Git operations

```bash
gh copilot suggest "undo the last commit but keep the changes staged"
```

### File operations

```bash
gh copilot suggest "rename all .txt files in the current directory to .md"
```

### System administration

```bash
gh copilot suggest "show which process is using port 3000"
```

After Copilot suggests a command, you can:
- **Run it directly** by copying and pasting
- **Ask for a variation** by describing what is different about your situation
- **Ask for an explanation** of the suggested command before running it

---

## Chaining Explain and Suggest

A practical workflow is to use `suggest` to get a command and then immediately use `explain` to understand it before running it.

For example:
```bash
gh copilot suggest "delete all Docker containers that are stopped"
# Copilot suggests: docker rm $(docker ps -aq -f status=exited)

gh copilot explain "docker rm $(docker ps -aq -f status=exited)"
# Copilot explains what each part does
```

This gives you confidence that the command does what you expect.

![Multi-Turn Demo](./images/multi-turn-demo.gif)

---

## Working with Git

Copilot CLI is particularly useful for Git workflows where you need to remember the exact syntax for less common operations.

**Writing commit messages:**
```bash
gh copilot suggest "write a commit message for changes that add user authentication using JWT tokens"
```

**Undoing mistakes:**
```bash
gh copilot suggest "I accidentally pushed to main, how do I revert the last push"
```

**Branch operations:**
```bash
gh copilot suggest "create a new branch from a specific commit hash"
```

**Rebasing:**
```bash
gh copilot explain "git rebase -i HEAD~3"
```

---

## Sessions and Persistence

![Session Persistence Timeline](./images/session-persistence-timeline.png)

By default, each `gh copilot` command starts a fresh session with no memory of previous requests. If you are working through a multi-step problem, include the relevant context in each prompt.

For example, if you asked Copilot to suggest a deployment script in one command and now want to extend it, include a brief description of what the script already does in your next prompt rather than assuming Copilot remembers it.

---

## Cross-File Intelligence

When working on a project, you may need Copilot to understand how multiple files relate to each other.


You can provide this context manually by describing the structure in your prompt:
```bash
gh copilot suggest "I have a Flask app where routes.py handles HTTP requests and services.py contains the business logic. In services.py, how should I structure a function that validates user input before saving to the database?"
```

---

## Writing Shell Scripts

You can use Copilot CLI to help write and understand shell scripts.

**Generating a script:**
```bash
gh copilot suggest "write a bash script that backs up the current directory to a timestamped folder"
```

**Explaining an existing script:**
If you have a script you inherited or downloaded, use `explain` to understand what it does before running it:
```bash
gh copilot explain "$(cat deploy.sh)"
```

> Note: Be cautious about passing long or sensitive scripts directly into the explain command. Review the content first and redact any credentials or tokens.

---

## Providing Better Prompts


Here are patterns that consistently produce better results:

| Pattern | Example |
|---|---|
| State your OS or environment | "On Ubuntu 22.04, ..." |
| Include the language or tool | "Using Python 3.11, ..." |
| Describe the goal, not just the error | "I want to X, but I'm seeing Y" |
| Give constraints | "without installing additional packages" |
| Specify output format | "output as a single command I can copy and run" |

---

## Exercises

**Exercise 2.1**
Use `gh copilot explain` on a command you have never used or that you find confusing. Write a one-sentence summary of what you learned.

**Exercise 2.2**
Use `gh copilot suggest` to get a Git command for one of the following tasks (your choice):
- Squash the last 3 commits into one
- Show a visual graph of the commit history
- Find which commit introduced a specific line of code

Run the command on a test repository.

**Exercise 2.3**
Try chaining `suggest` and `explain`. Get a command suggestion for any task, then use `explain` on the output. Notice whether the explanation changes how confident you are about running it.

---

## Summary

In this module you:
- Learned how context affects the quality of responses
- Used `explain` to understand commands in depth
- Used `suggest` for shell tasks, Git operations, and scripting
- Understood how sessions work and how to provide multi-file context
- Practised writing more specific prompts

Continue to [Module 03 — Development Workflows](../03-workflows/README.md).
