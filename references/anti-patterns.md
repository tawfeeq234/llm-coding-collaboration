# Anti-Patterns to Avoid

Common LLM coding mistakes identified from production experience. Reference this when reviewing code or planning implementations.

## 1. Over-Abstraction

**Pattern**: Creating unnecessary layers, interfaces, or abstractions "for flexibility."

**Signs**:
- Factory classes for single implementations
- Interfaces with only one implementer
- Wrapper classes that just delegate
- Configuration objects for 2-3 settings

**Fix**: Implement the concrete case first. Abstract only when a second use case appears.

## 2. Premature Optimization

**Pattern**: Optimizing before correctness is established or before bottlenecks are identified.

**Signs**:
- Caching without profiling
- Complex data structures for small datasets
- Async/threading for I/O-bound operations that aren't bottlenecks
- Micro-optimizations in non-hot paths

**Fix**: Write correct, readable code first. Profile. Optimize only proven bottlenecks.

## 3. Comment/Code Drift

**Pattern**: Changing code without updating related comments, or leaving stale TODOs.

**Signs**:
- Comments describing what code used to do
- TODO comments from weeks/months ago
- Docstrings with wrong parameter names
- "Temporary" code that's now permanent

**Fix**: Treat comments as part of the code change. Delete outdated comments rather than leaving them.

## 4. Scope Creep in Refactors

**Pattern**: Refactoring adjacent code that wasn't part of the task.

**Signs**:
- PR/diff includes "while I was here..." changes
- Renaming variables in unrelated functions
- Reformatting files not touched by the feature
- "Improving" code outside the task scope

**Fix**: Stick to the task. Note improvements for separate PRs. Ask before expanding scope.

## 5. Defensive Over-Engineering

**Pattern**: Adding error handling, validation, or edge cases that aren't needed.

**Signs**:
- Try/except blocks catching exceptions that can't occur
- Null checks on values that are always present
- Validation for internal function parameters
- Fallbacks for impossible states

**Fix**: Handle errors at boundaries (user input, external APIs). Trust internal contracts.

## 6. API Bloat

**Pattern**: Exposing too many options, parameters, or methods.

**Signs**:
- Functions with 8+ parameters
- Boolean flags that change behavior
- Multiple ways to do the same thing
- "Kitchen sink" classes

**Fix**: Start minimal. Add parameters only when users request them. Prefer separate functions over flags.

## 7. Copy-Paste Proliferation

**Pattern**: Duplicating code instead of extracting shared logic.

**Signs**:
- Multiple functions with 80%+ identical code
- Same bug fixed in multiple places
- Inconsistent behavior between similar features

**Fix**: Extract shared logic immediately when duplicating. Don't wait for "refactor later."

## 8. Silent Assumptions

**Pattern**: Making decisions without documenting or communicating them.

**Signs**:
- Magic numbers without explanation
- Implicit ordering dependencies
- Undocumented preconditions
- "It works because..." knowledge only in developer's head

**Fix**: Add brief comments for non-obvious decisions. State assumptions explicitly in code or docs.

## 9. Gold Plating

**Pattern**: Adding features or polish that wasn't requested.

**Signs**:
- Logging infrastructure for a script
- Admin UI for internal tools
- Internationalization for English-only products
- "Nice to have" features bundled with requirements

**Fix**: Deliver exactly what was requested. Propose enhancements separately.

## 10. Inadequate Error Messages

**Pattern**: Generic or unhelpful error messages that don't aid debugging.

**Signs**:
- "An error occurred"
- "Invalid input" without specifying what's invalid
- Stack traces without context
- Errors that hide the root cause

**Fix**: Include what happened, what was expected, and what to do about it.
