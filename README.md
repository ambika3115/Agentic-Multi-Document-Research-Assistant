📚 **Agentic Multi-PDF Research Assistant**

An AI research assistant that searches across multiple PDF documents and answers questions with verifiable page-level citations. It uses Retrieval-Augmented Generation (RAG) with FAISS vector search, and a LangGraph agent that checks whether the retrieved evidence is sufficient and searches again when it is not.

Tech stack: Python · LangChain · LangGraph · Gemini API · FAISS · Gradio

✨ **Features**
- Multi-document RAG: index many PDFs into a single FAISS vector store and ask questions across all of them.
- Agentic workflow (LangGraph): the agent plans its searches, retrieves evidence, grades whether it is enough, and runs additional searches with new queries when information is missing.
- Answers with references: every claim is cited as [file.pdf, p.X]. Citations are checked against the chunks that were actually retrieved, and a Sources list (file, page, snippet) is shown under each answer. Unmatched citations are flagged with a warning.
- Transparent reasoning: an expandable Agent steps section shows the queries, the evidence check, and any follow-up searches.
- Incremental indexing: add more PDFs at any time; only the new files are embedded.
- Two ways to use it: a polished Gradio web UI or a command-line mode.
- Notebook-friendly: missing dependencies are installed automatically on first run (useful for fresh Colab sessions).


🧠 **How it works**
Node	                What it does
plan	          Uses Gemini (structured output) to break the question into 1–3 focused search queries.
retrieve	      Runs each pending query against FAISS using MMR for diverse results, and merges new chunks into the evidence pool (duplicates removed).
grade	          Gemini judges whether the evidence fully supports an answer. If not, it states what is missing and proposes new queries (queries already tried are filtered out).
generate	      Answers using only the evidence, cites [file.pdf, p.X], states clearly what the documents do not cover, then verifies each citation.


-**Running in Google Colab / Jupyter**
- Paste the contents of multi_pdf_research_assistant.py into a cell.
- Set your key above it: import os; os.environ["GOOGLE_API_KEY"] = "your-gemini-key".
- Run the cell. The first run installs dependencies (~1 minute). For a public share link, set os.environ["GRADIO_SHARE"] = "1" first.

Colab may print pip dependency-conflict warnings about google-auth or requests. They are harmless for this project.


💬 **Example questions**
- Summarize the key points of each document.
- Compare the main conclusions across the documents.
- What methods or approaches are described? Cite the pages.
- Do any of the documents contradict each other?

**Example of the output format:**

text
Revenue grew 10% in 2023 [annual_report.pdf, p.12], while the second paper
attributes cost reductions to automation [ops_study.pdf, p.4].

Sources (cited in the answer)
- annual_report.pdf, page 12: "Revenue grew 10% in 2023 ..."
- ops_study.pdf, page 4: "Costs fell due to automation ..."

▸ Agent steps


⚠️ **Limitations**
- Scanned / image-only PDFs contain no extractable text and need OCR first.
- Citation checks are structural: they confirm that a cited file and page were among the retrieved evidence, not that the model interpreted the passage correctly. Use the Sources snippets to verify important claims.
- API rate limits: free-tier Gemini quotas can slow down indexing of very large PDFs. The script batches requests and retries automatically.
- Answers are only as good as the retrieved text; tables, charts, and figures inside PDFs are not interpreted.

