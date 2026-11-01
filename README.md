# 🤖 Agentic Multi-Document Research Assistant

An AI-powered research assistant that allows users to search across multiple PDF documents and receive accurate, context-aware answers using Retrieval-Augmented Generation (RAG), FAISS vector search, and Agentic AI workflows.

## 📌 Project Overview

Searching through multiple PDF documents manually can be time-consuming, especially when documents contain large amounts of information.

The **Agentic Multi-Document Research Assistant** simplifies this process by allowing users to upload multiple PDF documents and ask questions in natural language.

The system uses LangChain for document processing and RAG implementation, FAISS for efficient vector similarity search, and Gemini API for generating contextual answers.

LangGraph manages the agentic workflow by coordinating document retrieval, evidence evaluation, and additional retrieval when the available information is insufficient.

The assistant also provides document references to help users verify the generated answers.

## 🎯 Project Objectives

- Automate information retrieval from multiple PDF documents.
- Allow users to ask questions using natural language.
- Retrieve relevant information using semantic similarity search.
- Implement an agentic workflow that evaluates retrieved evidence.
- Perform additional retrieval when the initial context is insufficient.
- Generate context-aware answers with document references.
- Reduce manual document-search effort and improve answer reliability.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core application development |
| LangChain | Document loading, text splitting, embeddings, and RAG pipeline |
| LangGraph | Agentic workflow orchestration |
| Gemini API | Context-aware answer generation |
| FAISS | Vector storage and similarity search |
| Sentence Transformers / Gemini Embeddings | Convert text into vector representations |
| PyMuPDF / PyPDF | Extract text from PDF documents |

## ⚙️ System Workflow

1. **PDF Upload:** Users upload multiple PDF documents.
2. **Document Extraction:** Extract text from uploaded PDF files.
3. **Text Chunking:** Split extracted text into smaller, meaningful chunks with overlapping content.
4. **Embedding Generation:** Convert text chunks into numerical vector representations using an embedding model.
5. **Vector Storage:** Store generated embeddings in the FAISS vector database.
6. **User Query:** Accept questions in natural language.
7. **Semantic Retrieval:** Search FAISS to retrieve the most relevant document chunks.
8. **Evidence Evaluation:** LangGraph coordinates the workflow and checks whether the retrieved information is sufficient to answer the question.
9. **Additional Retrieval:** If the evidence is insufficient, the workflow performs another retrieval attempt.
10. **Answer Generation:** Gemini generates an answer based on the retrieved context.
11. **Source References:** Display document references to help users verify the generated information.

## 🧠 Agentic Workflow Using LangGraph

LangGraph is used to manage the agentic workflow through different nodes and conditional transitions.

### Main Workflow Nodes

- **Document Retrieval Node:** Retrieves relevant chunks from the FAISS vector database.
- **Evidence Evaluation Node:** Checks whether the retrieved context contains sufficient information to answer the user's question.
- **Additional Retrieval Node:** Performs another search if the initial retrieval does not provide sufficient evidence.
- **Answer Generation Node:** Uses Gemini API to generate a response based on the available context.

### Workflow Architecture

```text
             User Uploads PDFs
                    |
                    v
            Document Extraction
                    |
                    v
              Text Chunking
                    |
                    v
           Embedding Generation
                    |
                    v
             FAISS Vector DB
                    |
                    v
               User Query
                    |
                    v
             Retrieve Context
                    |
                    v
           Evidence Evaluation
                    |
             Is Evidence
              Sufficient?
               /       \
             Yes        No
              |          |
              v          v
         Generate    Additional
          Answer      Retrieval
              |          |
              |__________|
                    |
                    v
             Final Answer
                    |
                    v
           Document References
```

## 🔍 Key Features

- **Multi-PDF Support:** Search information across multiple PDF documents.
- **Semantic Search:** Retrieve relevant information based on meaning rather than exact keyword matching.
- **RAG Architecture:** Generate answers using retrieved document context.
- **Agentic Workflow:** Use LangGraph to manage retrieval and evidence evaluation.
- **Conditional Retrieval:** Perform additional searches when the initial evidence is insufficient.
- **Source References:** Provide document references for answer verification.
- **Context-Aware Responses:** Generate answers grounded in the uploaded documents.

## 📁 Project Structure

```text
Agentic-Multi-Document-Research-Assistant/
│
├── data/
│   └── documents/
│
├── documents/
│
├── embeddings/
│   └── faiss_index/
│
├── agents/
│   ├── retrieval_agent.py
│   ├── evaluation_agent.py
│   └── answer_agent.py
│
├── workflow/
│   └── research_graph.py
│
├── utils/
│   ├── pdf_extractor.py
│   ├── text_chunker.py
│   └── embeddings.py
│
├── config.py
├── main.py
├── requirements.txt
├── .env.example
├── .gitignore
└── README.md
```

*Note: This is a suggested folder structure. Modify it based on your actual implementation.*

## 🚀 Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/Agentic-Multi-Document-Research-Assistant.git

cd Agentic-Multi-Document-Research-Assistant
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

Activate the environment:

**Windows:**
```bash
venv\Scripts\activate
```

**Linux / macOS:**
```bash
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Gemini API Key

Create a `.env` file in the project root directory.

```env
GEMINI_API_KEY=your_gemini_api_key
```

Never upload your actual API key to GitHub.

### 5. Run the Application

```bash
python main.py
```

## 📊 Example Use Case

**Input:**

Upload multiple PDF documents related to Artificial Intelligence, Machine Learning, and Deep Learning.

**User Query:**

"What are the major differences between supervised and unsupervised learning?"

**Expected Output:**

The assistant retrieves relevant information from the uploaded documents, evaluates the available evidence, and generates a structured answer explaining the differences.

It also provides document references so users can verify the information.

## 🔮 Future Enhancements

- Add support for DOCX, TXT, and other document formats.
- Implement hybrid search combining keyword and semantic retrieval.
- Integrate a reranking model to improve retrieval accuracy.
- Add conversation memory for follow-up questions.
- Implement document-level access control.
- Add a user-friendly Streamlit interface.
- Support large-scale document collections.

## 💡 Expected Benefits

- Reduces manual document-search effort.
- Improves information retrieval across multiple documents.
- Provides context-aware and evidence-supported answers.
- Improves answer reliability through evidence evaluation.
- Makes research and document analysis more efficient.

## 👩‍💻 Author

**Ambika Yallal**

Interested in Artificial Intelligence, Generative AI, Machine Learning, and Agentic AI.

---

⭐ If you find this project useful, feel free to star the repository!
