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

Choose the license that best matches your goals before publishing (for example, MIT, BSD-3-Clause, GPLv3, or Apache-2.0).

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
