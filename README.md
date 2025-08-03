# GATE DSAI AI-Powered Study Tutor

This project implements a sophisticated Retrieval-Augmented Generation (RAG) pipeline to create a personalized AI tutor for the GATE Data Science & Artificial Intelligence (DSAI) exam. The system leverages a custom knowledge base of PDF study materials to provide accurate, context-aware answers to complex technical questions.

This chatbot is designed to be an intelligent study partner, helping aspirants to query their notes, understand concepts in depth, and get quick, evidence-based answers.

## ✨ Features

-   **Personalized Knowledge Base:** Answers questions based *only* on your provided PDF study materials (textbooks, notes, question papers, etc.).
-   **State-of-the-Art AI Models:** Utilizes a top-tier embedding model (`BAAI/bge-m3`) for superior document retrieval and a powerful LLM (`mistralai/Mistral-7B-Instruct-v0.1`) for high-quality answer generation.
-   **GPU Accelerated:** Optimized to run on a GPU for fast, interactive responses.
-   **Source Verification:** For every answer, the tutor provides the source document(s) it used, allowing for easy verification.
-   **Modular & Efficient:** A two-notebook system separates the time-consuming index-building process from the fast, interactive chatbot session.

## 🛠️ Technology Stack

-   **Programming Language:** Python 3.10
-   **Core Framework:** LangChain
-   **LLM (Answer Generation):** `mistralai/Mistral-7B-Instruct-v0.1`
-   **Embedding Model (Retrieval):** `BAAI/bge-m3`
-   **Vector Store:** FAISS (Facebook AI Similarity Search)
-   **PDF Processing:** PyMuPDF
-   **Environment:** Kaggle Notebooks (with GPU acceleration)
-   **Core Libraries:** Transformers, PyTorch, Accelerate

## 📂 Project Structure

```
.
├── Gate_DSAI/
│   ├── Artificial-Intelligence/
│   │   └── ... (your PDFs)
│   ├── Machine-Learning/
│   │   └── ... (your PDFs)
│   └── ... (other subject folders)
│
├── build_index.ipynb       # Notebook to process PDFs and create the vector index (Run Once)
└── gate-dsai-prep-llm.ipynb           # Main notebook to load the index and chat with the tutor (Run Anytime)
```

## 🚀 Getting Started

This project is designed to be run in a Kaggle Notebook environment to leverage free GPU access.

### Prerequisites

-   A Kaggle account.
-   Your collection of GATE DSAI study materials in PDF format, organized into folders.

### Step 1: Create a Kaggle Dataset

First, you need to upload your study materials as a private dataset on Kaggle.

1.  Go to Kaggle, click **Create**, and then **New Dataset**.
2.  Give your dataset a title, for example, `gate-dsai-llm`.
3.  Upload your entire `Gate_DSAI` folder containing all the subject sub-folders and PDFs.

### Step 2: Set Up the Index-Building Notebook

This notebook will read all your PDFs and create the vector index (the chatbot's "brain"). You only need to run this once.

1.  Create a new Kaggle Notebook.
2.  On the right-hand side, under **Settings**, set the **Accelerator** to **GPU T4 x2**.
3.  Click **"+ Add Data"** and add the Kaggle Dataset you created in Step 1. Your data will be available at a path like `/kaggle/input/gate-dsai-llm/Gate_DSAI`.
4.  Copy the code from the `build_index.ipynb` file into a cell and run it. This will take some time as it processes all your documents.
5.  After it completes successfully, it will create a new folder in your output directory: `/kaggle/working/my_vector_index`.

### Step 3: Set Up the Chatbot Notebook

This is the main notebook you will use for your study sessions.

1.  Create a second Kaggle Notebook.
2.  Enable the **GPU T4 x2** accelerator, just as you did before.
3.  Add your Kaggle Dataset containing the PDFs.
4.  **Important:** You also need to add the output from your first notebook. Click **"+ Add Data"**, go to the **"Notebook Output Files"** tab, find your `build_index` notebook, and add its output. This will make the `my_vector_index` folder available at `/kaggle/input/[your-notebook-name]/my_vector_index`.
5.  Copy the code from the `gate-dsai-prep-llm.ipynb` file into a cell.
6.  **Update the path:** In the chatbot code, make sure the `index_path` variable points to the correct location of your saved index from the previous step.
7.  Run the cell. The chatbot will initialize and you can start asking questions!

## 🤖 Example Interaction

```
--- GATE DSAI TUTOR IS READY ---

🤔 Your Question: "What is the primary key in a relational database?"

Here's what I found in your study materials:
---------------------------------------------------------
✅ ANSWER: A primary key is a constraint that uniquely identifies each record in a table. It must contain unique values and cannot contain NULL values. A table can have only one primary key, which may consist of single or multiple fields.
🔍 EVIDENCE: "A primary key is a field in a table which uniquely identifies each row/record in a database table."
📂 SOURCE(S): /kaggle/input/gate-dsai-llm/Database-Management/Fundamentals-of-Database-Systems-Elmasri-Navathe.pdf
---------------------------------------------------------

Here is a preview of the section(s) I used for context:
................................
A primary key is a field in a table which uniquely identifies each row/record in a database table. Primary keys must contain unique values. A primary key column cannot have NULL values. A table can have only one primary key, which may consist of single or multiple fields. When multiple fields are used as a primary key, they are called a composite key...
................................
```

## 💡 Future Improvements

-   **Web Interface:** Build a simple web interface using Gradio or Streamlit to make the chatbot more user-friendly.
-   **Conversation History:** Implement memory to allow for follow-up questions.
-   **Advanced Retrieval:** Experiment with more advanced retrieval strategies like HyDE (Hypothetical Document Embeddings) or Parent Document Retrievers for more complex queries.

## 📄 License

This project is licensed under the MIT License. See the `LICENSE` file for details.

