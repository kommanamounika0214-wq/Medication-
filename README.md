# Medication-
# H2: Medication Reminder Chatbot (Label-Aware)

## Problem Statement
Patients often struggle to understand complex drug labels and adhere to medication schedules. This project aims to build an AI-powered "Medication Reminder Chatbot" that allows users to ask natural language questions about specific drugs (e.g., side effects, contraindications) and automatically generates a structured reminder schedule.

The core problem is to convert unstructured medical text (drug labels) into actionable insights and structured data (JSON schedules) using Generative AI.

## Data Source
* **Dataset:** openFDA Drug Label API
* **Link:** https://open.fda.gov/apis/drug/label/download/
* **Description:** This project utilizes the openFDA API to fetch official drug labeling information, specifically focusing on sections like `dosage_and_administration`, `warnings`, and `indications_and_usage`.

## Proposed Solution (Rough Plan)
This solution utilizes a Retrieval-Augmented Generation (RAG) architecture to ensure accuracy and reduce hallucinations.

**1. Data Ingestion & Indexing:**
* Fetch drug label data (JSON/Text) from openFDA.
* Chunk the relevant text sections (Dosage, Warnings, etc.).
* Create vector embeddings of these chunks using an embedding model (e.g., OpenAI/Gemini embeddings).
* Store embeddings in a vector database (**ChromaDB**) for fast retrieval.

**2. RAG Pipeline (The "Chat" Feature):**
* **Input:** User asks a question (e.g., "Can I take Ibuprofen with milk?").
* **Retrieval:** The system queries ChromaDB to find the specific paragraphs from the official drug label relevant to the question.
* **Generation:** An LLM (Gemini/OpenAI) receives the user question + the retrieved label context and generates a precise, fact-based answer.

**3. Reminder Generation (The "Agent" Feature):**
* The system will include a specific prompt flow to extract dosage frequency instructions.
* **Output:** The LLM will generate a structured JSON object representing the medication schedule (e.g., `{"drug": "Amoxicillin", "frequency": "3 times daily", "times": ["08:00", "14:00", "20:00"]}`).

## Tech Stack
* **Language:** Python
* **Orchestration:** LangChain
* **Vector Database:** ChromaDB
* **LLM:** Gemini Pro / OpenAI GPT-4
* **Embeddings:** Google Generative AI Embeddings / OpenAI Embeddings

## Assumptions
* The user provides the exact generic or brand name of the drug.
* The openFDA API is available and responsive.
* The system focuses on text-based interaction (no voice/SMS integration initially).
