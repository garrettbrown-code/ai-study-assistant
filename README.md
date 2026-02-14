# AI Study Assistant Pipeline

A multi-stage document ingestion and AI orchestration system that transforms textbook PDFs into structured plaintext and generates adaptive quizzes, scoring, and personalized review summaries.

---

## Overview

This project implements an ETL-style pipeline for educational content:

PDF → Text Extraction → Cleaning & Segmentation → LLM Question Generation → Scoring → Adaptive Review

The goal is to convert unstructured textbook content into structured, machine-readable sections and use AI to dynamically assess and improve user understanding.

---

## System Architecture

PDF  
↓  
PyMuPDF Text Extraction  
↓  
Regex-Based Cleaning & Segmentation  
↓  
Structured Section Storage  
↓  
OpenAI API (Question Generation + Scoring)  
↓  
Progress Tracking (JSON Persistence)  

---

## Core Features

### Document Ingestion
- Extracts text from PDF using PyMuPDF
- Detects chapter and section mappings
- Associates pages via footer markers
- Removes headers, footers, URLs, references, and noise
- Normalizes whitespace and special characters
- Preserves structured chapter/section hierarchy

### AI Integration
- Generates structured quiz and exam questions (JSON-only format)
- Supports multiple choice and short answer
- Scores user responses (0–10 scale)
- Provides explanatory feedback
- Generates adaptive summaries weighted toward weak topics

### Adaptive Learning Workflow
- Identifies low-scoring questions
- Extracts weak-topic prompts
- Generates targeted remediation summaries
- Tracks cumulative chapter progress

### Resilient API Handling
- Supports multiple OpenAI SDK response formats
- Implements JSON extraction fallback logic
- Handles malformed AI responses safely

---

## Tech Stack

- Python
- PyMuPDF (fitz)
- OpenAI API
- JSON
- Regex
- File I/O

---

## Running the Project

### 1. Clone repository

```
git clone https://github.com/yourusername/ai-study-assistant.git
cd ai-study-assistant
```

### 2. Create virtual environment

```
python -m venv venv
source venv/bin/activate  # macOS/Linux
venv\Scripts\activate     # Windows
```

### 3. Install dependencies

```
pip install -r requirements.txt
```

### 4. Create environment file

Create a `.env` file:

```
OPENAI_API_KEY=your_api_key_here
```

### 5. Run ingestion pipeline

```
python ingestion/pdf_parser.py
```

### 6. Run interactive chapter processor

```
python ai_orchestration/quiz_generator.py
```

---

## Key Engineering Concepts Demonstrated

- ETL-style pipeline design
- Text normalization and parsing
- Regex-based data cleaning
- Structured JSON enforcement
- AI API orchestration
- Error handling and fallback logic
- Progress persistence and state management

---

## Future Improvements

- Web interface (Flask or FastAPI frontend)
- Database-backed progress tracking
- Docker containerization
- Background task processing
- Rate limiting and retry handling
- Unit testing for ingestion pipeline

---

## License

MIT License
