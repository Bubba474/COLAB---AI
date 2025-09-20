# COLAB---AI
🤖 AI Agent - Triage & Internal Policies

This project was developed during the Alura + Google Gemini Immersion and implements an AI Agent for:

📌 Automatic Service Desk triage (classifying user requests into self-resolution, request for more info, or ticket creation).

📑 Internal Policy Assistant (HR/IT) that answers questions based on company documents using RAG (Retrieval-Augmented Generation).

⚙️ Tech Stack

Python 3

LangChain

Google Gemini (via LangChain + API Key)

FAISS
 – Vector database for semantic search

PyMuPDF
 – PDF document parsing

🚀 Features
🔹 1. Automatic Triage (Service Desk)

The agent classifies user messages into a structured JSON output:

{
  "decisao": "AUTO_RESOLVER" | "PEDIR_INFO" | "ABRIR_CHAMADO",
  "urgencia": "BAIXA" | "MEDIA" | "ALTA",
  "campos_faltantes": ["..."]
}


📌 Rules:

AUTO_RESOLVER: Clear questions that can be answered by internal policies.

PEDIR_INFO: Vague messages that require more context.

ABRIR_CHAMADO: Requests for exceptions, approvals, or special access.

🔹 2. Internal Policy Q&A (RAG)

Upload and process PDF documents (internal policies).

Split text into chunks for better indexing.

Generate embeddings with Gemini.

Store vectors in FAISS for semantic retrieval.

Answer user questions only based on available documents. If no relevant context is found, the agent replies:

"I don’t know."


Each answer can also return citations with:

📄 Document name

📍 Page number

📌 Relevant text snippet

🛠️ Installation

Clone this repository or copy the notebook.

Install dependencies:

pip install --upgrade langchain langchain-google-genai google-generativeai
pip install --upgrade langchain_community faiss-cpu langchain-text-splitters pymupdf


Set your Google Gemini API Key in Colab secrets or environment variables:

from google.colab import userdata
GOOGLE_API_KEY = userdata.get('GEMINI_API_KEY')

🧪 Example Queries
triagem("Can I get reimbursement for my home office internet?")
# -> {"decisao": "AUTO_RESOLVER", "urgencia": "BAIXA", "campos_faltantes": []}

perguntar_politica_RAG("Can I reimburse Alura courses?")
# -> Answer + document citations (if found)

📌 Use Cases

HR and IT policy Q&A assistant

Service Desk automation (reduce manual triage)

Knowledge management based on company documents
