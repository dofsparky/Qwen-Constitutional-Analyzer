# QCAv16-3

## Offline Constitutional Analysis Engine

> **Retrieval-first constitutional analysis powered by C, llama.cpp, and Qwen.**

QCAv16-3 is an offline constitutional analysis engine designed to compare statutes, regulations, ordinances, and legal documents against constitutional reference material without relying on cloud services.

Instead of forcing an entire legal code into a language model's context window, QCA indexes documents, retrieves only the most relevant statutory material, builds a compact prompt, and submits that prompt to a locally running Qwen model through **llama.cpp**.

Everything stays on your machine.

No cloud.

No subscriptions.

No telemetry.

---

# Features

* Completely Offline
* Written in ANSI C
* Compatible with llama.cpp
* Optimized for Qwen GGUF models
* Retrieval-First Architecture
* Automatic Document Caching
* Prompt Budget Management
* Resume Support
* Multi-threaded Processing
* Markdown, JSON and CSV Reports
* Constitutional Cross-Reference Engine
* Compact Prompt Generation

---

# Why QCA?

Large legal codes contain far more text than can fit into an LLM's context window.

Rather than asking the model to read thousands of pages at once, QCA narrows the problem before inference begins.

```text
Legal Document
       │
       ▼
 Text Extraction
       │
       ▼
 Chunk Builder
       │
       ▼
 Document Cache
       │
       ▼
 Front Matter Filter
       │
       ▼
 Relevance Ranking
       │
       ▼
 Compact Prompt Builder
       │
       ▼
 Prompt Budget Enforcement
       │
       ▼
 Qwen + llama.cpp
       │
       ▼
 Constitutional Analysis
```

This retrieval-first approach improves efficiency while leaving more context available for reasoning and structured output.

---

# What's New in QCAv16-3

## Intelligent Ingestion

QCA now filters non-statutory material before analysis.

Skipped content includes:

* Publisher front matter
* Table of contents
* Index pages
* Editorial sections
* Short placeholder chunks
* Other non-statutory metadata

This prevents the model from wasting inference time on material that has no constitutional relevance.

---

## Compact Retrieval

Instead of embedding complete matching sections into every prompt, QCA includes concise excerpts from the highest-ranked matches.

Benefits include:

* Smaller prompts
* More room for reasoning
* Reduced context pressure
* Better completion rates

---

## Prompt Budget Management

QCA automatically limits prompt size to preserve context for:

* Model reasoning
* Final analysis
* Structured output

---

## Cached Processing

Documents are indexed once and reused across future analyses, reducing preprocessing time and improving retrieval consistency.

---

# Typical Workflow

## 1. Prepare Documents

```bash
./QCAv16-3 \
    --prepare \
    --input IowaCode2026.txt \
    --reference bill_of_rights.txt \
    --outdir analysis
```

This extracts, indexes, and caches the documents without invoking the language model.

---

## 2. Run Constitutional Analysis

```bash
./QCAv16-3 \
    --profile ultra \
    --workers auto \
    --prompt-budget 5000 \
    --input IowaCode2026.txt \
    --reference bill_of_rights.txt \
    --outdir analysis \
    --runner-template 'llama-cli -m MODEL.gguf --jinja --reasoning on --reasoning-budget -1 -c {CTX_SIZE} -n 2048 -f {PROMPT_FILE}'
```

---

## 3. Question Mode

```bash
./QCAv16-3 \
    --questions questions.txt \
    --input IowaCode2026.txt \
    --reference bill_of_rights.txt \
    --outdir analysis \
    --runner-template 'llama-cli ...'
```

---

# Output

QCA generates:

* Markdown reports
* JSON reports
* CSV exports
* Prompt files
* Raw model responses
* Cached document packs
* Resume state information

---

# Project Philosophy

QCA is built around a simple principle:

> **Language models should spend their context reasoning about the law—not reading publication metadata.**

The engine performs the heavy lifting before inference by filtering, ranking, and compressing the source material into a prompt that emphasizes the most relevant statutory text.

---

# Current Status

Current capabilities include:

* Retrieval-first prompt generation
* Cached indexing
* Prompt budgeting
* Multi-document comparison
* Constitutional cross-referencing
* Resume support
* Fully offline execution

---

# Roadmap

