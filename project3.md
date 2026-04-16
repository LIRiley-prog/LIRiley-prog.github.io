[Back to Portfolio](./)

PDF Citation Parser
===================

-   **Class:** CSCI 495 – Systems Analysis & Software Design
-   **Grade:** A
-   **Language(s):** Python (Backend), JavaScript/React (Frontend), Flask
-   **Source Code Repository:** [csci495-Fall25-greenTeam-citationParser](https://github.com/LIRiley-prog/csci495-Fall25-greenTeam-citationParser)  
    (Please [email me](mailto:Liriley@csustudent.net?subject=GitHub%20Access) to request access.)

## Project Description

The PDF Citation Parser is a full-stack web application developed as a team project (Green Team) for CSCI 495 – Systems Analysis & Software Design. The application allows users to upload academic PDF documents and automatically extract and parse citation references from them.

The backend is powered by **Python** and **Flask**, using the `pymupdf4llm` library to convert PDF content into structured Markdown format, which is then processed to identify and extract citation data. The frontend is built with **React**, providing a clean interface for uploading PDFs and viewing the parsed results. A **Makefile** automates environment setup, server startup, and testing.

This was a collaborative team project, giving practical experience in Agile software development, version control with Git, and full-stack web application architecture.

## How to Run the Program

```bash
# Set up environment and run the Flask server
make setup
make run

# Run tests
make test
```

The React frontend runs on `localhost:3000` and the Flask backend serves at `localhost:5000`.

## UI Design

The web application features a clean upload interface where users can:

- **Upload a PDF** — drag and drop or browse for an academic paper
- **Parse Citations** — the backend processes the PDF and extracts all reference citations
- **View Results** — parsed citations are displayed in a readable, structured list

The frontend dynamically updates as results are returned from the Flask API, providing a smooth user experience without page reloads.

## Code Snippets

### parse_pdf.py — Core PDF Processing Engine

```python
import re
import unicodedata
import pymupdf4llm
from flask import current_app
from pdf_database import db
from pdf_database.models import Papers, Body, Reference, Citations
from .find_citations import find_citations
from .parse_references import parse_references
from .split_text import paragraphize, sentenceify


def extract_body_text(text: str) -> str:
    """Extracts body text between the Introduction and Reference headers"""
    intro_match = re.search(r"(?im)^[#\s\*]*introduction[\s\*]*$", text)
    ref_match = re.search(r"(?im)^[#\s\*]*references[\s\*]*$", text)

    start_index = intro_match.end() if intro_match else 0
    end_index = ref_match.start() if ref_match else len(text)

    if start_index >= end_index:
        return ""
    return text[start_index:end_index].strip()


def fix_garbled_text(text: str) -> str:
    """Cleans leftover unicode still present in the markdown"""
    text = unicodedata.normalize('NFKC', text)
    mapping = {
        '\ue045': 'E', '\ue059': 'Y', '\ue04f': 'O',
        '\ue04e': 'N', '\ue043': 'C', '\ue055': 'U',
        '\ue047': 'G', '\ue04d': 'M',
    }
    return text.translate(str.maketrans(mapping))
```

### parse_pdf.py — ParsedPDF Class (Database Integration)

```python
class ParsedPDF:
    def __init__(self, filename, title):
        with current_app.app_context():
            self.count = dict()
            self.refs = dict()

            text = fix_garbled_text(
                pymupdf4llm.to_markdown(filename,
                    ignore_graphics=True,
                    ignore_images=True,
                    hdr_info=my_headers))

            # Check for existing paper or create new entry
            old_paper = db.session.execute(
                db.select(Papers).where(Papers.filename == filename)
            ).scalar()

            if old_paper:
                new_paper = old_paper
                new_paper.processing_status = "In Progress"
            else:
                new_paper = Papers(
                    filename=filename,
                    processing_status="In Progress",
                    title=title)

            db.session.add(new_paper)
            db.session.commit()

            # Parse references and citations
            for i, paragraph in enumerate(paragraphize(text)):
                body = Body(paper_id=new_paper.paper_id,
                           body_number=i,
                           body_paragraph=paragraph)
                db.session.add(body)
                db.session.commit()
                for sentence in sentenceify(paragraph):
                    for citation in find_citations(sentence):
                        db.session.add(Citations(
                            body_id=body.body_id,
                            reference_id=reference_entries[citation].reference_id,
                            sentence_content=sentence,
                            paragraph_content=paragraph,
                            llm_summary="TBD"))

            new_paper.processing_status = "Complete"
            db.session.commit()
```

## Additional Considerations

This project was developed using Agile methodology with a team of students. My role as part of the Green Team involved contributing to both the backend PDF processing pipeline and integration with the React frontend. The project demonstrates real-world software engineering practices including team collaboration, API design, automated build tooling, and full-stack development.

[Back to Portfolio](./)
