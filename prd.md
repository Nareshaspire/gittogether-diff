# PRD: GitTogether Visual Diff & Summary Tool (PoC)

## Problem

Reviewing a change well means reading the diff, working out what it does to the system, spotting what could break callers, and then writing release notes by hand. That last step is tedious, and the middle two are easy to miss under time pressure.

## Target user

Developers and tech leads who review pull requests or prepare release notes and want a fast second opinion on a change.

## Value proposition

Paste two versions of a change and get, in seconds: what changed, what it means architecturally, what might break, and ready-to-paste markdown release notes.

## User stories

1. As a reviewer, I paste a before and after snippet and see a visual diff so I can confirm the tool is looking at what I think it is.
2. As a reviewer, I get an architectural impact summary so I understand the blast radius without reading every line.
3. As a maintainer, I see flagged potential breaking changes with severity so I know whether this is a patch, minor, or major release.
4. As a release manager, I copy clean markdown release notes into a changelog.
5. As a presenter, I click **Load sample** and run the whole flow without typing.

## Functional requirements

| ID | Requirement | Priority |
|---|---|---|
| F1 | Two text areas for Version A and Version B | Must |
| F2 | Client-side visual diff, added lines green, removed lines red | Must |
| F3 | Analyze button calls the backend and shows a loading state | Must |
| F4 | Result shows summary, architectural impact, breaking changes, release notes | Must |
| F5 | Breaking changes show severity (high / medium / low) | Must |
| F6 | Copy button for the release notes markdown | Must |
| F7 | Load sample button | Must |
| F8 | Demo mode when no API key is configured, clearly labeled | Should |
| F9 | Friendly error messages (empty input, oversize input, API failure) | Should |

## Non-functional requirements

- Runs with `node server.js`, no `npm install` required (Node 18+).
- API key stays server-side, read from environment or `.env`.
- Typical analysis completes in under 15 seconds.

## Demo script (about 2 minutes)

1. (0:00) State the problem in one sentence.
2. (0:15) Click **Load sample**. Point out the visual diff.
3. (0:30) Click **Analyze**.
4. (0:45) Walk through the summary and architectural impact.
5. (1:10) Highlight the flagged breaking change and its severity.
6. (1:30) Click **Copy** on the release notes and paste them somewhere.
7. (1:50) Close with what is next: GitHub integration, multi-file analysis.

## Success metrics (PoC)

- Demo recorded in one take under 2 minutes.
- Sample flagging a signature change correctly surfaces it as a breaking change.

## Future ideas (not in this PoC)

Fetch by commit SHA or PR URL, multi-file diffs, semver recommendation, GitHub Action, streaming output.
