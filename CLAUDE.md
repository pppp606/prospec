# 🧠 AI Agent Guide: `prospec`

`prospec` is a test runner designed to evaluate prompt behavior in LLM-based coding tools like **Claude Code CLI**.

Inspired by testing frameworks like RSpec and Jest, it allows you to run lightweight, reproducible prompt-based test cases and store results in CSV format for historical comparison.

---

## 🔍 What It Does

* ✅ Runs prompt test cases (`instruction.txt` → `expected.txt`)
* 📊 Logs output correctness, tokens used, cost, duration
* 📁 Archives results per day for comparison
* ⚙️ Respects context auto-loaded by Claude Code (e.g. `/docs/ai`)
* 🧪 Can be integrated into CI or used locally like `npm test`

---

## 📁 Directory Structure

```
promptspecs/                 # Default prompt test directory
  └── user_enum_check/
      ├── instruction.txt    # Prompt to run
      └── expected.txt       # Expected output

logs/                        # Evaluation results
  └── archive/               # Daily backups (optional)

prospec.config.json          # Configuration file
```

---

## 🧪 Example Test Case

**promptspecs/user\_enum\_check/instruction.txt**

```txt
ユーザーの種類を表すenumに `admin`, `guest`, `apple` が定義されています。
`apple?` がtrueになるのはどのようなときか説明してください。
```

**promptspecs/user\_enum\_check/expected.txt**

```txt
`apple?` は、ActiveRecordのenum定義において `apple` という値が定義されている場合に、自身の値が `apple` であるかを返すpredicateメソッドです。
```

---

## ⚙️ prospec.config.json

```json
{
  "testdir": "promptspecs",
  "logdir": "logs",
  "archive": true,
  "match": "contains"
}
```

* `testdir`: Directory of test cases (can be customized)
* `logdir`: Where to store results
* `archive`: Save daily CSV snapshots (true/false)
* `match`: Matching strategy: `"exact"`, `"contains"`, or `"regex"`

---

## 🧾 CSV Output Format

Each test run appends to `logs/results-YYYYMMDD.csv`

```
date,test_name,success,input_tokens,output_tokens,total_cost_usd,duration_ms
2025-07-01,user_enum_check,true,25,456,0.1229,20879
```

---

## 🧭 Assumptions

* `Claude Code CLI` automatically loads context from `/docs/ai/`
* You do **not** need to specify `--context` or `input.rb`
* You can use `--output-format json` for parsing results
* Response body is **not** stored, only metadata and verdict

---

## 🛠 Planned Features

* `prospec run` command (TypeScript)
* `prospec diff` to compare test run CSVs
* Fuzzy matching or LLM-based evaluation
* Jest/CI integration
* Command hooks before/after test runs