Future development is expected to focus on:

* Improved statutory section detection
* Better legal citation recognition
* Enhanced retrieval ranking
* Richer reporting
* Interactive desktop interface
* Visualization tools for retrieval and analysis

---

# Requirements

* Linux
* GCC
* llama.cpp
* Qwen GGUF model

Recommended:

* Multi-core CPU
* SSD storage
* 8 GB RAM or more

---

# Disclaimer

QCA is intended for constitutional research, education, and document analysis.

It does **not** provide legal advice or authoritative legal determinations. AI-generated analyses should always be verified against the underlying legal authorities, applicable statutes, and relevant case law.

---

# License

See the included LICENSE file for licensing information.

---

## Built for researchers, developers, and legal professionals who want private, transparent, fully offline constitutional analysis.


# QCAv16-2

### Offline Constitutional Analysis Engine

> **Retrieval-first constitutional analysis powered by C, llama.cpp, and Qwen.**

QCAv16-2 is a high-performance offline constitutional analysis engine designed to compare statutes, regulations, ordinances, and legal documents against constitutional reference material without relying on cloud services.

Instead of attempting to place entire legal codes into an LLM's context window, QCA builds searchable document caches, retrieves only the most relevant material, and generates optimized prompts that fit comfortably within the model's available context.

Everything runs locally.

No subscriptions.

No telemetry.

No internet required.

---

# Highlights

* Completely Offline
* Written in ANSI C
* Compatible with llama.cpp
* Optimized for Qwen GGUF models
* Retrieval-First Architecture
* Prompt Budgeting
* Automatic Document Caching
* Resume Interrupted Analyses
* Markdown / JSON / CSV Reports
* Multi-threaded Document Preparation
* Cross-Reference Engine
* Context-Aware Prompt Generation

---

# Why QCA?

Large legal codes can contain millions of characters.

Even modern language models cannot reliably analyze an entire legal code within a single context window.

QCA solves this problem by retrieving only the portions of the documents that matter.

```text
Document

        │

        ▼

Chunk Builder

        │

        ▼

Searchable Cache

        │

        ▼

Relevance Ranking

        │

        ▼

Compact Context Assembly

        │

        ▼

Prompt Budget Enforcement

        │

        ▼

Qwen + llama.cpp

        │

        ▼

Structured Constitutional Report
```

This approach dramatically reduces context waste while leaving more room for reasoning and complete responses.

---

# What's New in QCAv16-2

This release focuses on prompt quality and model reliability.

### Compact Retrieval

Instead of embedding complete matching sections, QCA now inserts compact excerpts for the highest-ranked matches.

This leaves significantly more room for Qwen's reasoning.

---

### Smarter Prompt Budgeting

QCA automatically reserves context space for:

* Model reasoning
* Final analysis
* Structured output

rather than allowing the prompt to consume nearly the entire context window.

---

### Malformed Chunk Protection

QCA detects and skips malformed chunks before they are sent to the model.

Examples include:

* Empty sections
* One-character titles
* Corrupted chunks
* Placeholder content

This prevents wasted inference on invalid inputs.

---

### Cached Retrieval

Documents are indexed once and reused on future runs.

Benefits include:

* Faster startup
* Reduced preprocessing
* Smaller prompts
* Better retrieval consistency

---

# Typical Workflow

## Step 1

Prepare the documents.

```bash
./QCAv16-2 \
    --prepare \
    --input IowaCode2022.pdf \
    --reference BillOfRights.pdf \
    --outdir analysis
```

This builds cached document packs and searchable indexes.

---

## Step 2

Analyze the document.

```bash
./QCAv16-2 \
    --profile ultra \
    --workers auto \
    --prompt-budget 5000 \
    --input IowaCode2022.pdf \
    --reference BillOfRights.pdf \
    --outdir analysis \
    --runner-template 'llama-cli -m MODEL.gguf --jinja --reasoning on --reasoning-budget -1 -c {CTX_SIZE} -n 2048 -f {PROMPT_FILE}'
```

---

## Step 3

Ask constitutional questions.

```bash
./QCAv16-2 \
    --questions questions.txt \
    --input IowaCode2022.pdf \
    --reference BillOfRights.pdf \
    --outdir analysis \
    --runner-template 'llama-cli ...'
```

---

# Generated Output

