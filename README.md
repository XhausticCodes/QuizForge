# QuizForge

QuizForge is a simple AI study helper.

You upload your study file, and QuizForge creates:
- MCQ quizzes
- Flashcards

It is built as a college major project using Flask + SQLite + Groq API.

## What Problem It Solves

Most students read notes passively and forget quickly.  
QuizForge turns notes into active learning content (questions and flashcards) so revision becomes faster and smarter.

## Main Features

- User registration and login
- Upload study files (`pdf`, `png`, `jpg`, `jpeg`, `docx`, `pptx`)
- Auto text extraction from uploaded files
- AI quiz generation
- AI flashcard generation
- Quiz score saving
- History page (view/delete generated items)

## Tech Stack

- Python
- Flask
- SQLite
- Groq API (`llama-3.3-70b-versatile`)
- `pdfplumber`, `pytesseract`, `python-docx`, `python-pptx`

## Project Structure

```text
QuizForge-main/
├─ app.py                  # Main Flask app (routes + flow)
├─ database.py             # SQLite table creation + CRUD functions
├─ extractor.py            # Text extraction logic for different file types
├─ ai_generator.py         # Groq AI prompt + parsing logic
├─ templates/              # HTML pages
├─ static/                 # CSS/JS/assets
├─ uploads/                # Temporary uploaded files
├─ requirements.txt
└─ .env                    # API keys (not committed)
```

## How the App Works (End-to-End)

1. User registers or logs in.
2. User chooses mode: quiz or flashcards.
3. User uploads a file.
4. App checks file type and saves it.
5. App extracts text from the file.
6. App sends text to Groq model.
7. Model returns JSON output.
8. App stores results in SQLite.
9. User sees quiz/flashcards and can view history later.

## Local Setup

### 1) Clone repo

```bash
git clone https://github.com/XhausticCodes/QuizForge.git
cd QuizForge
```

### 2) Create virtual environment

On Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

### 3) Install dependencies

```powershell
pip install -r requirements.txt
pip install python-dotenv groq
```

### 4) Add environment variable

Create `.env` file in project root:

```env
GROQ_API_KEY=your_actual_groq_api_key
```

### 5) Run server

```powershell
.\.venv\Scripts\python app.py
```

Open:
- `http://127.0.0.1:5000`

## Notes for OCR

For image text extraction, Tesseract OCR must be installed on your system.  
Current code expects:

`C:\Program Files\Tesseract-OCR\tesseract.exe`

If your installation path is different, update it in `extractor.py`.

## Database Tables

- `users` -> stores name, email, hashed password
- `saved_quizzes` -> stores generated quiz JSON + score
- `saved_flashcards` -> stores generated flashcard JSON

## Security (Current + Improvements)

Current:
- Password hashing is used
- Protected routes require login
- File extension checks are implemented

Can be improved:
- Move Flask `secret_key` to `.env`
- Add CSRF protection
- Add better exception handling around AI JSON parsing

## Team Presentation Tip

Use this role split:
- Member 1: Backend flow (`app.py`)
- Member 2: AI generation (`ai_generator.py`)
- Member 3: File extraction (`extractor.py`)
- Member 4: Database + UI (`database.py` + templates)

---

If you are preparing for viva, check:
- `QuizForge_Viva_Rolewise_Handbook.docx`
