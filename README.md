# PDF-Chatbot
Junior AI Engineer Assignment of Amlgo Labs
 PDF Chatbot (Local Embeddings & Local LLM)

## Overview

This project is a **PDF chatbot** that can answer questions about a document (like a User Agreement or contract) using only **free, open-source tools**.  
It does not use OpenAI or any paid APIs, so you don’t need a credit card or API key.  
Everything runs locally on your computer.



## Project Architecture & Flow

1. **Document Preprocessing & Chunking:**  
   We start by splitting the PDF into small, readable pieces (called "chunks") using a script.  
   This makes it easier for the AI to search and understand the document.

2. **Semantic Embedding:**  
   Each chunk is converted into a list of numbers (an "embedding") using a free model called `all-MiniLM-L6-v2`.  
   This helps the AI compare the meaning of your question with the document chunks.

3. **Vector Database:**  
   All the embeddings are stored in a local database (Chroma), so we can quickly find the most relevant chunks for any question.

4. **Retriever:**  
   When you ask a question, the system searches the database for the most relevant chunks.

5. **Local LLM Generator:**  
   Instead of using OpenAI (which costs money), we use a small, free language model called TinyLlama.  
   This model takes your question and the relevant chunk(s) and tries to generate a helpful answer.

6. **Streamlit Chatbot Interface:**  
   The chatbot runs in your browser using Streamlit.  
   You type your question, and the answer appears in real time, streaming out as it’s generated.



## Why Not OpenAI?

We do **not** use OpenAI or any paid APIs because:
- They require payment and a credit card for API tokens.
- Our goal is to make everything free and accessible.
- All models and tools used here are open-source and run on your own computer.



## How to Run the Project

### 1. Install Requirements

Open your terminal and run:
```
pip install -r requirements.txt
pip install transformers
```

### 2. Preprocess & Chunk the PDF

Split your PDF into chunks:
```
python src/chunker.py
```

### 3. Create Embeddings

Generate embeddings and store them in the vector database:
```
python src/embedder.py
```

### 4. Start the Chatbot

Launch the Streamlit app:
```
streamlit run app.py
```
Open [http://localhost:8501](http://localhost:8501) in your browser.



## Model & Embedding Choices

- **Embeddings:**  
  We use `all-MiniLM-L6-v2` from the `sentence-transformers` library.  
  This model is fast, free, and works well for finding similar text.

- **LLM (Language Model):**  
  We use `TinyLlama-1.1B-Chat-v1.0`, a small, open-source model that can run on most computers.  
  It generates answers based on the retrieved document chunks and your question.

- **Vector Database:**  
  We use Chroma, a free and easy-to-use vector database for storing and searching embeddings.



## How the Chatbot Works (with Streaming)

- You type a question about the document.
- The system finds the most relevant chunk(s) from the PDF.
- The local LLM (TinyLlama) generates an answer using those chunks.
- The answer appears in your browser, streaming out in real time.
- You can also see which chunk(s) were used to answer your question.
- There’s a sidebar showing which model is used and how many chunks are in the database.
- You can clear the chat at any time.



## Sample Queries

Here are some example questions you can ask the chatbot:

- What is the main topic of the document?
- What sections survive after the termination of the User Agreement?
- What is the process for resolving legal disputes according to the document?
- Who are the entities referred to as "eBay" in this agreement?



## Screenshots

![alt text](<test1.jpg>)      ,   ![alt text](<test2.jpg>)    ,  ![alt text](<test3.jpg>)

## Notes

- All code and models are free and run locally.
- No API keys, payment, or credit card required.
- If you want to use a different document, just replace the PDF and rerun the chunking and embedding steps.



## Folder Structure

- `/data` – your original PDF files
- `/chunks` – processed and cleaned text chunks
- `/vectordb` – saved vector database with embeddings
- `/src` – all the Python scripts (chunker, embedder, retriever, generator, pipeline)
- `/notebooks` – (optional) for experiments and analysis
- `app.py` – the Streamlit chatbot app
- `requirements.txt` – list of required Python packages
- `README.md` – this file

## Github repository link

