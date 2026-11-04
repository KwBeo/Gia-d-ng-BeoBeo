# HomeEase — Agent Instructions

## Project Overview

- **Project:** HomeEase, a university software engineering project.
- **Purpose:** Household goods e-commerce website.
- **Frontend:** Next.js with TypeScript.
- **Backend:** Python with Flask.
- **Database:** PostgreSQL.
- **Payment:** Cash on Delivery (COD).
- **User-facing language:** Vietnamese.
- **UI:** Modern and responsive.

Treat these details as the intended project direction. Inspect the repository before assuming a feature, framework, or architectural layer is already implemented.

## Repository and Change Safety

- Inspect the relevant files, project structure, and Git status before making changes.
- Do not delete or overwrite an existing file without first explaining why and obtaining approval.
- Never make changes directly on the `main` branch. Before editing, check the current branch; if it is `main`, stop and ask to move to an appropriate working branch.
- Use these branch naming conventions:
  - `feature/<feature-name>` for features
  - `fix/<bug-name>` for bug fixes
  - `docs/<document-name>` for documentation
- Do not commit or push unless explicitly requested.
- Keep changes focused on the request. Do not create application source code unless requested.

## Architecture and Implementation

- Use clean architecture and keep frontend, backend, and database responsibilities separate.
- Prefer modular, cohesive code that follows existing project conventions.
- Add appropriate input validation and error handling at system boundaries.
- Write maintainable code and document non-obvious decisions or behavior.
- Keep user-facing text in Vietnamese, consistent with the product requirements.
- Implement payment as Cash on Delivery unless the user explicitly changes this requirement.

## Configuration and Security

- Never hardcode passwords, API keys, tokens, or other secrets.
- Use environment variables for configuration and provide `.env.example` templates when environment configuration is needed.
- Do not put real credentials or secret values in `.env.example`; use safe placeholders and explain required variables.
- Validate and handle untrusted input appropriately.

## Planning and Approval

- For major changes, present a concise plan and wait for approval before implementation.
- Ask for clarification when requirements or consequential design choices are ambiguous.
- Do not treat this instruction as approval to expand the requested scope.

## Verification and Reporting

- Run relevant tests or checks after making code changes; choose the smallest existing commands that cover the change.
- Do not claim a feature or change works unless it has been tested. Clearly state what was and was not verified.
- Explain every important file created or modified and summarize the change.
- If tests cannot be run, state the reason and any remaining validation needed.
