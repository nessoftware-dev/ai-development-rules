# AI Development Rules

Project-specific rules for using AI assistants during software development.

## Why these rules exist

AI assistants are useful development partners, but they may not automatically know all of a project's conventions. For example, they may:
- Create a new helper when an existing one could be reused.
- Suggest a different pattern from the one already used in the project.
- Apply styling or naming conventions inconsistently.
- Make assumptions about package APIs or dependency versions.
- Modify more code than is necessary for the requested change.

These rules make the expected project conventions explicit so that AI-generated code fits the codebase instead of gradually making it more inconsistent.

The rules were developed through extensive discussions with multiple AI assistants about how to make AI-generated code more consistent, focused, and aligned with an existing project.
These discussions showed that AI assistants can sometimes miss project-specific conventions, repeat functionality that already exists, or choose a different implementation style. This is understandable because an AI assistant usually has only limited knowledge of a project's history, design decisions, and preferred patterns.
The rules provide that additional context and help the assistant make changes that fit naturally into the existing codebase.

## Why the rules are strict

The rules are intentionally stronger than general-purpose coding guidelines. General advice such as “follow best practices” is often too vague for an AI assistant and may result in several different interpretations.

Strict rules:

- Reduce the number of decisions the AI must make.
- Prevent the introduction of competing patterns.
- Protect existing architecture and project conventions.
- Make generated code more predictable and reviewable.
- Require confirmation before potentially destructive changes.
- Prefer reuse over duplication.
- Encourage small, focused changes.

These rules are not intended to replace developer judgment. They define safe defaults for AI-assisted changes. Explicit developer instructions always take priority.

## Available rules

- [Flutter development rules](flutter/rules.md)

## How to use the rules

Provide the relevant rules file to your AI coding assistant as project instructions or custom instructions.

Use only the rules relevant to the project or technology being developed. The rules should be committed together with the project so they can be reviewed and updated like source code.

When adding new rules, prefer specific and verifiable instructions over vague guidance. For example:

```text
Reuse an existing dialog utility instead of creating a new dialog helper.
