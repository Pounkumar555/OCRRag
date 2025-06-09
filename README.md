# OCRRag
Here's the cleaned-up version of the `README.md` file with all emojis removed:

---

# OCR\_RAG: Intelligent Document Processing with Mistral OCR + Qdrant + Gemini

This n8n workflow automates document processing from PDFs using OCR, vector embeddings, and AI-powered retrieval-augmented generation (RAG). It converts PDFs to text using Mistral OCR, indexes content into Qdrant for semantic search, and enables chat-based Q\&A through Gemini AI.

---

## Features

* Google Drive Integration: Automatically fetch PDFs from a folder.
* OCR with Mistral: Extracts text and page-level content using Mistral’s OCR API.
* Semantic Chunking & Embeddings: Chunks and embeds content using OpenAI embeddings.
* Vector Storage with Qdrant: Stores vectorized documents for fast semantic retrieval.
* Chat-triggered Q\&A: Supports conversational RAG using Gemini AI + LangChain nodes.

---

## Setup Instructions

### 1. Create Qdrant Collection

Use the `Create collection` node:

* Replace `QDRANTURL` with your Qdrant instance URL.
* Replace `COLLECTION` with the collection name, e.g., `ocr_mistral_test`.

```json
{
  "vectors": {
    "size": 1536,
    "distance": "Cosine"
  }
}
```

---

### 2. Ingest PDFs from Google Drive

* Set your Google Drive credentials.
* Point the `Search PDFs` node to your folder containing PDFs.

### 3. OCR + Chunk + Embed

* PDFs are uploaded to Mistral and processed with OCR.
* The extracted content is chunked using a Token Splitter.
* Embeddings are generated via OpenAI Embeddings API.

---

### 4. Store in Qdrant

* The markdown chunks are stored in the configured Qdrant collection.
* Optionally, you can use summarization for light-weight embedding with the `Summarization Chain`.

---

### 5. Retrieval-Augmented Chat (RAG)

* The `When chat message received` trigger starts a Q\&A workflow.
* The `Vector Store Retriever` finds relevant chunks using Qdrant.
* The `Question and Answer Chain` returns Gemini-powered answers.

---

## Key Technologies Used

| Tool/Service | Role                           |
| ------------ | ------------------------------ |
| Mistral OCR  | Extract text from PDFs         |
| n8n          | Workflow orchestration         |
| Qdrant       | Vector database for RAG        |
| OpenAI       | Embeddings generation          |
| Gemini AI    | Conversational AI for answers  |
| LangChain    | Q\&A Chain & Integration layer |

---

## Testing

To test the workflow:

1. Click “Test Workflow” in n8n.
2. Send a chat message (e.g. "What is this document about?").
3. Observe the Gemini response powered by vector search.

---

## Notes

* Ensure you have credentials set for:

  * Google Drive
  * Mistral Cloud
  * Qdrant (HTTP Header Auth)
  * OpenAI
* The workflow includes a subworkflow call for modular OCR processing.
* Modify the `Set page` node if you want full content or summary-based embeddings.

---

## Screenshot

![image](https://github.com/user-attachments/assets/e6a1667c-1ed5-4e5a-8062-39c42c8186ac)

---

## Files & Nodes Overview

* `Get PDF`, `Mistral Upload`, `Mistral Signed URL`, `Mistral OCR`
* `Token Splitter`, `Embeddings OpenAI`, `Qdrant Vector Store`
* `When chat message received`, `Vector Store Retriever`, `Google Gemini Chat Model`
* `Summarization Chain`, `Loop Over Items`, `Execute Workflow`

---

## Use Cases

* Enterprise Document Analysis
* PDF-based Chatbots
* Intelligent Knowledge Retrieval
* Legal/Medical Document Summarization

---

## Author

Built by [Pounkumar](https://github.com/Pounkumar555)
For support or questions, feel free to reach out.

---
