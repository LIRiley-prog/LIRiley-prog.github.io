[Back to Portfolio](./)

PDF Citation Parser
===================

-   **Class:** CSCI 325 – Object-Oriented Programming
-   **Grade:** C+
-   **Language(s):** Python (Backend), JavaScript/React (Frontend), Flask
-   **Source Code Repository:** [csci495-Fall25-greenTeam-citationParser](https://github.com/LIRiley-prog/csci495-Fall25-greenTeam-citationParser)  
    (Please [email me](mailto:Liriley@csustudent.net?subject=GitHub%20Access) to request access.)

## Project Description

The PDF Citation Parser is a full-stack web application developed as a team project (Green Team) for CSCI 325 – Software Engineering. The application allows users to upload academic PDF documents and automatically extract and parse citation references from them.

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

## Additional Considerations

This project was developed using Agile methodology with a team of students. My role as part of the Green Team involved contributing to both the backend PDF processing pipeline and integration with the React frontend. The project demonstrates real-world software engineering practices including team collaboration, API design, automated build tooling, and full-stack development.

[Back to Portfolio](./)