QCA produces:

* Markdown reports
* JSON reports
* CSV exports
* Prompt files
* Raw model responses
* Cached document packs
* Resume checkpoints

---

# Design Philosophy

QCA is built around one principle:

> **The language model should spend its context reasoning—not reading.**

Rather than flooding the model with entire documents, QCA supplies only the evidence most relevant to the current analysis.

This improves efficiency, consistency, and the likelihood of complete responses.

---

# Current Status

Current capabilities include:

* Retrieval-first prompt generation
* Cached indexing
* Automatic prompt budgeting
* Multi-document comparison
* Constitutional cross-referencing
* Resume support
* Offline execution

---

# Roadmap

## QCAv17

Planned enhancements include:

* Native Qt desktop application
* Interactive constitutional dashboard
* Constitutional heat map
* Retrieval visualizer
* Prompt inspector
* Live analysis progress
* One-click project management
* Interactive report browser

---

# Requirements

* Linux
* GCC
* llama.cpp
* Qwen GGUF model

Recommended:

* Multi-core CPU
* SSD storage
* 8 GB RAM or more

---

# Disclaimer

QCA is intended for constitutional research, education, and document analysis.

It does **not** provide legal advice or make authoritative legal determinations. AI-generated findings should always be reviewed alongside the original legal authorities and applicable case law.

---

# License

See the included LICENSE file for licensing information.

---

## Built for researchers who want constitutional analysis to remain private, transparent, and completely offline.



# QCAv16-1 — Offline Constitutional Analysis Engine

> **Research constitutional questions locally using Qwen + llama.cpp. No cloud. No subscriptions. Your machine. Your documents.**

---

## Overview

QCA (Qwen Constitutional Analyzer) is a C-based offline document analysis engine designed to compare statutes, regulations, ordinances, and other legal documents against one or more constitutional reference documents.

The current focus is using the **United States Bill of Rights** as the primary reference while analyzing large legal codes such as the Iowa Code.

Unlike traditional document search tools, QCA uses a **retrieval-first architecture** that builds searchable indexes and only sends the most relevant material to the language model.

Everything runs locally.

---

# Features

* Fully offline
* Written in C
* Works with llama.cpp
* Optimized for Qwen GGUF models
* PDF and TXT input support
* Multiple reference documents
* Cached document indexing
* Resume interrupted analyses
* Automatic prompt budgeting
* Retrieval-first architecture
* Markdown, JSON and CSV output
* Multi-core document preparation
* Context-aware prompt generation

---

# Why QCA Exists

Large legal codes frequently exceed the context window of local language models.

Instead of attempting to load an entire legal code into Qwen, QCA performs retrieval before inference.

```
PDF
      ↓

Chunk Documents

      ↓

Build Search Index

      ↓

Retrieve Best Matches

      ↓

Neighbor Expansion

      ↓

Prompt Budget Check

      ↓

Qwen

      ↓

Structured Report
```

This allows QCA to analyze very large documents while remaining compatible with modest hardware.

---

# Requirements

* Linux
* GCC
* llama.cpp
* Qwen GGUF model (recommended)

Recommended hardware:

* 8 GB RAM minimum
* SSD storage
* Multi-core CPU

---

# Installation

Compile:

```bash
make
```

---

# Prepare Documents

Build the searchable cache.

```bash
./QCAv16-1 \
    --prepare \
    --input "/path/document.pdf" \
    --reference "/path/bill_of_rights.pdf" \
    --outdir analysis
```

This extracts the source documents, creates searchable packs, and builds the retrieval cache without starting the language model.

---

# Analyze Entire Document

```bash
./QCAv16-1 \
    --profile ultra \
    --workers auto \
    --prompt-budget 5000 \
    --input "/path/document.pdf" \
    --reference "/path/bill_of_rights.pdf" \
    --outdir analysis \
    --runner-template 'llama-cli -m MODEL.gguf --jinja --reasoning on --reasoning-budget -1 -c {CTX_SIZE} -n 2048 -f {PROMPT_FILE}'
```

---

# Question Mode

```bash
./QCAv16-1 \
    --questions questions.txt \
    --input "/path/document.pdf" \
    --reference "/path/bill_of_rights.pdf" \
    --outdir analysis \
    --runner-template 'llama-cli ...'
```

