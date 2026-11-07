# AI PyVuln Detector

A command-line tool that sends a Python file to the Gemini API and prints a color-coded list of the security vulnerabilities it finds, each with an explanation, impact, and suggested fix.

> **Status:** early prototype, built in a weekend. It has not been benchmarked yet, so treat its output as a second opinion, not a verdict. See [Known limitations](#known-limitations).

![Scanner output on the sample file](docs/output-severity.png)

## What it detects

Tested so far on a deliberately vulnerable sample (`examples/vun.py`):

| Type | Found in sample |
|---|---|
| SQL injection | Yes |
| Command injection (`os.system` with user input) | Yes |
| Weak password hashing (MD5) | Yes |
| Hardcoded credentials | Yes |

Each finding is printed as:

```
SEVERITY: CRITICAL
TYPE: SQL Injection
DESCRIPTION: User input is directly concatenated into a SQL query string without sanitization.
IMPACT: An attacker can bypass authentication, read, modify, or delete database contents.
FIX: cursor.execute("SELECT * FROM users WHERE username = ? AND password = ?", (username, password))
```

Severity levels are color-coded in the terminal with `colorama`.

## Requirements

- Python 3.10+ (developed on 3.14)
- A Gemini API key ([how to get one](https://ai.google.dev/gemini-api/docs/api-key)); developed and run on the free tier
- Packages: `google-genai`, `python-dotenv`, `colorama`

## Setup

```bash
git clone <repo-url>
cd <repo-folder>

python -m venv venv
source venv/bin/activate          # fish shell: source venv/bin/activate.fish
                                  # Windows:    venv\Scripts\activate

pip install -r requirements.txt
```

Create a `.env` file in the project root:

```
GOOGLE_API_KEY=your_key_here
```

`.env` is listed in `.gitignore`. Never commit it. If a key ever lands in git history, revoke it and create a new one.

## Usage

```bash
python scanner.py path/to/file.py
```

Try it on the included sample:

```bash
python scanner.py examples/vun.py
```

> `examples/vun.py` contains intentionally vulnerable code (including shell command execution). It is a test input. **Do not run it.**

## How it works

1. `scanner.py` loads the API key from `.env` and reads the target file.
2. The file's contents are inserted into a security-analysis prompt that asks for a fixed report format (severity, type, description, impact, fix).
3. The prompt is sent to `gemini-3.5-flash-lite`.
4. The response is printed with severity levels colored by `colorama`.

## Known limitations

- **Your code leaves your machine.** The full file is sent to Google's API, including any secrets inside it. Don't scan proprietary code or files containing real credentials.
- **Output is not deterministic.** Scanning the same file twice produced different report layouts (one run included CWE IDs, the other did not):

  | Run 1 | Run 2 |
  |---|---|
  | ![Run 1](docs/run-1.png) | ![Run 2](docs/run-2.png) |

- **Severity is the model's opinion.** It is not CVSS or any calibrated scale. In the sample, hardcoded credentials were rated MEDIUM, which many reviewers would rate higher.
- **Suggested fixes are not verified.** For example, the SQL injection fix parameterizes the query but still compares a plaintext password. Review every fix before applying it.
- **Prompt injection is possible.** Text inside the scanned file (such as a comment addressed to the model) can influence the report.
- **No measured accuracy.** It has only been run on one small sample, so false-positive and false-negative rates are unknown.
- Python files only, one file per run.

## Roadmap

- [ ] Benchmark against [Bandit](https://github.com/PyCQA/bandit) on a set of intentionally vulnerable Python files: what each tool catches and misses
- [ ] Request structured JSON output instead of free text, so the report format is stable
- [ ] Redact secrets before sending code to the API
- [ ] Package as a VS Code extension

## Project layout

```
scanner.py          # CLI entry point
examples/vun.py     # intentionally vulnerable test input (do not run)
docs/               # screenshots used in this README
requirements.txt
.env                # your API key (not committed)
```
