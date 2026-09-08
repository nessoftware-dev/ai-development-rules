# AI Rules for Flutter projects

## Project packages
Use the following packages instead of implementing equivalent functionality locally:
- [`result_utils`](https://pub.dev/packages/result_utils)  
  Use for typed success/failure results returned by repositories and services.
- [`dialog_utils`](https://pub.dev/packages/dialog_utils)  
  Use for displaying application dialogs (confirmation, alert, info, error and waiting messages).

When using `result_utils` or `dialog_utils`:
1. Before using either package, verify that the package is available in the project's `pubspec.yaml` and use the version already resolved by `pubspec.lock`.
2. Inspect the package documentation, exports, and existing usages in the codebase.
3. If the package API cannot be inspected, ask before adding new usage.

## Code Consistency (HIGHEST PRIORITY)
**ALWAYS maintain and extend existing code style - NEVER introduce alternative implementations WITHOUT ASKING FIRST.**

When working on the project:
1. Examine existing code patterns and styles in similar files/screens
2. Match the style, structure, and approach of existing code
3. Extend existing patterns rather than creating alternatives
4. Keep uniformity across all files and screens
5. Do NOT mix different implementations for the same problem
6. **ASK BEFORE introducing alternative implementations** (even if they seem better)
7. Prefer consistency over personal preferences

This rule takes precedence over all other optimization or style considerations.

## Code Reuse
**ALWAYS search for and reuse existing utility functions and components before creating new ones.**

Before implementing:
1. Check existing widgets/screens for patterns
2. Use existing dialog functions from `dialog_utils` instead of creating custom dialogs
3. Do not duplicate functionality that already exists in the codebase

## Error Handling with FutureResult (REQUIRED for ALL Service Layers)
**ALWAYS use FutureResult pattern for service layer error handling. NO EXCEPTIONS should ever be thrown.**

Universal error handling standards:
1. **ALL** service functions that can fail must return `Future<FutureResult<T>>` (never `Future<T>`)
2. Use try-catch blocks to capture ANY exception and convert to `FutureResult.error(String)`
3. Return errors as: `FutureResult.error(String)`
4. Return success as: `FutureResult.success(value)`
5. UI layer accesses results via `.hasError`, `.error`, and `.value` properties
6. Number of wrapper functions: ZERO - base functions return FutureResult directly
7. **Wrap ONLY the external function call that throws - NO other code in try-catch**
   - Move all safe transformations, mapping, filtering, sorting OUTSIDE try-catch
   - This clarifies exactly which operation can fail
   - If a transformation throws unexpectedly, that's a visible failure (not silently caught)

## Package Management
**ALWAYS verify current package versions before adding dependencies.**

When adding packages to pubspec.yaml or other dependency files:
1. Search pub.dev for the package using the available package registry or package-search tool
2. Check the LATEST version available
3. Only specify versions that are confirmed to exist
4. Prefer recent stable versions unless requirements dictate otherwise
5. Never guess or use outdated version numbers

## Actions Requiring User Confirmation

### Ask Before:
- **Deleting files** (destructive operations)
- **Accessing files outside this project**
- **Modifying project structure significantly**
- **Overwriting existing files**
- **Creating or storing new rules in memory**
- **Introducing alternative implementations**

## Code Organization in Classes
**ALWAYS organize class members in this order:**

1. Fields/Properties (private variables, controllers, etc.)
2. Override methods (`@override` annotated methods)
   - `initState()`
   - `dispose()`
   - `build()`
   - etc.
3. Helper methods (private functions with `_` prefix)
4. Getter/setter methods

This structure makes code easier to scan - overrides are visible at the top, implementations below.

## Development Process
**ALWAYS update rules.md when adding new rules or guidelines.**

Keep this file synchronized with all working patterns and rules. This ensures:
- Rules are visible to the team
- Consistency across the project
- Easy reference for future work

## AI Agent Behavior
**ALWAYS follow the project rules in this file when modifying or creating code for this repository.**

This preference is project-local so it applies to all contributors working on the repo.

## Development Preferences
- Use absolute file paths in tool calls
- Include 3-5 lines of context before/after when replacing code
- Use multi_replace_string_in_file for multiple independent edits
- Parallelize independent tool calls when possible
- Verify changes work before confirming completion
