# Typhon Web UI

Typhon Web UI is a visual console for running:

- `Typhon.bypassRCE`
- `Typhon.bypassREAD`

It is designed for quick pyjail experimentation with a cleaner workflow than raw script calls.

## Quick start

```powershell
cd <project-root>
python -m pip install -r webui\requirements.txt
python webui\app.py
```

Open `http://127.0.0.1:5000`.

## What changed in this UI

The page is split into:

- Basic area (common settings):
  - command/filepath mode
  - `local_scope`
  - WAF rules (`banned_chr`, `allowed_chr`, `banned_re`, `banned_ast`, `max_length`)
- Advanced area (engine tuning only):
  - search depth / recursion
  - runtime behavior (`timeout_sec`, `log_level`, `interactive`)
  - output strategy (`print_all_payload`)

This keeps common blacklist/whitelist constraints out of Advanced Options.

## Output terminal behavior

The right panel is styled as a terminal shell and now does output cleanup for readability:

- strips ANSI color escape sequences
- folds noisy progress lines (e.g. repeated `Bypassing (...)`)
- reduces repeated blank lines and duplicate separators
- keeps final summary and successful payload sections visible

## Language

Built-in bilingual UI:

- `中文`
- `EN`

Language choice is stored in `localStorage`.

## local_scope tokens

`local_scope` accepts JSON. For non-JSON objects, use tokens:

- `@builtin:list`
- `@builtin:dict`
- `@builtin:Exception`
- `@module:os`

Example:

```json
{
  "lit": "@builtin:list",
  "dic": "@builtin:dict",
  "__builtins__": null
}
```

## Notes

- Leaving `local_scope` empty keeps Typhon's original behavior (no forced safe default by Web UI).
- `is_allow_exception_leak` is shown in `READ` mode only.
