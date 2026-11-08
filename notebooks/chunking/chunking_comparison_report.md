# AgenticEd: RAG Chunking Comparison Report

### Overview
This report documents three text-chunking strategies (**Fixed-Size**, **Sentence-Based**, and **Paragraph-Based**) applied to the AgenticEd course content (`agenticed_content.txt`). Effective chunking preserves context for downstream Retrieval-Augmented Generation (RAG) systems.

---

### Summary Metrics Across All Three Methods

| Strategy | Total Chunks | Min Words | Max Words | Avg Words | Sections Split |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Fixed-Size Chunking** | 5 | 26 | 139 | 77.4 | None |
| **Sentence-Based Chunking** | 5 | 26 | 139 | 77.4 | None |
| **Paragraph-Based Chunking** | 5 | 26 | 139 | 77.4 | None |

The file has 5 sections, and each section is under the 180-word budget. Each method therefore produces one chunk per section, and the three outputs are identical.

---

### Key Observations from the Experiments

1. **The three methods only differ for long sections.** Every section in this file is shorter than the 180-word budget (the longest is Section 3 at 139 words), so no method has to split anything. Adding a section longer than 180 words would show the differences: fixed-size chunking would cut mid-sentence, sentence-based chunking would keep sentences whole, and paragraph-based chunking would keep paragraphs whole unless a paragraph exceeds the budget.

2. **Which method is best for an AgenticEd Chatbot?**
   * For this file, the output is identical, so no method is better.
   * For general retrieval, **sentence-based chunking with a soft word budget** is the safest choice. It never cuts a sentence and keeps chunks under the budget.
   * For sections where line breaks or lists matter, such as Section 2's learning levels and Section 3's six weekly lessons, **paragraph-based chunking** keeps that layout intact.
