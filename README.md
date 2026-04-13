# pdf2img-ocr

A local PDF OCR pipeline powered by [Ollama](https://ollama.com) vision models. Converts PDF pages to images, runs OCR via a vision LLM, and optionally refines the output into clean text, study notes, or structured notes — all running offline.

## Features

- Multi-page PDF → image → OCR via local vision model
- Three refine modes: **clean**, **summary**, **deep**
- Output language selection: English or Bahasa Indonesia
- Auto-discovers available Ollama models
- Saves raw and compiled output to `outputs/`

## Requirements

- Python 3.10+
- [Ollama](https://ollama.com) installed and running
- At least one supported vision model pulled in Ollama

### Supported Models

| Role | Keywords matched |
|------|-----------------|
| Vision (OCR) | `qwen3-vl`, `qwen2.5vl`, `deepseek-ocr`, `llama3.2-vision`, `gemma4`, `ministral-3`, `glm-ocr` |
| Refine (LLM) | `glm-5.1`, `gemma4`, `qwen3.5`, `gpt-oss` |

## Setup

```bash
bash setup.sh
source venv/bin/activate
```

Pull a model (example):

```bash
ollama pull glm-ocr:bf16
```

## Usage

```bash
python pdf2img-ocr.py path/to/file.pdf
```

### Options

| Flag | Default | Description |
|------|---------|-------------|
| `--dpi` | `200` | Render resolution (higher = more detail, slower) |
| `--ocr-model` | `glm-ocr:bf16` | Override OCR model directly |

### Example

```bash
python pdf2img-ocr.py lecture.pdf --dpi 300
```

The script will:
1. Ask you to select a vision model for OCR
2. Process each page and print token/timing stats
3. Ask if you want to refine the output (skip / clean / summary / deep)
4. If refining: ask for a refine model and output language
5. Save results to `outputs/<timestamp>-raw.txt` and `outputs/<timestamp>-compiled.txt`

## Output

```
outputs/
  20240413120000-raw.txt       ← raw OCR text per page
  20240413120000-compiled.txt  ← refined output (if selected)
```
