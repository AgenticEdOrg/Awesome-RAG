# AgenticEd: RAG Chunking Comparison Report

### Overview
This report documents the implementation and evaluation of three distinct text-chunking strategies (**Fixed-Size**, **Sentence-Based**, and **Paragraph-Based**) applied to the AgenticEd course content (`agenticed_content.txt`). Effective chunking optimizes content retrieval and context preservation for downstream Retrieval-Augmented Generation (RAG) systems.

---

### Summary Metrics Across All Three Methods

| Strategy | Total Chunks | Min Words | Max Words | Avg Words | Sentence Integrity | Paragraph Integrity |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Fixed-Size Chunking** | 10 | 37 | 180 | 97.3 | ❌ Broken (mid-sentence cuts) | ❌ Broken |
| **Sentence-Based Chunking** | 10 | 37 | 177 | 97.3 | ✅ Fully Preserved | ⚠️ Partial (grouped by sentence) |
| **Paragraph-Based Chunking** | 9 | 37 | 321 | 108.1 | ✅ Fully Preserved | ✅ Fully Preserved |

---

### Key Observations from the Experiments

1. **Boundary Preservation vs. Strict Sizing**:
   * **Fixed-size chunking** enforces a rigid word ceiling (180 words), but at the cost of splitting thoughts across chunk boundaries. For example, in Section 7, the text was cut mid-sentence between `fixed-7` (ending with `"7. Anyone visiting the"`) and `fixed-8` (starting with `"site can instantly generate an unverified certificate..."`).
   * **Sentence-based chunking** successfully resolved mid-sentence clipping by respecting grammatical punctuation (`.`, `!`, `?`), keeping every chunk safely under the 180-word soft budget (max: 177 words).
   * **Paragraph-based chunking** preserved topical unity and structural layout using double newline delimiters (`\n\n`), but resulted in an outlier in Section 7 (321 words) because the section was written as a single continuous block without blank lines.

2. **Which method is best for an AgenticEd Chatbot?**
   * **Sentence-based chunking with a soft word budget** provides the best overall balance for general retrieval. It guarantees that retrieved context contains grammatically complete sentences without risking oversized outliers that exceed LLM context windows.
   * For sections where multi-line formatting or structured lists are critical (such as Section 2's learning levels and Section 3's six weekly lessons), **paragraph-based chunking** is superior because it preserves structural layout and list relationships.