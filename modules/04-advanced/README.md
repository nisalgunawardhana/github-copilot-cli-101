# Module 04 — Custom Instructions and Agents

**Estimated time:** 45–60 minutes

In this final module, you will learn how to customise GitHub Copilot's behaviour for your projects using instruction files and custom agents. These features let you give Copilot persistent context so it produces more relevant, project-specific responses.

---

![Hiring Specialists Analogy](./images/hiring-specialists-analogy.png)

## Why Custom Instructions Matter

By default, Copilot CLI treats every session as a fresh start. It does not know your project's conventions, your preferred coding style, or the constraints you work within.

Custom instruction files solve this by letting you describe your project and preferences once. Every time Copilot is used in that project, it reads these instructions and factors them into its responses.

This is the difference between a generic response and one that actually fits your codebase.

---

## The AGENTS.md File

An `AGENTS.md` file placed at the root of your project tells Copilot important information about how to behave in that context.

### Creating an AGENTS.md file

Create the file at the root of your project:
```bash
touch AGENTS.md
```

### What to include

A well-written `AGENTS.md` should answer:
- What is this project?
- What language and framework does it use?
- What are the coding conventions?
- What should Copilot avoid or prioritise?

### Example AGENTS.md

```markdown
# Project Instructions for Copilot

## Project Overview
This is a REST API built with Python and FastAPI. The database layer uses SQLAlchemy with PostgreSQL.

## Coding Conventions
- Use Python 3.11 type hints on all function signatures
- Follow PEP 8 formatting (enforced by Black)
- All database queries must go through the repository layer — do not call the database directly from route handlers
- Prefer explicit error handling over bare except clauses

## Testing
- Use pytest for all tests
- Tests live in the `tests/` directory, mirroring the `src/` structure
- All new features require at least one happy path and one failure path test

## What to Avoid
- Do not suggest print statements for logging — use the `logger` object from `src/utils/logging.py`
- Do not suggest synchronous database calls — all DB operations must be async
```

---

## Custom Agents


A custom agent is a more specialised version of `AGENTS.md`. Where `AGENTS.md` applies to the whole project, a custom agent is a focused instruction set for a specific task.

You create a custom agent by writing an `.agent.md` file that defines what the agent does, what it knows, and how it should respond.

### When to create a custom agent

Create a custom agent when you repeatedly give Copilot the same setup information before asking a question. Common use cases:

- A code reviewer specialised in your team's style guide
- A test writer that knows your testing conventions and frameworks
- A documentation writer that knows your documentation format

### Example: A test writer agent

Create a file called `pytest-writer.agent.md`:

```markdown
# pytest-writer

## Role
You help write pytest unit tests for Python functions.

## Conventions
- Use descriptive test function names that explain what is being tested
- Group related tests in classes prefixed with `Test`
- Use pytest fixtures for shared setup, not setUp methods
- Include a docstring in each test explaining the expected behaviour
- Mark tests that hit the database with `@pytest.mark.integration`

## Format
When generating tests, output the full test file content ready to paste.
Include an import block at the top, any required fixtures, and all test functions.
```

To use this agent, reference it when making a request:
```bash
gh copilot suggest --agent pytest-writer "write tests for a function that validates email addresses"
```

Here is what using a custom agent looks like in practice:

![Python Reviewer Demo](./images/python-reviewer-demo.gif)

---

## Deciding Where to Place Instructions

The decision tree below helps you figure out whether a given instruction belongs in `AGENTS.md`, a custom agent file, or inline in your prompt.

![Agent File Placement Decision Tree](./images/agent-file-placement-decision-tree.png)

---

## Project-Level vs Task-Level Instructions

Understanding when to use each:

| Type | File | Scope | When to use |
|---|---|---|---|
| Project instructions | `AGENTS.md` | Whole project | Coding style, architecture rules, what to avoid |
| Custom agent | `*.agent.md` | Specific task type | Repeated tasks with specific requirements |
| Inline context | Your prompt | Single request | One-off context that varies per request |

For most projects, a well-written `AGENTS.md` is enough to improve response quality significantly. Custom agents are worth adding when you find yourself typing the same setup text repeatedly.

---

## Writing Effective Instructions

### Be specific, not generic

Generic instruction:
```
Write clean code.
```

Specific instruction:
```
Functions should be no longer than 20 lines. If a function is longer, split it into smaller private functions.
```

### Describe what not to do

Copilot benefits from knowing what to avoid, not just what to do:
```
Do not suggest external libraries that are not already in requirements.txt.
Do not generate code that requires changes to the database schema.
```

### Include examples

If your team has conventions that are hard to describe in words, include a short example:
```
Use this logging pattern:
    logger.info("Processing request", extra={"user_id": user_id, "action": "process"})

Not this:
    print(f"Processing request for user {user_id}")
```

---

## Reviewing Your Setup

Once you have an `AGENTS.md` in place, test it by asking Copilot something that would normally require you to provide that context manually. Compare the response to what you would have gotten without the instructions.

If the response still lacks context, your `AGENTS.md` might need more detail in the relevant section.

---

## Exercises

**Exercise 4.1**
Create an `AGENTS.md` file for a real or practice project. Include at minimum:
- A one-paragraph project overview
- Two coding conventions
- One thing Copilot should avoid

**Exercise 4.2**
Write a simple custom agent for one of these tasks:
- A commit message writer that follows conventional commits format
- A code reviewer focused on performance
- A documentation writer for your preferred format

Test the agent with one request and compare the output to what you get without the agent.

**Exercise 4.3 — Reflection**
After completing all four modules, write 2–3 sentences answering:
- Which workflow from Module 03 was most useful to you, and why?
- What would you add to your `AGENTS.md` after using Copilot for a week?

Keep these notes — the reflection question is part of your submission.

---

## Summary

In this module you:
- Understood why custom instructions improve response quality
- Created an `AGENTS.md` file with project-level context
- Learned how to write custom agents for repeated tasks
- Practised writing specific, actionable instructions

---

## You Have Completed the Course

You have worked through all four modules of GitHub Copilot CLI 101. The next step is to complete your submission and earn your completion badge.

Return to the [main README](../../README.md#submission-task) for submission instructions.
