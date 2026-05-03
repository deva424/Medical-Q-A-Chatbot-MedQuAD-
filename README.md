
#  Medical Q&A Chatbot (MedQuAD)

A specialized Question-Answering system designed to provide reliable medical information using the **MedQuAD Dataset**. This project leverages semantic search and Named Entity Recognition (NER) to understand and respond to user queries through a web interface.

---

##  Problem Statement
General-purpose chatbots often struggle with the precision required for medical inquiries. The goal of this project is to develop a domain-specific Q&A bot that:
*   Utilizes the **MedQuAD dataset** (12,000+ clinical Q&A pairs) to ensure data quality.
*   Implements a **Retrieval-Augmented** approach to find the most contextually relevant answers.
*   Performs **Medical Entity Recognition** to identify symptoms, diseases, and treatments within user queries.
*   Provides a clean, accessible **Streamlit** interface for end-user interaction.

---

##  Methodology

The system architecture follows a modern NLP pipeline for Retrieval-Augmented Generation (RAG) principles:

### 1. Data Processing
The MedQuAD dataset is provided in XML format. The system parses these files to extract clean Question-Answer pairs, which are then stored in a structured Pandas DataFrame for efficient handling.

### 2. Semantic Search & Vector DB
Instead of simple keyword matching, we use **Semantic Search**:
*   **Embeddings:** Questions are converted into high-dimensional vectors using the `all-MiniLM-L6-v2` Sentence Transformer.
*   **Indexing:** A **FAISS (Facebook AI Similarity Search)** index is built on these vectors. 
*   **Retrieval:** When a user asks a question, the system finds the "closest" existing question in the database using L2 distance (Euclidean distance).

### 3. Medical Named Entity Recognition (NER)
To enhance the assistant's understanding, we integrate **ScispaCy** (`en_core_sci_sm`). This specialized model identifies biomedical entities (like *asthma*, *hypertension*, or *insulin*) from the user's input, providing structured context alongside the retrieved answer.

### 4. User Interface
A **Streamlit** dashboard handles the frontend, maintaining session state for a "chat-like" experience and displaying detected medical entities as metadata.

---

##  Requirements & Installation

### Core Dependencies
*   **Python 3.10+**
*   **Streamlit:** For the web interface.
*   **FAISS-cpu:** For lightning-fast vector similarity search.
*   **Sentence-Transformers:** For generating semantic text embeddings.
*   **ScispaCy:** For specialized medical NLP tasks.
*   **Pandas:** For data manipulation.

### Setup
```bash
# Install required Python packages
pip install streamlit pandas sentence-transformers faiss-cpu spacy scispacy

# Install the specialized medical NLP model
pip install [https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.5.4/en_core_sci_sm-0.5.4.tar.gz](https://s3-us-west-2.amazonaws.com/ai2-s2-scispacy/releases/v0.5.4/en_core_sci_sm-0.5.4.tar.gz)

# Clone the MedQuAD dataset
git clone [https://github.com/abachaa/MedQuAD.git](https://github.com/abachaa/MedQuAD.git)

# Dataset link in drive
https://drive.google.com/drive/folders/1GIrZGkrzLmrdbu1rU8Hqlu0WCAn_HKPI?usp=drive_link

