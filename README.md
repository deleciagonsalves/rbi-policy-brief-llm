# RBI Policy Brief Generator with an LLM (and a Hallucination Check)

A Python project that uses an open-source LLM to turn an RBI policy document (PDF) into a plain-English brief, compares a basic prompt with a structured prompt, and then fact-checks the LLM's numbers against the original text.

## Why this project
LLMs can sound confident and still invent numbers. In economics and finance a wrong number matters, so this project does not just use an LLM, it also checks it.

## How it works
1. Read the PDF with pypdf and split it into chunks of about 300 words
2. Load an instruction-tuned open LLM (Qwen2.5-1.5B-Instruct) with Hugging Face Transformers
3. Summarise each chunk, then combine the notes into one brief (map-reduce)
4. Compare a basic prompt with a structured prompt (role, rules, output format)
5. Hallucination check: find every number in the LLM output and test whether it appears in the source document

## Tech stack
Python, Hugging Face Transformers, PyTorch, Qwen2.5 (open LLM), pypdf, regular expressions, Google Colab

## How to run
Open the notebook in Google Colab, choose Runtime > Change runtime type > T4 GPU, run each step in order, and upload an RBI policy PDF when asked.

## Data used
An RBI Monetary Policy document from October 2026 (PDF).

## Key findings
- The LLM introduced no numbers missing from the source (0 unsupported numbers across the brief and both prompt answers).
- The structured prompt (role, rules, output format) gave a shorter, more focused answer than the basic prompt.
- The number check cannot verify claims without numbers, such as the stated risks, so those must be checked against the source by hand.
## Limitations
- A small open model is weaker than the largest LLMs and can still make mistakes
- The number check only catches numbers that are missing from the source
- Only the first 6 chunks are summarised, to keep it fast

## Future improvements
Compare two model sizes, add a RAG step to choose the most relevant chunks, and build a Gradio interface.
