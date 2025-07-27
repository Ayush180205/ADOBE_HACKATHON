# Execution Instructions

## Docker Setup and Execution

### 1. Build the Docker Image
```bash
docker build -t hackathon-document-intelligence .
```

### 2. Prepare Input Files
Place your input files in the project directory:
- `input.json` - Challenge specification
- `documents/` - PDF files (if using real PDFs)
- `input_json_dir/` - JSON files (if using pre-processed JSON)

### 3. Run the Container

#### Option A: Using Docker Run
```bash
docker run -v $(pwd):/app hackathon-document-intelligence
```

#### Option B: Interactive Mode
```bash
docker run -it -v $(pwd):/app hackathon-document-intelligence bash
```

### 4. View Results
After execution, results will be available in:
- `output_dir/output_[persona].json` - Main output

## Local Execution (Without Docker)

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Run Processing
```bash
python process_input.py
```

## Input Format

### input.json Structure
```json
{
  "challenge_info": {
    "challenge_id": "round_1b_001",
    "test_case_name": "menu_planning",
    "description": "Dinner menu planning"
  },
  "documents": [
    {
      "filename": "document1.pdf",
      "title": "Document 1"
    }
  ],
  "persona": {
    "role": "Food Contractor"
  },
  "job_to_be_done": {
    "task": "Prepare a vegetarian buffet-style dinner menu"
  }
}
```

## Output Format

The system generates `output_[persona].json` with:
- **Metadata**: Input documents, persona, job, timestamp
- **Extracted Sections**: Top 10 relevant sections with importance ranking
- **Sub-section Analysis**: Detailed analysis of top 5 sections

## Performance Specifications

- **Model Size**: 90MB (under 1GB limit)
- **Processing Time**: ~30 seconds for 9 documents (under 60-second limit)
- **CPU-Only**: No GPU required
- **Offline**: No internet access needed

## Troubleshooting

### Common Issues
1. **Permission Errors**: Use `sudo` for Docker commands
2. **Volume Mount Issues**: Ensure correct path mapping
3. **Memory Issues**: System has sufficient RAM (4GB+ recommended)

### Logs
Check container logs with:
```bash
docker logs <container_id>
```

## Validation

Test the system with provided sample data:
```bash
# Run with sample input
python process_input.py
```

The system is designed to work universally across any domain, persona, and job requirement as specified in the hackathon challenge. 