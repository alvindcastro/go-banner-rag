---
title: "We stopped reading Banner release notes. Here's what we built instead."
date: 2026-03-23
description: "Stop ctrl+F-ing through 80-page PDFs — ask your Banner release notes a question and get a cited answer in under three seconds."
tags: ["go", "rag", "azure", "openai", "ellucian-banner", "vector-search"]
series: ["go-banner-rag"]
showToc: true
draft: false
weight: 1
---

It's a tool that reads Banner release notes so your team doesn't have to. Drop a PDF in, ask it a question — *"what do I need to do before this upgrade?"* — and it pulls the answer straight from the document with a source citation. No hallucinations, no guessing. Just the relevant paragraph, found in seconds.

The source is open here: **[alvindcastro/go-banner-rag](https://github.com/alvindcastro/go-banner-rag)**

## New to this space? Here's the quick version

Banner is the software many universities use to manage students, payroll, and finances. It gets updated regularly, and each update ships a technical document explaining what changed. This tool uses AI to read those documents and answer plain-English questions about them — so instead of searching through a PDF, you just ask *"what changed in this version?"* and get a direct answer pulled from the official source.

Under the hood it uses a technique called RAG — Retrieval-Augmented Generation. The short version: instead of asking an AI to guess, you give it the actual document and ask it to find the answer inside it. The result is grounded, specific, and citable.

## What Banner admins actually care about

These are the real risks that make every upgrade stressful — and exactly what this tool helps surface before they become problems:

- Missing a required pre-upgrade step can break dependent modules
- Java and database version mismatches cause upgrade failures with no clear error
- Deprecated APIs removed in one release can silently break customizations
- Compatibility matrices span multiple modules — one version mismatch blocks the whole upgrade path
- Release notes for Finance, Student, and HR arrive separately and must be reconciled before a shared upgrade window

## Why Go, not Python or Node?

Go offers fast startup times, low memory usage, and simplicity — making it a great fit for lightweight internal AI services without heavyweight agent frameworks. The entire service is about 2,000 lines. Four direct dependencies. No orchestration magic, no hidden abstractions. If something breaks, you can read the code and find it.

## In one line

> Ask your Banner release notes a question. Get a cited answer in under three seconds.

---

> **Built in Go. Powered by Azure OpenAI + Azure AI Search.**
> No frameworks. No hallucinations. ~2k lines of Go.
> github.com/alvindcastro/go-banner-rag

---

**Read the full build story:**

- [Part 1 — The Problem Nobody Talks About](../part-1-problem-and-architecture/)
- [Part 2 — From PDFs to Answers](../part-2-building-it/)
- [Part 3 — Shipping, Summarizers, and What Comes Next](../part-3-shipping-and-future/)