---

# Retrieval-First Architecture

QCA intentionally avoids sending entire documents to the LLM.

Instead it:

* indexes documents
* scores relevant chunks
* retrieves the best matches
* expands nearby context
* enforces a configurable prompt budget
* launches the model

This leaves room for reasoning and reduces context overflow.

---

# Current Output

QCA currently generates:

* report.md
* JSON output
* CSV indexes
* prompt files
* raw model responses
* cached retrieval packs
* resumable analysis state

---

# Current Development

Recent work has focused on:

* smarter retrieval
* prompt budgeting
* resumable analyses
* automatic context trimming
* multi-threaded preparation
* improved cross-reference handling

---

# Planned Features

## QCAv17

* Native Qt desktop interface
* Live analysis dashboard
* Constitutional heat map
* Prompt inspector
* Retrieval visualizer
* Interactive report browser
* One-click document preparation
* Built-in model launcher

---

# Project Goals

The long-term objective is to build a professional, offline constitutional research platform that remains accessible on consumer hardware.

Planned capabilities include:

* Multiple constitutional reference documents
* State constitutions
* User-supplied reference libraries
* Advanced retrieval algorithms
* Plugin architecture
* Cross-platform desktop application
* Optional REST API

---

# Disclaimer

QCA is intended for research, education, and document analysis.

It does **not** provide legal advice, legal representation, or authoritative determinations regarding the constitutionality of any law. Results are generated by an AI model and should be independently verified against the underlying legal authorities.

---

## License

See the LICENSE file included with this repository.

---

**Made with C, llama.cpp, and a lot of persistence.**








# QCAv13-7 - Qwen Constitutional Analyzer

> **An offline Constitutional research assistant powered by llama.cpp and Qwen.**
>
> Analyze legislation against the United States Bill of Rights entirely on your own computer.

---

# What is QCA?

QCA (Qwen Constitutional Analyzer) is a **100% local** constitutional research tool written in C.

Its purpose is to help researchers, students, journalists, attorneys, historians, and everyday citizens compare legislation against a constitutional reference document (such as the U.S. Bill of Rights).

Unlike cloud AI systems, **QCA never requires an Internet connection once everything is installed.**

Your documents remain on your computer.

---

# Goals

QCA attempts to identify:

* Possible Constitutional concerns
* Possible conflicts with the Bill of Rights
* Direct restrictions
* Indirect restrictions
* Hidden burdens
* Chilling effects
* Excessive government discretion
* Search and seizure issues
* Due process concerns
* Equal protection concerns
* Property rights concerns
* Potential constitutional arguments

It does **not** make legal rulings.

Instead, it provides organized research for further review.

---

# Important Disclaimer

QCA is **not** a lawyer.

It does **not** determine whether a statute is unconstitutional.

It identifies **possible Constitutional issues** that deserve additional legal analysis.

Always verify important conclusions using primary legal sources and qualified legal professionals.

---

# Features

* Completely offline
* Written in portable C
* Works with llama.cpp
* Supports Qwen GGUF models
* PDF input
* Plain text input
* Multiple reference documents
* Resume interrupted analysis
* Cached document indexing
* Automatic worker selection
* Multiple memory profiles
* Markdown reports
* JSON output
* CSV index generation
* Large document support (70MB+)

---

# System Requirements

Minimum

* 64-bit Linux
* 8 GB RAM
* GCC
* pdftotext
* llama.cpp

Recommended

* 16 GB RAM or more
* SSD storage
* Qwen3-4B-Q4_K_M.gguf

---

# Software Needed

## 1. Install llama.cpp

Clone and build:

```bash
git clone https://github.com/ggml-org/llama.cpp
cd llama.cpp
make -j$(nproc)
sudo make install
```

Verify:

```bash
llama-cli --version
```

---

## 2. Download a Qwen Model

Recommended:

```
Qwen3-4B-Q4_K_M.gguf
```

Place it somewhere such as:

```
/home/username/models/
```

Example:

```
/home/delta/models/Qwen3-4B-Q4_K_M.gguf
```

---

## 3. Build QCA

```bash
unzip QCAv13-7_bundle.zip

cd QCAv13-7

make
```

---

# Supported Input Types

Input document

* PDF
* TXT

Reference document

* PDF
* TXT

