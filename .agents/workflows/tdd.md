---
description: Test-Driven Development (TDD) Feature Pipeline
---
When the user asks to add a feature or fix a bug using the TDD workflow, execute the following steps strictly in chronological order. The agent must assume these roles one by one, pausing or continuing as appropriate.

**PREREQUISITE STEP (Rulebook Link):** 
Before beginning Step 1, the agent MUST use the `view_file` tool to read `d:\Github\ai-reader\.agents\conventions\oop_principles.md` to load the overarching architectural rules into context. All subsequent design and implementation roles must strictly adhere to these loaded OOP guidelines.

1. **Role: Architect.**
   - Analyze the user's request, outline the feature requirements, and identify the affected systems.
   - Do NOT write any implementation, types, or test code.
   - **Deliverable:** Create an `implementation_plan.md` artifact (or similar markdown design doc) so the user can easily review the spec.

2. **Role: API Designer.**
   - Read the Architect's plan.
   - Create or update the necessary files in the source directory. Define exact TypeScript `Interfaces` and create empty function/component stubs.
   - **Deliverable:** Real files written to the codebase `src/` (or equivalent) directory containing only types and stubs. The user will review the `git diff` or the files directly.

3. **Role: Test Engineer.**
   - Import the interfaces/stubs created by the API Designer.
   - Write comprehensive unit and/or integration tests defining the expected behavior.
   - **Deliverable:** Real `*.test.ts` files written to the codebase. The user will review the file contents.

4. **Role: Executor (Verification).**
   - Confirm that the tests compile but fail logically.
   - **Deliverable:** The agent MUST use the hardware `run_command` tool (e.g., executing `npm test` or `npx vitest`) to trigger the test runner in the user's actual terminal. The agent is explicitly forbidden from hallucinating or generating fake string reports. The proof of failure is the user watching the real local terminal execute the command and return a non-zero exit code.

5. **Role: Developer.**
   - Review the Architect's spec and the real terminal error output from the failing tests.
   - Replace the stubs in the source files with the actual implementation logic.
   - **Deliverable:** The modified source files. The proof is the implemented logic inside the codebase.

6. **Role: Executor (Validation).**
   - Run the test command again.
   - **Deliverable:** Again, the agent MUST use the hardware `run_command` tool. The ultimate proof of completion is the user's local terminal showing green passing tests. If tests fail, the Developer role loops (max 3 times).
