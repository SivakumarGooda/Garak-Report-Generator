# Garak-Report-Generator

Converts [Garak](https://github.com/NVIDIA/garak) JSONL scan output into a
single, self-contained HTML report that is easier to read than the raw JSONL.

The report groups results by probe, shows the model's responses, highlights
refusals and jailbreak indicators, and prints a summary of failed tests and
overall risk.

## Requirements

Python 3.8+ (standard library only — no third-party packages).

## Usage

```bash
python garak_reporter.py -i <scan.report.jsonl> -o <report.html>
```

Example:

```bash
python garak_reporter.py -i llama3.1_test.report.jsonl -o llama3.1.html
```

| Option | Required | Description |
|---|---|---|
| `-i`, `--input` | Yes | Garak `.report.jsonl` file to read |
| `-o`, `--output` | No | Output HTML path (default: `garak_report.html`) |

The script prints a summary to the terminal: model, target type, total tests,
total requests/responses, failed test cases, failed responses, and overall risk.

## Sample data in this repository

| File | Description |
|---|---|
| `llama3.1_test.report.jsonl` | Garak scan output for Llama 3.1 via Ollama |
| `dolphin_test.report.jsonl` | Garak scan output for Dolphin Llama 3 |
| `llama3.1.html`, `dolphin-llama3.html`, `ollama_demo.html` | Generated example reports |

## Security note

The generated HTML loads Chart.js from the jsdelivr CDN
(`https://cdn.jsdelivr.net/npm/chart.js`). For offline or high-assurance use,
vendor Chart.js locally or pin an exact version with a Subresource Integrity
(SRI) hash. Report content includes raw model output, so treat generated HTML
as untrusted data and open it locally rather than hosting it publicly.
