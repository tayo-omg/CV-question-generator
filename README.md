# CV-question-generator
# CV Claim-Based Interview Question Generator

A Python API that extracts professional claims from an uploaded CV and generates concise, claim-based interview questions.

The project demonstrates document processing, prompt design, structured AI responses, file validation and REST API development using FastAPI.

## Features

- Accepts CVs in PDF and DOCX formats.
- Extracts text from PDF pages, Word paragraphs and tables.
- Identifies verifiable claims about:
  - technical skills;
  - employment responsibilities;
  - projects;
  - measurable achievements;
  - leadership experience;
  - qualifications and certifications.
- Generates 15–20 claim-based interview questions.
- Randomly selects 10 unique questions.
- Limits each question to 20 words.
- Classifies questions as Easy, Medium or Hard.
- Provides expected answer points.
- Identifies possible red flags in candidate responses.
- Rejects unsupported, empty or oversized files.
- Avoids questions about protected personal information.

## Technologies Used

- Python
- FastAPI
- Pydantic
- OpenAI API
- pypdf
- python-docx
- Uvicorn

## Project Structure

```text
cv-question-generator/
├── cv_question
├── .env
├── .gitignore
├── requirements.txt
└── README.md
```

## Installation

Clone the repository:

```powershell
git clone <https://github.com/tayo-omg/CV-question-generator>
cd <cv¬question>
```

Create a virtual environment:

```powershell
python -m venv venv
```

Activate the virtual environment in PowerShell:

```powershell
.\venv\Scripts\Activate.ps1
```

Install the required packages:

```powershell
python -m pip install fastapi uvicorn openai python-dotenv python-docx pypdf python-multipart
```

Alternatively, install them from `requirements.txt`:

```powershell
python -m pip install -r requirements.txt
```

## Environment Variables

Create a `.env` file in the main project folder:

```env
OPENAI_API_KEY=your_openai_api_key
OPENAI_MODEL=your_supported_model
```

Do not upload your `.env` file to GitHub.

Add the following to `.gitignore`:

```gitignore
.env
venv/
__pycache__/
*.pyc
```

## Running the Application

From the main project folder, run:

```powershell
python -m uvicorn src.cv_questions.api:app --reload
```

Open the interactive API documentation:

```text
http://127.0.0.1:8000/docs
```

## API Endpoints

### Health Check

```http
GET /health
```

Example response:

```json
{
  "status": "healthy",
  "service": "cv-question-api"
}
```

### Generate Interview Questions

```http
POST /cv/questions
```

Upload a PDF or DOCX file through the `cv` form field.

Example response:

```json
{
  "filename": "sample_cv.pdf",
  "claims": [
    "Led a team that recovered debts exceeding N300 million."
  ],
  "questions": [
    {
      "claim": "Led a team that recovered debts exceeding N300 million.",
      "question": "How did you lead your team to recover over N300 million?",
      "expected_points": [
        "Explain the candidate's leadership role",
        "Describe the recovery approach",
        "Explain how the result was measured"
      ],
      "difficulty": "Medium",
      "red_flags": [
        "Cannot explain personal contribution",
        "Provides inconsistent details",
        "Cannot support the reported result"
      ]
    }
  ]
}
```

## Response Fields

| Field | Description |
|---|---|
| `claim` | A professional statement extracted from the CV. |
| `question` | A short interview question connected to the claim. |
| `expected_points` | Two to four points a strong answer should address. |
| `difficulty` | The question level: Easy, Medium or Hard. |
| `red_flags` | Warning signs to watch for in the candidate’s answer. |

## File Validation

- Supported formats: PDF and DOCX.
- Maximum file size: 5 MB.
- Empty files are rejected.
- Files containing very little extractable text are rejected.
- Image-only scanned CVs are not supported because OCR is not included.

## Skills Demonstrated

This project demonstrates:

- REST API development with FastAPI;
- PDF and DOCX text extraction;
- file upload and validation;
- exception and HTTP error handling;
- prompt engineering;
- structured AI output using Pydantic;
- Python type annotations;
- environment-variable management; and
- privacy-conscious recruitment tooling.

## Responsible Use

This application supports interview preparation and does not make hiring decisions.

Generated questions should be reviewed by a qualified interviewer. Users should obtain appropriate permission before processing real CVs and should not upload candidate information or API credentials to the repository.

## Portfolio Notice

This repository presents a standalone demonstration of a CV-question generation component. It does not contain employer data, candidate records, production credentials or unrelated workplace systems.
