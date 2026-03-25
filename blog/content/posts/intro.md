---
title: "Building a Banner Upgrade Assistant with Go and Azure"
date: 2026-03-23
description: "A practical RAG service that answers questions about Ellucian Banner ERP upgrades using official release notes — built in Go on top of Azure OpenAI and Azure AI Search."
tags: ["go", "rag", "azure", "openai", "ellucian-banner", "vector-search"]
series: ["go-banner-rag"]
showToc: false
draft: false
weight: 1
---

I recently built a small Retrieval-Augmented Generation (RAG) service in Go that answers questions about Ellucian Banner ERP upgrades using official release notes and documentation.

The core idea is simple: take a large document corpus, index it semantically, and let users ask natural-language questions that return grounded, source-based answers.

In this project, Banner PDF release notes are parsed, chunked, and embedded using Azure OpenAI. Those embeddings are stored in Azure AI Search — using hybrid vector + keyword search. When a user asks a question, the system retrieves the most relevant content and generates an answer strictly based on that context.

## Why Go?

Go offers fast startup times, low memory usage, and simplicity — making it a great fit for lightweight internal AI services without heavyweight agent frameworks.

## Key highlights

- Explicit, easy-to-follow RAG pipeline
- No orchestration frameworks or hidden magic
- Hybrid search for better precision
- Answers grounded in real documentation

This project is intended as a practical reference implementation for teams looking to build production-ready RAG systems — especially for internal knowledge and upgrade scenarios.

The full source is open-sourced here: **[alvindcastro/go-banner-rag](https://github.com/alvindcastro/go-banner-rag)**

---

**Read the full build story:**

- [Part 1 — The Problem Nobody Talks About](../part-1-problem-and-architecture/)
- [Part 2 — From PDFs to Answers](../part-2-building-it/)
- [Part 3 — Shipping, Summarizers, and What Comes Next](../part-3-shipping-and-future/)
