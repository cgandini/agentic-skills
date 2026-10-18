# Audit Dimensions — full checklist

Load this when running a Full Audit. For each finding record: dimension, short title, exact location (file + line), severity, explanation, concrete recommendation.

**Do not invent findings. Do not report issues you cannot substantiate from the code provided.**

---

## Pattern Recognition Shortcuts

Fast greps that surface most real defects before deep reading.

| Pattern | Likely issue | Quick check |
|---|---|---|
| `eval()`, `exec()`, `os.system()` | Security critical | grep for these strings |
| `except:` / `except Exception:` | Silent failures | grep bare excepts |
| `password`, `secret`, `key`, `token` | Hardcoded credentials | grep + check if literal |
| `if DEBUG`, `debug=True` | Insecure default | check config blocks |
| Functions >50 lines | Maintainability risk | count lines per function |
| Nested `if` >3 levels | Complexity hotspot | visual scan |
| No `test_` / `.test.` files | Quality gap | list test files |
| `f"SELECT` or `+ "SELECT` | SQL injection | grep string-built queries |
| `requests.get` without `timeout=` | Production risk | check every HTTP call |
| `while True` without `break` | Unbounded loop | grep infinite loops |
| `@ts-ignore` / `@ts-expect-error` | Suppressed error | measure density per file |
| `as any` / `as unknown as` | Cast escape hatch | count per file |
| `useEffect(() => {...}, [])` w/o cleanup | React leak | grep empty-dep effects |
| `onClick={async () => await ...}` w/o try/catch | Unhandled rejection | grep inline async handlers |
| `.map(async ...)` without `Promise.all` | Silent unawaited work | grep async inside map |
| `JSON.parse(` without try/catch | Crash on malformed input | grep parse calls |

---

## 1. Architecture & Design

**Quick checks:** Can you find the entry point in 10 seconds? Are API / business logic / data layers distinguishable? Does any single file exceed 300 lines?

- Separation-of-concerns violations (business logic inside route handlers or UI components)
- God objects or modules with more than one clear responsibility
- Tight coupling with no abstraction boundary
- Blurred system boundaries (DB queries scattered across layers)
- Circular dependencies / import cycles
- No clear data flow or state management strategy

## 2. Consistency & Maintainability

**Quick checks:** Are similar operations named consistently (`get` vs `fetch` vs `load`)? Do function names match what they do? Is duplicated logic visible?

- Naming drift for the same operation (`get_user` / `fetchUser` / `retrieveUserData`)
- Mixed paradigms interleaved without justification
- Copy-paste logic repeated 3+ times — extract
- Abstractions that obscure rather than clarify
- Inconsistent error-handling patterns across modules
- Magic numbers or strings without named constants

## 3. Robustness & Error Handling

**Quick checks:** Does every external call (API, DB, file) have error handling? Any bare `except:`? What happens on empty, null, or malformed input?

- Missing input validation at entry points (HTTP handlers, CLI args, file reads)
- Catch-all handlers that swallow failures silently
- Unhandled edge cases: empty collections, null returns, zero values, division by zero
- Assuming external services always succeed, with no fallback
- No retry logic for transient failures (network, rate limits)
- Missing timeouts on blocking operations
- External data used without validation

## 4. Production Risks

**Quick checks:** Hardcoded URLs, IPs, or paths? Any logging at all? Database queries inside loops?

- Hardcoded configuration (URLs, credentials, timeouts, thresholds)
- Missing structured logging or observability hooks
- Unbounded loops, missing pagination, N+1 query patterns
- Blocking I/O in async contexts; thread-unsafe shared state
- No graceful shutdown or cleanup on exit
- Missing health / readiness endpoints
- No rate limiting or backpressure
- Synchronous operations in event-driven contexts

## 5. Security & Safety

**Quick checks:** grep `eval`, `exec`, `os.system`, `subprocess`. grep `password`, `secret`, `api_key`, `token` as literals. Look for `SELECT * FROM` + concatenation. Verify sanitization before DB, shell, or file operations.

- Unsanitized user input reaching a database, shell, file path, or `eval`
- Credentials, API keys, or tokens in source or logs
- Insecure defaults (`DEBUG=True`, permissive CORS, no rate limiting)
- Trust boundary violations — external data treated as internal
- SQL injection via string concatenation
- Path traversal — user input in file paths without validation
- Missing authentication or authorization on sensitive operations
- Insecure deserialization (`pickle`, `yaml.load` without SafeLoader)
- Missing CSRF protection on state-changing endpoints
- Wildcard CORS origins

## 6. Dead or Hallucinated Code

**Quick checks:** For each function/class definition, find its callers. Look for unused imports. Verify referenced libraries appear in `package.json` / `requirements.txt`.

- Functions, classes, or modules defined but never called
- Imports absent from declared dependencies
- References to APIs, methods, or fields that do not exist in the installed library version
- Type annotations contradicting actual usage
- Comments describing behavior the code does not have
- Unreachable blocks (after `return` / `raise` / `break` on all paths)
- Feature flags or conditionals that are always true or always false

## 7. Technical Debt Hotspots

**Quick checks:** Count function parameters (5+ = refactor candidate). Measure nesting depth (4+ = candidate). Look for boolean flags that switch behavior.

- Logic correct today that breaks under realistic load or scale
- Deep nesting (4+ levels) obscuring control flow
- Boolean parameter flags that change what a function does — split into separate functions
- Functions with 6+ parameters and no config object
- Areas where one future requirement change would touch many unrelated files
- Missing type hints on complex functions in dynamically typed languages
- No documentation for public APIs or non-obvious algorithms
- Test coverage gaps on critical paths
