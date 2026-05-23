# CodeCraft (Flask + JSON)

A simple personalized learning platform backend built with Flask.

## Beginner-Friendly Project Structure

```text
CodeCraftHub/
  app/
    __init__.py        # App factory and route registration
    routes.py          # REST API endpoints (CRUD)
    storage.py         # JSON file read/write helpers
  data/
    courses.json       # JSON "database" file
  run.py               # Entry point
  requirements.txt     # Python dependencies
  README.md
```

## Setup and Run

```bash
python -m venv .venv
# Windows PowerShell
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python run.py
```

Server runs at: `http://127.0.0.1:5000`

## Course Data Model (JSON)

Each course is stored like:

```json
{
  "id": "generated-uuid",
  "course_name": "Python Basics",
  "description": "Learn Python fundamentals",
  "target_completion_date": "2026-06-30",
  "status": "In Progress"
}
```

Allowed `status` values:
- `Not Started`
- `In Progress`
- `Completed`

## REST API Endpoints

- `GET /` - Health check
- `GET /api/courses` - List all courses
- `GET /api/courses/<course_id>` - Get one course by ID
- `POST /api/courses` - Create a new course
- `PUT /api/courses/<course_id>` - Replace a course (all fields required)
- `PATCH /api/courses/<course_id>` - Partially update a course
- `DELETE /api/courses/<course_id>` - Delete a course

### Create Course Example

```bash
curl -X POST http://127.0.0.1:5000/api/courses \
  -H "Content-Type: application/json" \
  -d '{
    "course_name": "Flask Fundamentals",
    "description": "Build web APIs with Flask",
    "target_completion_date": "2026-07-15",
    "status": "Not Started"
  }'
```

## How Data Storage Works (No Database)

1. `load_courses()` ensures `data/courses.json` exists and reads it as a Python list.
2. API handlers modify that list in memory.
3. `save_courses()` writes the updated list back to `data/courses.json`.

This is ideal for learning and small local apps.
