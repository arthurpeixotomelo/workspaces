---
applyTo: "**"
---

# General Model Instructions (Strict Agent Mode)

## Pre-Action Checklist

Before any action, the agent must confirm and log (use `(x)` for checked, `( )` for unchecked):

- ( ) Architecture/implementation plan **or relevant instruction file** found and used
- ( ) All relevant instruction files referenced and applied
- ( ) All required documentation for libraries incorporated
- ( ) "Planner" chatmode used for all planning/analysis steps

If any item is unchecked, **halt and prompt the user** for the missing prerequisite.

---

## 1. Architecture/Implementation Plan & Guidelines Precedence

- **Always search for a software architecture or implementation plan** in the current repository (README, `.md` files, or designated planning docs) before any code generation.
- **Definition of Plan/Guideline:**  
  For routine refactors, code style, or best-practice improvements, the presence of a relevant instruction file (e.g., `.github/instructions/css.instructions.md`, `.github/instructions/markdown.instructions.md`, or language/framework-specific guides) is sufficient and should be treated as the guiding plan.  
  Only block and require a new architecture/implementation plan if the request involves a new feature, major system change, or if no relevant guideline exists.
- **If a plan or relevant instruction file exists:**  
  - Use it as the *primary and binding* guide for all implementation and code generation.
  - Reference and follow all additional instructions (e.g., `.github/instructions/markdown.instructions.md`, language/framework-specific guides) relevant to the context, file type, or language.  
  - If multiple instruction files are relevant (e.g., for web projects involving HTML, CSS, JS, frameworks), apply all of them.
- **If no plan or relevant instruction file exists:**  
  - **Do not generate code under any circumstances.**  
  - Prompt the user to create or provide an architecture/implementation plan or relevant instruction file using the standard template (see `.github/instructions/markdown.instructions.md`).
  - Only proceed once a plan or relevant instruction file is available.
- **If any planning, requirements analysis, or implementation plan creation is needed:**  
  - **Always switch to or invoke the "Planner" chatmode and follow its process before proceeding.**

---

## 2. Contextual Documentation Search (Library Usage)

- **Use the `contextDocs` toolset only when:**
  - A library is detected in the codebase, mentioned in requirements, or requested for use.
  - You are generating new code or modifying existing code that uses a library.
- **When using a library:**
  - Prefer libraries that already have an `llms.txt` file linked in `llmsTxtDocs` or similar sources.
  - Retrieve and incorporate up-to-date documentation for the relevant library before generating or modifying code.

---

## 3. Summarize Implementation

- Summarize the implementation approach that will be applied, based on the available architecture/plan and any relevant documentation.
- Clearly state how the plan and documentation inform the implementation.
- **Explicitly list all instruction files and documentation used for the current action.**
- **Log the reasoning** for each step, especially when multiple instruction files are combined or when using the "Planner" chatmode.

---

## 4. Code Generation

- Only proceed to code generation after:
  - An architecture/plan **or relevant instruction file** has been found and strictly followed.
  - All relevant documentation for libraries to be used has been incorporated.
  - All relevant instruction files have been referenced and their requirements applied.
  - The "Planner" chatmode has been used for all planning/analysis steps.
- Ensure all generated code aligns with the plan and all referenced instructions.

---

## 5. Reference to Other Instructions

- When working with markdown, documentation, or language-specific files, always reference and comply with all relevant instruction files (e.g., `.github/instructions/markdown.instructions.md`, language/framework-specific guides).
- If in doubt, prompt the user for clarification or for the appropriate instruction file.

---

## Example Summary of Used Instructions/Docs

> **Instruction/Documentation Summary:**  
> - Architecture/Plan: `README.md`
> - Instruction Files: `.github/instructions/markdown.instructions.md`, `.github/instructions/javascript.instructions.md`
> - Library Docs: [Drizzle ORM](https://orm.drizzle.team/llms-full.txt), [Hono](https://hono.dev/llms-full.txt)  
> - Reasoning: Used "Planner" chatmode for requirements analysis and plan; combined markdown and JavaScript instructions due to mixed file context; followed architecture plan for all structural decisions.

> **Example (Routine Refactor):**  
> - Task: Refactor CSS in a component  
> - Architecture/Plan: `.github/instructions/css.instructions.md`  
> - Instruction Files: `.github/instructions/markdown.instructions.md`, `.github/instructions/css.instructions.md`  
> - Reasoning: Used CSS and markdown instructions as the guiding plan for style refactor; no feature-level plan required for this scope.

---

> **Note:**  
> The agent must be strict in enforcing these steps. If any required plan, documentation, or instruction file is missing, halt and prompt the user rather than proceeding.  
> Always output a summary of which instruction files and documentation were used for each action, and provide reasoning for their selection and application.
