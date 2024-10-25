
# End-to-End NLP System for Pittsburgh and CMU

## Overview

This project focuses on building an end-to-end NLP system that performs data scraping, processing, and Q&A retrieval for information related to Pittsburgh and Carnegie Mellon University (CMU). The system gathers data from multiple sources, processes it into a vector-based database, and utilizes Retrieval-Augmented Generation (RAG) to provide accurate answers to user queries.

## Table of Contents

1. [Datasets Creation](#datasets-creation)
2. [Model Details](#model-details)
3. [Results](#results)
4. [Analysis & Improvements](#analysis--improvements)
5. [Usage Instructions](#usage-instructions)
6. [Future Enhancements](#future-enhancements)

## Datasets Creation

### 1. Pittsburgh and History
- **Source**: Wikipedia API
- **Content**: Historical data about Pittsburgh, extracted recursively from related pages. 
- **Output**: 1,673 text files about Pittsburgh and 290 files about its history.
- **Annotations**: 50 QA pairs generated.

### 2. CMU and CMU History
- **Source**: CMU website using Python libraries (requests, BeautifulSoup).
- **Content**: General information, athletics, admissions, academics, etc.
- **Output**: A folder with text files and URLs. Additionally, PDFs of CMU fact sheets were included.
- **Annotations**: 60 QA pairs generated.

### 3. Events in Pittsburgh and CMU
- Scraping of events from multiple sources, including the official CMU events calendar and Pittsburgh municipal event calendars.
- **Output**: Events compiled in CSV format with details such as event name, date, time, and location.
- **Annotations**: 100 QA pairs generated.

### 4. Cultural and Sports Data
- **Music and Culture**: Data about the Pittsburgh Symphony, Opera, and other cultural events.
- **Sports**: Data from official pages of Pittsburgh Pirates, Steelers, and Penguins, including historical achievements and schedules.
- **Annotations**: 104 QA pairs.

## Model Details

### 1. Vector Database Creation
- Utilized LangChain with Chroma for vector storage.
- **Model**: HuggingFace’s "all-MiniLM-L6-v2" for sentence embeddings.
- Data processed in batches to handle large files efficiently.

### 2. RAG Model Implementation
- Few-shot prompting to enhance Q&A response accuracy.
- Models Tested:
  - `meta-llama/Llama-2-7b-chat-hf`
  - `meta-llama/Llama-3-70b-chat-hf` (selected for better performance and concise responses).

### 3. Training and Evaluation
- Three systems were tested:
  - Baseline without retriever.
  - Basic retriever.
  - Retriever with training data.
- **Results**:
  - Error rates were reduced by 4% when incorporating training data.

## Results

- Baseline system struggled with up-to-date information.
- Basic retriever showed improvement in answering current event questions.
- Combining training data retriever improved overall accuracy.

## Analysis & Improvements

### Challenges
- Inconsistent retrieval for specific queries related to Pittsburgh Pirates and Pittsburgh Symphony due to incomplete or misclassified data.

### Proposed Improvements
- Implementing area-specific vector databases for better retrieval accuracy.
- Enhanced data collection for under-represented areas, such as detailed events or team roles.

## Usage Instructions

1. **Install Requirements**: 
   ```
   pip install -r requirements.txt
   ```
2. **Run Data Scraping**:
   - Use `crawler.ipynb` to collect data from specified sources.

## Future Enhancements

- **Increased Coverage**: Extend data scraping to more sources, especially for sports and music data.
- **Refined Prompting**: Adjust few-shot examples for better model adherence.
- **Parallel Processing**: Optimize data processing speed with parallel scraping.

