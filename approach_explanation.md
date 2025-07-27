# Approach Explanation: Persona-Driven Document Intelligence System

## Methodology Overview

Our system implements a three-tier intelligent document analysis approach that combines advanced NLP techniques with multi-factor relevance scoring to deliver precise, persona-driven results.

## Core Architecture

### 1. Advanced Query Understanding (Tier 1)
We deconstruct the persona and job-to-be-done into structured components using NLP techniques:
- **Core Entities Extraction**: Identifies key nouns (e.g., "literature review", "revenue trends", "reaction kinetics")
- **Constraint Analysis**: Separates positive constraints (desired attributes) from negative constraints (what to avoid)
- **Context Inference**: Determines group size, urgency, complexity, and domain-specific requirements

This structured understanding enables the system to work universally across any domain without hardcoded rules.

### 2. Multi-Factor Relevance Scoring (Tier 2)
We implement a weighted scoring formula that combines four critical factors:
```
Final Score = (0.4 × Semantic_Score) + (0.3 × Keyword_Score) + (0.2 × Title_Score) - (0.1 × Penalty_Score)
```

- **Semantic Score**: Cosine similarity using Sentence Transformers (all-MiniLM-L6-v2) for thematic relevance
- **Keyword Score**: Direct matching of core entities and positive constraints
- **Title Score**: Heavy bonus for keywords appearing in section titles
- **Penalty Score**: Deduction for negative constraint violations

This approach ensures both broad thematic relevance and specific detail matching.

### 3. Intelligent Content Extraction (Tier 3)
For sub-section analysis, we perform sentence-level scoring within top-ranked sections:
- Score each sentence based on core entities and constraints
- Extract top 2-3 highest-scoring sentences
- Combine into concise, actionable refined text

## Technical Implementation

**Model**: Sentence Transformers (all-MiniLM-L6-v2) - 90MB, CPU-optimized
**NLP Library**: NLTK for tokenization and entity extraction
**Processing**: PyMuPDF for robust PDF text extraction
**Scoring**: Custom multi-factor algorithm with configurable weights

## Universal Compatibility

The system achieves domain-agnostic operation through:
- Dynamic constraint extraction from user queries
- No hardcoded domain-specific keywords
- Adaptive scoring based on query structure
- Flexible content extraction patterns

## Performance Characteristics

- **Model Size**: 90MB (well under 1GB limit)
- **Processing Time**: ~30 seconds for 9 documents (under 60-second limit)
- **CPU-Only**: No GPU dependencies
- **Offline Operation**: All processing local, no internet required

## Validation Results

Tested across multiple domains:
- **Academic Research**: Correctly prioritizes methodology and benchmark sections
- **Business Analysis**: Accurately identifies financial trends and strategic content
- **Educational Content**: Effectively extracts key concepts and mechanisms

The system demonstrates consistent performance across diverse document types, personas, and job requirements, making it truly universal for any hackathon challenge. 