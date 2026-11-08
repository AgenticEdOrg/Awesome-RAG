# AgenticEd: RAG Chunking Comparison Report

### Overview
This report compares three text-chunking strategies (**Fixed-Size**, **Sentence-Based**, and **Paragraph-Based**) on the AgenticEd sample content (`agenticed_content.txt`). Good chunking keeps context intact for downstream Retrieval-Augmented Generation (RAG) systems.

---

### Summary Metrics Across All Three Methods

| Strategy | Total Chunks | Min Words | Max Words | Avg Words | Sections Split |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Fixed-Size Chunking** | 8 | 26 | 180 | 101.9 | Section 4, mid-sentence |
| **Sentence-Based Chunking** | 8 | 26 | 179 | 101.9 | Section 4, between sentences |
| **Paragraph-Based Chunking** | 8 | 26 | 152 | 101.9 | Section 4, between paragraphs |

The file has 6 sections. Five are shorter than the 180-word budget, so each becomes one chunk. Section 4 (the FAQ, 428 words) is longer, so each method splits it into three chunks.

---

### Key Observations from the Experiments

1. **Fixed-size chunking cuts sentences.** Section 4 is split at exactly 180 words. That falls mid-sentence twice: "...with your discussion" / "depth." and "...they've worked" / "through the weeks...".

2. **Sentence-based chunking keeps sentences whole.** Every break falls between sentences, and every chunk stays under the 180-word budget.

3. **Paragraph-based chunking keeps paragraphs whole.** Section 4 becomes three chunks of 130, 152, and 146 words, each holding one or more complete question-and-answer pairs.

4. **Which method is best for an AgenticEd Chatbot?**
   * **Sentence-based chunking with a soft word budget** is the best overall choice for this file. It never cuts a sentence and keeps chunks under the budget.
   * **Paragraph-based chunking** keeps each question and answer together, which suits FAQ-style content.
