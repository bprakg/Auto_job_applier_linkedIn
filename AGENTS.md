# AGENTS.md - Developer Instructions

## Execution
- **Main Bot**: `python runAiBot.py`
- **History UI**: `python app.py` (Access at `http://localhost:5000`)

## Configuration
- **Config Directory**: `config/` (`personals.py`, `questions.py`, `search.py`, `secrets.py`, `settings.py`).
- **Validation Requirement**: Every new configuration variable **MUST** be registered and validated in `modules/validator.py` within the corresponding `validate_*` method.

## Coding Conventions
Follow these strictly to avoid rejection:

### Naming
- **Functions & Global Variables**: `lower_snake_case`
- **Local Variables**: `camelCase`

### Documentation & Typing
- **Docstrings**: Mandatory `''' Explanation '''` placed immediately below the function definition.
- **Type Hints**: Mandatory for all function parameters and return types (e.g., `def func(p1: str) -> int:`).

### Contribution Attestation
All code additions or modifications must be wrapped in the following tags:
```python
##> ------ <Full Name> : <GitHub ID/Email> - <Type of change> ------
# Modified/New code here
##<
```

## Architecture
- `runAiBot.py`: Application entry point.
- `config/`: Environment and user-specific settings.
- `modules/`: Core logic, browser automation, and AI implementation.
- `modules/validator.py`: Central point for all configuration sanity checks.

---

## 🛠️ Current Status & Debugging Notes (May 2026)

### ✅ Resolved
- **Validator Crashes**: Fixed `desired_salary` validation error in `config/questions.py`.
- **Env Stability**: Updated `undetected-chromedriver` and `selenium` to handle Chrome version mismatches.
- **Search Location**: Improved selectors for the "City, state, or zip code" input to be more robust.
- **Logic Bugs**: Fixed `UnboundLocalError` for `jobs_top_card` in the main loop of `runAiBot.py`.
- **Selector Flexibility**: Modified `wait_span_click` to use descendants-based text matching (`.`) instead of `text()`.

### ⚠️ Pending / Known Issues
- **Easy Apply Filter**: The "Easy Apply" toggle in the "All filters" modal is currently not being selected. Multiple selector strategies (by name, aria-label, and ancestral fieldset) have been tried but are not consistently working.
- **Stale Elements**: The bot occasionally encounters `StaleElementReferenceException` when the LinkedIn DOM updates during application.
- **Debug Workflow**: Use `logs/filter_debug.html` to inspect the DOM of the filter modal when `apply_filters()` fails.
