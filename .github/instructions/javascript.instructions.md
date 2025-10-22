---
applyTo: "**/*.js, **/*.ts, **/*.jsx, **/*.tsx"
---

# Project General Coding Standards

## Naming Conventions
- Use **camelCase** for variables, functions, and methods.
- Use **camelCase** for filenames except for React components.
- Use **PascalCase** for React component filenames, component names, interfaces, and type aliases.
- Use **kebab-case** for all directory names, package names, and CSS class names.
- Use **UPPER_SNAKE_CASE** for environment variables and constants.
- **Prefix hook functions** with `use` (e.g., `useAuth`, `useUserStore`).

## Formatting Rules
- Use **single quotes** for strings (`'example'`).
- **No semicolons** at the end of statements.
- **No trailing commas** in objects and arrays.
- Indentation should be **2 spaces**.
- Ensure **consistent spacing** around operators and keywords.

## Linting & Formatting
- Enforce these rules with the Deno linter and formatter, using your custom settings.
- Rely on the linter/formatter to enforce import source order and other style rules.

## Best Practices
- Use **ES modules (`import/export`)** instead of CommonJS, **never use `require`**.
- Avoid **non-null assertions (`!`)** unless absolutely necessary.
- Prevent **unused variables and parameters** in all scopes.
- Use **const** or **let**; avoid `var`.
- Avoid **mutating function arguments**, especially objects and arrays.
- **Prefer arrow functions**, except when used for exports or default exports.
- Group imports by source: **standard libraries**, then **third-party modules**, then **local files**.
- Minimize function complexity; **keep functions focused and short**.
- Use **destructuring** to access object and array properties where appropriate.
- **Import only what is needed**; avoid wildcard (`*`) imports.
- Avoid **side effects** in shared modules—initialize logic within functions or components.
- **Use type narrowing** where possible instead of type assertions.
- Prefer **named exports** over default exports for utilities and shared modules.

## TypeScript Guidelines
- Use TypeScript for all new code.
- Follow functional programming principles where possible.
- Use interfaces for data structures and type definitions.
- Prefer immutable data (`const`, `readonly`).
- Use optional chaining (`?.`) and nullish coalescing (`??`) operators.
- Prefer **type aliases** for simple shapes and unions.
- Avoid `any`; prefer `unknown` or properly defined types.
- Use literal unions or `const enum` over traditional enums when possible.
- Avoid global type augmentation unless necessary.

## React Guidelines

- Use functional components with hooks.
- Always import types separately using `import type { ... } from 'react'`; never use `React.` for types or elements.
- never use `context.provider` as it is not needed since react 19.
- Always use `ReactNode` for function component return types, and always explicitly type the return value of all React components and hooks.
- Never use `React.FC`, `React.FunctionComponent`, or `React.ReactNode` via the `React.` namespace.
- Follow the React hooks rules (no conditional hooks).
- Use `export default function` for components.
- Use `useEffect` for side effects and cleanup.
- Keep components small and focused.
- Use `useMemo` and `useCallback` for performance optimization when needed.
- Group hooks at the top of components before logic.
- Create custom hooks for reusable logic, and always use named exports for hooks/utilities.
- Use descriptive prop names instead of generic ones like `data` or `item`.
- Use `key` props when rendering lists to avoid re-renders.
- Use TypeScript interfaces for prop validation.
- Prefer destructuring with defaults in the function parameter list for default props.
- Do not use inline anonymous functions in JSX; define handlers/callbacks outside of JSX.
- Do not use legacy lifecycle methods; use hooks for all side effects and state.