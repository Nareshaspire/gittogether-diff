# Scope: GitTogether Visual Diff & Summary Tool (PoC)

**Timebox:** one afternoon. **Goal:** a working, demo-able proof of concept that fits a 2-minute screen recording.

## In scope

- Single web page with two input panes: **Version A (before)** and **Version B (after)**.
- Inputs can be raw code snippets or raw git commit diffs (unified diff text).
- A client-side **visual diff** (red/green line diff) of the two inputs.
- One **Analyze** button that sends both inputs to Claude and returns:
  1. A short plain-English summary
  2. Architectural impact
  3. Potential breaking changes, each with a severity
  4. Clean markdown release notes with a **Copy** button
- A **Load sample** button so the demo needs no typing.
- Zero-dependency Node server that serves the page and proxies the Claude API call (keeps the API key off the client).
- A **demo mode** (no API key needed) that returns a clearly labeled canned response, so the UI can always be shown.

## Out of scope (explicitly)

- Authentication, accounts, or saved history
- GitHub/GitLab integration, fetching commits by SHA or URL
- Multi-file repository analysis, cloning, or dependency graph building
- Streaming responses, rate limiting, caching
- Syntax highlighting, word-level diffs, side-by-side file trees
- Deployment, CI, tests beyond a manual smoke check
- Handling inputs larger than ~60k characters per pane

## Success criteria

- Paste or load a sample, click Analyze, and see all four result sections in under ~15 seconds.
- Whole flow can be recorded in a single take of under 2 minutes.
- `node server.js` is the only command needed to run it.

## Risks

| Risk | Mitigation |
|---|---|
| Model returns malformed JSON | Tolerant parser; show raw text as fallback |
| No API key during demo | Demo mode with labeled canned output |
| Large pastes slow or fail | Hard input cap with a clear error message |