Examples

```
2022-iowa-code.pdf

bill-of-rights.pdf
```

---

# How QCA Works

Instead of trying to force an entire 70+ MB document into the model's context window, QCA performs several stages:

1. Extracts text from PDFs
2. Builds a cached document pack
3. Splits documents into logical chunks
4. Creates a searchable local index
5. Retrieves the most relevant sections
6. Sends those sections to Qwen
7. Saves the AI's response
8. Repeats until the document has been processed

This approach dramatically reduces memory usage while improving answer quality.

---

# Analysis Mode

If **no `--questions` file** is supplied, QCA automatically enters Analysis Mode.

Each section of the document is analyzed individually against the supplied Constitutional reference.

Example:

```bash
./QCAv13-7 \
--profile ultra \
--workers auto \
--input "/home/delta/iowa/2022-iowa-code.pdf" \
--reference "/home/delta/references/bill-of-rights.pdf" \
--outdir "iowa-2022" \
--runner-template 'llama-cli -m /home/delta/models/Qwen3-4B-Q4_K_M.gguf --jinja --reasoning on --reasoning-budget -1 -c {CTX_SIZE} -n 2048 --temp 0.6 --top-k 40 --top-p 0.95 --min-p 0.05 --repeat-penalty 1.05 -f {PROMPT_FILE}'
```

---

# Question Mode

Create a text file:

```
questions.txt
```

Example:

```
Does this chapter burden freedom of speech?

Could this section violate the Fourth Amendment?

Does this statute create compelled speech?

Could this licensing requirement burden a Constitutional right?
```

Run:

```bash
./QCAv13-7 \
--questions questions.txt \
--profile ultra \
...
```

---

# Profiles

| Profile | Context Size |
| ------- | -----------: |
| low     |         1024 |
| medium  |         2048 |
| high    |         4096 |
| ultra   |         8192 |

Ultra should be used whenever sufficient RAM is available.

---

# Workers

Automatic:

```
--workers auto
```

Manual:

```
--workers 1

--workers 2

--workers 4
```

For systems with 8 GB RAM, `--workers auto` is generally the safest choice.

---

# Output Files

```
report.md
```

Human-readable report.

```
index.json
```

Machine-readable output.

```
index.csv
```

Spreadsheet-friendly summary.

```
.qca_cache/
```

Cached document packs.

```
.qca_state/
```

Resume information.

```
work/
```

Prompts and raw AI responses.

---

# Resume Capability

If analysis is interrupted, simply execute the same command again.

QCA automatically resumes from the last completed section.

---

# Cached Document Packs

The first run extracts and indexes the documents.

Future runs reuse the cached data, making subsequent analyses significantly faster.

Use:

```
--reindex
```

to force regeneration.

---

# Why Use Cached Packs?

A 70 MB legal code cannot fit inside an 8K context window.

Instead, QCA indexes the document once and retrieves only the most relevant sections for each analysis. This retrieval-based workflow is substantially more efficient and better suited to limited hardware.

---

# Repository Structure

```
QCAv13-7/
│
├── QCAv13-7
├── QCAv13-7.c
├── README.md
├── Makefile
│
├── work/
├── .qca_cache/
├── .qca_state/
│
├── report.md
├── index.json
└── index.csv
```

---

# Roadmap

Future versions are planned to include:

* Better semantic document retrieval
* Multiple Constitutional reference documents
* Cross-document citation graph
* Persistent local memory
* Automatic constitutional amendment detection
* Multi-model support
* Windows support
* Optional graphical interface
* Export to PDF
* HTML reports
* Faster indexing
* Improved retrieval ranking

---

# Contributing

Bug reports, suggestions, and pull requests are welcome.

If you discover issues or have ideas for improving constitutional research workflows, feel free to open an issue or submit a pull request.

---

# License

Free and Open Source

2026 - ∞

---

# Acknowledgements

This project would not be possible without the open-source community.

Special thanks to the developers behind:

* llama.cpp
* GGML
* Qwen
* GCC
* Poppler (`pdftotext`)
* ---buddy ;)---

---

# Final Notes

QCA is designed as a research aid. It helps users organize and examine legal text through the lens of a constitutional reference while keeping all processing local. Treat its findings as starting points for further investigation rather than definitive legal conclusions.
