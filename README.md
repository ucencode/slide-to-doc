# toolama

A growing set of offline AI-powered tools using Ollama and local LLMs.

## Tools

| Tool | Description |
|------|-------------|
| [pdf2img-ocr](pdf2img-ocr.py) | PDF → image → OCR via vision model, with optional refine output |

## Requirements

- Python 3.10+
- [Ollama](https://ollama.com) installed and running

## Setup

```bash
bash setup.sh
source venv/bin/activate
```

---

## pdf2img-ocr

Converts PDF pages to images, runs OCR via a local vision LLM, and optionally refines the output into clean text, study notes, or structured notes.

### Supported Models

| Role | Keywords matched |
|------|-----------------|
| Vision (OCR) | `qwen3-vl`, `qwen2.5vl`, `deepseek-ocr`, `llama3.2-vision`, `gemma4`, `ministral-3`, `glm-ocr` |
| Refine (LLM) | `glm-5.1`, `gemma4`, `qwen3.5`, `gpt-oss` |

Pull a model example:

```bash
ollama pull glm-ocr:bf16
```

### Usage

```bash
python pdf2img-ocr.py path/to/file.pdf
```

### Options

| Flag | Default | Description |
|------|---------|-------------|
| `--dpi` | `200` | Render resolution (higher = more detail, slower) |
| `--ocr-model` | `glm-ocr:bf16` | Override OCR model directly |

### Refine Modes

| Mode | Description |
|------|-------------|
| `skip` | Save raw OCR only |
| `clean` | Fix OCR noise, broken words, grammar |
| `summary` | Compress into bullet-point study notes |
| `deep` | Structured output: concept, core idea, key points, analogy |

### Output

```
outputs/
  <timestamp>-raw.txt       ← raw OCR text per page
  <timestamp>-compiled.txt  ← refined output (if selected)
```
