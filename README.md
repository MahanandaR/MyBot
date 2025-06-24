# SmartLinkBot

➤ Problem Statement
---------------------
In today's fast-paced digital world, users often need quick, reliable answers from specific web content without reading entire articles or reports. General-purpose chatbots like ChatGPT may not give accurate responses from custom sources.
There is a need for a smart assistant that can extract, understand, and answer questions based only on a user-specified set of URLs.

----------------------------------------------------------------------------------------------------------------------------------------------------------

➩ Project Goal:
-----------------
Build a chatbot that allows users to ask questions about the latest news headlines from reliable sources like NDTV, BBC, or India Today, and get summarized, intelligent answers.

➺ Tech Stack:
--------------
● Python || Streamlit (for UI) || LangChain || HuggingFace Embeddings || ChromaDB (Vector DB) || LLM API (Groq or OpenAI) || UnstructuredURLLoader (for loading news content)

-----------------------------------------------------------------------------------------------------------------------------------------------------------
➤ Implementation Overview
----------------------------
→ This project implements a mini RAG-based chatbot that:

● Takes URLs from the user via a Streamlit UI.

● Scrapes and loads webpage content using UnstructuredURLLoader.

● Splits the content into chunks and stores them in a Chroma vector database using Hugging Face embeddings.

● Uses LangChain's RAG pipeline with the Groq-hosted LLaMA 3 LLM to retrieve relevant chunks and generate answers.

● Displays answers and source URLs in a styled interface, with optional dark mode.

It’s designed to help users ask natural questions and get contextual answers from any given webpage.
![image](https://github.com/user-attachments/assets/c3ce80b2-f049-4495-b322-a6dc2af7a41d)

✹ Think of this project as a mini ChatGPT-like bot, but with a twist:
-----------------------------------------------------------------------
#### ⋆ How It’s Like ChatGPT:

⋆ It uses a Large Language Model (LLM) (like ChatGPT does) to generate answers.

⋆ It accepts natural language questions from the user.

⋆ It responds in a chat-like Q&A format.

#### ⋆ How It's Different:

⋆ It doesn’t rely on training data from the internet.

⋆ Instead, it pulls content only from the URLs you provide.

⋆ It uses RAG (Retrieval-Augmented Generation), which first fetches relevant chunks from the URL content (vector store) and then sends them to the LLM for answering.

##### ❝ It’s a mini GPT-powered Q&A bot that reads the webpages you give it and answers your questions based only on that content.❞
---------------------------------------------------------------------------------------------------------------------------------------------------------
➤ Setup and Installation
-----------------------------------
1.Create and Activate Virtual Environment:
![image](https://github.com/user-attachments/assets/297cb678-ae28-48bc-80c8-6147e23858ae)


> conda create -n tf-env python=3.10

> conda activate tf-env

2.Install Dependencies:

>pip install -r requirements.txt

3.Create a .env file in the root directory and add:

> Grog and HuggingFace API Key & save.

➺ Folder Structure:
--------------------
![image](https://github.com/user-attachments/assets/c15bcf90-a231-477f-900f-9e937d8ce8e8)

---------------------------------------------------------------------------------------------------------------------------------------------------------------
➤ Script: rag.py – Responsible for scraping, chunking, embedding, and answering
--------------------------------------------------------------------------------
1.Import & Setup:
---------------------
![image](https://github.com/user-attachments/assets/31f37fd5-dd7f-4097-b2cc-7a8bcac27c43)


2.LangChain & Model Setup:
---------------------------
![image](https://github.com/user-attachments/assets/0b62a493-a502-4fd0-8bd4-ace8e90137a5)

3.Configuration:
-------------------
![image](https://github.com/user-attachments/assets/717b09c6-66af-4c4d-bd57-dc99650d298c)

4.Authentication:
-------------------
![image](https://github.com/user-attachments/assets/3afa5746-b492-433d-a4f2-832b7a0bb97f)

5.Function: initialize_components():
------------------------------------
Initializes the LLM and vector store if not already created.

![image](https://github.com/user-attachments/assets/cf71214b-42d7-4e37-b2f1-6adfabc87e93)

6.Function: process_urls(urls):
-------------------------------
• Loads data from URLs.

• Splits into small readable chunks.

• Converts to embeddings and stores in Chroma DB.

![image](https://github.com/user-attachments/assets/d1d22213-af1d-4612-9227-c8b5a1b9710b)

7.Function: generate_answer(query):
-----------------------------------
![image](https://github.com/user-attachments/assets/0a81b448-92f8-4c92-a4a4-a07b31b01d75)

8.Sample Run (for testing):
----------------------------
![image](https://github.com/user-attachments/assets/bfa4e3a6-7293-4ea6-86f6-afdf5b0f0998)

-------------------------------------------------------------------------------------------------------------------------------------------------------------
➤ How RAG Works Here:
-------------------------
◘ Input: You enter one or more URLs.

◘ Scraping: Content is fetched using UnstructuredURLLoader.

◘ Chunking: Text is split using RecursiveCharacterTextSplitter.

◘ Embedding: Each chunk is embedded using Hugging Face models.

◘ Storing: Vectors are stored in a Chroma vector database.

◘ Querying: You ask a question, and the system retrieves relevant chunks.

◘ Answering: LLM answers your question using context retrieved from chunks.

➤ Components Overview:
------------------------
➭ LLM	llama-3-3-70b-versatile from Groq (via ChatGroq)

➭ Embedding	Alibaba-NLP/gte-base-en-v1.5 from Hugging Face

➭ Vector Store	Chroma – Local persistent vector database to store and retrieve chunks

➭ Loader	UnstructuredURLLoader – Extracts clean text from web URLs

➭ Text Splitter	RecursiveCharacterTextSplitter – Splits content into small meaningful chunks

-------------------------------------------------------------------------------------------------------------------------------------------------------
➤ main.py - Streamlit frontend code for the Smart URL Answer Bot:
------------------------------------------------------------------

![image](https://github.com/user-attachments/assets/eea57192-7ee3-4176-a2f5-0a3714cb31ee)
![image](https://github.com/user-attachments/assets/0090ae9c-65d0-4743-afc2-4d02d29cd059)
![image](https://github.com/user-attachments/assets/d3806acc-9d66-4636-a143-3bd07446b330)
![image](https://github.com/user-attachments/assets/339bc55b-4fa8-4afb-b691-236ab6a70eb4)
![image](https://github.com/user-attachments/assets/d145a9d5-66a7-4898-9dba-e874f7becf49)

Summary of This Code:
--------------------------------
◘ st.sidebar.toggle("🌙 Dark Mode") - 	Adds dark mode toggle.

◘ CSS via st.markdown(<style>) -	Dynamically sets styles for both light and dark modes.

◘ process_urls(urls) - Backend function to scrape and vectorize content.

◘ generate_answer(query)	- LLM query run using RAG.

◘ .answer-card -	Result box with purple border and background.

URLs to Test:
-------------
https://www.indiatoday.in/india

https://www.ndtv.com/latest

https://www.bbc.com/news/world/asia/india

Sample Questions:
----------------
What is the latest update on the Indian elections?

What did the Prime Minister say today?

Any international news involving India?

![image](https://github.com/user-attachments/assets/49ef2a0c-293b-4887-bf59-3a93f4f73641)


![image](https://github.com/user-attachments/assets/06677b54-a7a3-4a38-a178-6f8ea8707d97)

This command is to clear resources(vector):
----------------------------------------------
![image](https://github.com/user-attachments/assets/1e8bea4a-ea0f-46c5-a67f-1a8741b863f9)
