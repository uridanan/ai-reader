---
description: Automated QA Explorer & Bug Logger
---
When the user asks to run an exploratory QA session or find bugs, execute the following steps chronologically to hunt for errors and feed them back into the TDD pipeline.

1. **Role: Test Environment Setup.**
   - Ensure the application is running locally.
   - IMPORTANT: Ensure the standard output/error of the backend and frontend servers are being written to a log file (e.g., `/tmp/qa_session.log`) so they can be parsed later. If the server needs to be started, use the `run_command` tool to run it in the background, piping output to the log file (e.g., `npm run dev > /tmp/qa_session.log 2>&1`).

2. **Role: The Chaos Monkey (Browser Subagent).**
   - Execute the `browser_subagent` tool and direct it to the local application URL.
   - Provide the subagent with an exploratory task description: *"Explore the application extensively posing as an erratic user. Click all main navigation links, attempt to fill out and submit any forms (both with valid and invalid/empty data), and interact with dynamic UI elements. Attempt to break the UI. When you have exhausted the main user flows, return a detailed summary of the exact steps you took."*
   - Set a highly descriptive `RecordingName` so the session is saved as a WebP video for human review.

3. **Role: Log Analyst.**
   - Once the subagent finishes and returns control, use the `grep_search` tool (or `read_file`) on `/tmp/qa_session.log`.
   - Search for critical server or application error keywords such as `ERROR`, `Exception`, `Traceback`, `500`, or `Unhandled`.

4. **Role: Bug Reporter (Synthesis).**
   - Cross-reference the Subagent's summary of actions with the specific errors found in the logs.
   - Create or update a `bug_backlog.md` file in the root directory.
   - For every distinct error found, create a structured ticket that includes:
     - **Issue:** A brief title.
     - **Stack Trace:** The raw error logs.
     - **Reproducible Use Case:** The exact actions the subagent was performing right before the error appeared.
     - **TDD Hook:** A pre-written prompt ready to be copy-pasted into the `/tdd` workflow (e.g., *"Using the /tdd workflow, fix the null reference error occurring when the registration form is submitted with an empty email field."*).
