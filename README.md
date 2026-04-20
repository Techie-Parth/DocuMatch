# Document Template Matcher Node.js

This is a separate Node.js version of the corrected project idea. It does not disturb the existing Python/FastAPI project.

## Project idea

The system stores templates in categories such as:

- Research Paper
- CV
- Certificate
- Letter
- Invoice

When a user uploads a document, the backend detects the document type using document keywords and returns only the templates from the same category.

Examples:

- Upload a research paper: only research paper templates are shown.
- Upload a CV: only CV templates are shown.
- Upload a certificate: only certificate templates are shown.

## Run

```bash
cd document-template-node
npm start
```

Open:

```text
http://localhost:5000
```

## Deploy

### Render

1. Push this project to GitHub.
2. Create a new Render Web Service from the repo.
3. Render will detect [render.yaml](./render.yaml) automatically.
4. Deploy the service.

This project stores templates and uploaded files on disk. The included `render.yaml` mounts persistent storage at `/var/data` and sets `DATA_DIR=/var/data`.

### Railway

1. Push this project to GitHub.
2. Create a new Railway project from the repo.
3. Add a Volume and mount it at `/var/data`.
4. Add an environment variable: `DATA_DIR=/var/data`.
5. Deploy the service.

Railway will use [railway.json](./railway.json) for the start command. The app will automatically create `templates.json` inside the mounted data folder if it does not exist, and it will seed it from the bundled templates on first boot.

## API

### Match uploaded document

```text
POST /api/match
```

Multipart form field:

```text
document
```

### List templates

```text
GET /api/templates
```

### Add template

```text
POST /api/templates
```

Multipart form fields:

```text
name
category
description
templateFile
```

## Note

This version uses simple keyword-based classification with lightweight DOCX text extraction. For a stronger final-year version, you can later replace the classifier with ML/NLP and use a dedicated parser for PDF and DOC files.
