# Medical-Question-Answering-System

#### Drive link-> https://drive.google.com/drive/folders/13D0_qNBPOnrdsGr805OGqKDqvuSIBxhu?usp=sharing
### Overview
This project develops a domain-specific Medical Question Answering system capable of understanding natural language medical queries and providing accurate, contextually relevant answers.
The system integrates:
Advanced Language Models (BioBART)

1.Retrieval-Augmented Generation (RAG) for context retrieval

2.Recognizing Question Entailment (RQE) for enhanced answer grounding

3.FAISS for fast semantic similarity search.

### Problem Statement
With the increasing volume of medical queries on the internet, finding accurate and trustworthy information is challenging. Manual searches can be overwhelming and often lead to misinformation due to the complexity and vastness of medical data.
Our goal is to create a medical-domain QA system that reduces this gap and provides reliable answers.

### Dataset Overview
#### Source: Medical QnA dataset
#### Features:
qtype – question category (e.g., symptoms, treatment)
Question – raw medical question
Answer – raw medical answer
#### Statistics:
Total Entries: 16,407
Unique Questions: 14,979
Unique Answers: 15,817
Question types: 16 categories (symptoms, treatment, causes, etc.)
Questions with multiple answers: 875
###  Data Preprocessing
Load dataset & inspect basic stats
Analyze question types
Remove duplicates (Q-A pairs)
Text cleaning:
Lowercasing
Removing special characters & stopwords
Lemmatization
Normalize categories (qtype)
Save processed dataset as med_procees_cleaned.csv
### System Architecture
 Baseline (RAG)
Model: multi-qa-MiniLM-L6-cos-v1 for embeddings

Retriever: FAISS (cosine similarity)

Generator: BioBART (GanjinZero/biobart-base)

### Pipeline:

Question → Retrieve top-k similar answers → Generate answer

Enhanced (RAG + RQE)

RQE Integration: Retrieve semantically similar QA pairs using Recognizing 
Question Entailment

Pipeline:

Question → Retrieve top-k contexts + RQE QA pairs → Generate enriched answer

 #### Implementation Steps
1. Context Retrieval with FAISS
Encode cleaned questions & answers

#### Build FAISS index

Retrieve top-k (k=3) relevant answers as context

2. RQE-based Context Augmentation
Identify related questions using entailment

Add retrieved Q-A pairs to model input for richer context

### 3. Model Training
Model: Seq2Seq LM (BioBART)

Optimizer: AdamW (lr=2e-5)

Epochs: 3

Loss Function: Cross-entropy (PAD tokens ignored)

Batching: Custom PyTorch Dataset & DataLoader

### Results
Metric	Baseline (RAG)	RAG + RQE	Improvement

Exact Match	53.21%	61.47%	+8.26%

F1 Score	66.04%	73.29%	+7.25%

BLEU	43.88	49.52	+5.64

ROUGE-L	59.10	65.23	+6.13
