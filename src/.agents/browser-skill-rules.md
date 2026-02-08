# Browser Access (Mandatory)

If completing a task requires a **real browser** (page rendering, SPA behavior, JavaScript execution, UI interactions, authentication, visual verification, screenshots, browser console, network requests), the agent **MUST** use the browser-skill implemented on top of `camhahu/browser`, as described in `skills/browser/SKILL.md`.

## When browser-skill is mandatory

Use browser-skill in all cases where it is necessary to:

- verify data or behavior on a real website rather than relying on memory or assumptions
- open a page and wait for it to fully load
- scroll pages and navigate via links
- click buttons, work with forms, selects, and modal dialogs
- perform authentication and work with cookies or sessions
- take screenshots or provide visual confirmations
- validate SPA behavior (React, Vue, etc.)
- confirm that UI or functionality actually works in practice

## Forbidden behavior

- ❌ It is forbidden to "simulate" a browser by guessing or inventing page contents.
- ❌ It is forbidden to replace browser-skill with plain HTTP requests when UI, JavaScript, or visual validation is required.
- ❌ If there is any doubt whether a browser is required — **assume that it is**, and use browser-skill.

## Workflow

1. Open and follow the instructions in `skills/browser/SKILL.md`.
2. Use browser-skill to:
   - start a browser session
   - navigate to the required URL
   - wait for DOM and network readiness
   - perform actions (clicks, input, navigation)
   - collect results (text, screenshots, DOM fragments, logs)
3. Properly terminate the browser session according to the skill instructions.

## Result requirements

- Clearly state **what exactly was verified** (URL, page state, key elements).
- If screenshots were taken, save them to the path specified by the skill and reference them explicitly.
- If the outcome depends on UI state, describe the **exact sequence of browser actions** performed.

## Error handling

If browser-skill fails (timeouts, blocking, authentication issues):

- capture and preserve errors, logs, or screenshots
- explicitly describe the cause of the failure
- propose the minimal next step (test account, credentials, whitelisting, disabling anti-bot in staging, etc.)
