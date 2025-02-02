# PDF Chatbot with Vector Search and AWS Deployment

## Project Overview
This project implements a **PDF-based chatbot** that extracts text from PDFs, processes the text using **vectorization techniques**, and retrieves the most relevant responses based on user queries. It utilizes **Retrieval-Augmented Generation (RAG)** and **Vector Databases** to enhance the chatbot's response accuracy. The application is deployed on **AWS Lambda** with **S3, IAM, and Lambda Layers** for scalability.

## Technologies & Libraries Used
- **Programming Language:** Python
- **Libraries:**
  - `pdfplumber` - Extracting text from PDFs
  - `scikit-learn` - TF-IDF Vectorization and Cosine Similarity
  - `numpy` - Handling numerical computations
  - `pdfplumber` - Extracting data from PDFs
  - `boto3` - AWS SDK for managing S3 and Lambda
- **AWS Services:**
  - S3 (Storage)
  - Lambda (Serverless Execution)
  - IAM (Permissions Management)
  - Lambda Layers (Adding Dependencies)

## Features
1. **PDF Extraction:** Parses the PDF content using `pdfplumber`.
2. **Text Chunking:** Splits extracted text into meaningful chunks.
3. **Vectorization:** Converts text into numerical vectors using **TF-IDF**.
4. **Similarity Search:** Finds relevant responses using **Cosine Similarity**.
5. **Retrieval-Augmented Generation (RAG):** Retrieves relevant chunks for AI-generated responses.
6. **AWS Deployment:**
   - Stores PDFs in **S3**
   - Processes queries using **AWS Lambda**
   - Uses **IAM roles & permissions** for secure access

---

# Explanation of Core Concepts

## **1. PDF Data Extraction & Vectorization**
- **Extracting Data from PDF:**
  - `pdfplumber` is used to extract textual data from **scanned and digital PDFs**.
  - Text is then **chunked into segments** for efficient searchability.
- **Vectorization Technique:**
  - `TfidfVectorizer` from `sklearn` is used to transform text into **TF-IDF vectors**.
  - TF-IDF helps **weight words based on importance** rather than frequency alone.

## **2. Vector Databases & Techniques**
- **Why Use Vector Databases?**
  - Traditional databases are not effective in searching unstructured data like text.
  - Vector DBs store text as **high-dimensional embeddings** for **fast retrieval**.

- **Popular Vector Databases in the Industry:**
  - **FAISS (Facebook AI Similarity Search)** - Efficient, scalable, widely used.
  - **Pinecone** - Fully managed, real-time search.
  - **Weaviate** - Open-source, integrates with machine learning models.
  - **ChromaDB** - Lightweight, designed for AI applications.
  - **Milvus** - High-performance, distributed, open-source.
  - **Qdrant** - Scalable, cloud-native, integrates with deep learning.

## **3. Retrieval-Augmented Generation (RAG) and Its Types**
- **Standard RAG:** Uses a simple retrieval mechanism to fetch relevant documents.
- **Corrective RAG:** Enhances retrieval accuracy by refining retrieved knowledge.
- **Speculative RAG:** Uses **speculative retrieval & generation** simultaneously.
- **Fusion RAG:** Merges multiple sources of retrieved information.
- **Agentic RAG:** Uses intelligent agents for decision-making.
- **Self RAG:** Evaluates outputs in multiple iterations to ensure correctness.

## **4. Cosine Similarity for Relevance Search**
- Used to **compute similarity** between query and document vectors.
- Formula:
  \[ \text{cosine similarity} = \frac{A \cdot B}{||A|| ||B||} \]
- Helps in **ranking search results** based on relevance.

## **5. AWS Deployment & Lambda Setup**
### **Permissions & IAM Role Configuration**
- IAM Role grants Lambda access to **S3 & Vector Database**.
- Required IAM Permissions:
  - `s3:GetObject`
  - `s3:PutObject`
  - `lambda:InvokeFunction`
  - `logs:CreateLogGroup`
  - `logs:CreateLogStream`

### **Lambda Function Overview**
- Downloads PDF from **S3** to `/tmp/`
- Extracts text and **vectorizes** using TF-IDF.
- Finds **most relevant chunk** using **Cosine Similarity**.
- Returns **relevant passage** to the user.

### **Adding Dependencies via Lambda Layers**
- Scikit-learn is **not natively available** in AWS Lambda.
- Solution:
  - Use a pre-built **Lambda Layer** for `scikit-learn`.
  - Upload as a **ZIP file** to AWS and attach as a layer.

### **Testing the Lambda Function**
- Create a test event with JSON input:
```json
{
  "query": "What is this document about?"
}
```
- Invoke the function and check logs in **CloudWatch**.

---

## **6. Code Review for DataFrame Structure**
- **Initial Approach:** Saved extracted text **as CSV** after vectorization.
- **Refactored Approach:** Stored results in **memory (DataFrame object)**.
- **Comparison:** Verified that DataFrame **structure remained unchanged**.

---

## **7. Practical Applications of RAG**
- **Chatbots & Conversational AI**
- **Legal & Compliance Document Search**
- **Medical Research & Clinical Trials**
- **Financial Document Analysis**
- **Enterprise Knowledge Base Search**

---

## **Final Notes & Best Practices**
- Optimize **vector database indexing** for faster retrieval.
- Ensure **proper chunking** to avoid loss of context.
- Secure S3 access using **IAM Role Restrictions**.
- Monitor Lambda **execution time & memory usage** for cost efficiency.

### **Next Steps**
- Explore **hybrid search (keyword + vector search)**.
- Integrate **Large Language Models (LLMs) for generative responses**.
- Deploy **API Gateway** for external API access.

---

## **Conclusion**
This project successfully integrates **PDF processing, RAG, and vector databases** to build a scalable **document-based chatbot**. By leveraging **AWS Lambda & S3**, the solution is highly scalable, serverless, and cost-efficient. 🚀

