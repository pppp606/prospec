## ✅ ToDo: Development Tasks

* [ ] **Create `run.ts`**

  * Iterate over each test case inside the configured `testdir`
  * Run `instruction.txt` with `claude` CLI
  * Compare the result to `expected.txt` using the configured match method
  * Use `--output-format json` to extract metadata (tokens, cost, duration)
  * Append results to `logs/results-YYYYMMDD.csv`

* [ ] **Implement `utils/claudeRunner.ts`**

  * Function to execute Claude CLI and parse JSON output
  * Handle errors, timeouts, malformed responses

* [ ] **Create `matcher.ts`**

  * Implements comparison logic for `match: exact | contains | regex`

* [ ] **Write test code (Jest)**

  * Unit tests for `matcher.ts`
  * Integration tests for `run.ts` (mocking Claude responses)

* [ ] **Log handling**

  * Append new test results to `logs/results-YYYYMMDD.csv`
  * If `archive` is enabled, generate a new file each day

* [ ] **Add example test cases**

  * Provide working and failing samples in `promptspecs/sample/`

* [ ] **Documentation**

  * Write a general-purpose `README.md`
  * Keep `README.agent.md` up-to-date for AI agents

* [ ] **CLI wrapper for `prospec`**

  * `prospec run`: execute all prompt tests
  * `prospec diff`: compare test runs across dates (planned feature)

* [ ] **Prevent leaking `expected.txt` to the AI during test runs**

  * Ensure `expected.txt` is **never included in Claude's context**
  * For Claude Code CLI, update the project-level `conf` to include:

    ```json
    {
      "ignorePatterns": ["expected.txt"]
    }
    ```
  * Confirm the context loading mechanism respects this exclusion
  * Optionally validate this behavior with a control test case

