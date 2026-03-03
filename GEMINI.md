# Project Overview

`clinique_to_do` is a web-based, interactive medical observation checklist designed for medical practitioners and students. It ensures that essential points are covered during patient consultations and examinations, providing both a quick mobile reference and a comprehensive desktop report generator.

# Key Components

*   **`index.html` (The Hub):** The central entry point. It features:
    *   Direct links to the Simple and Normal checklists.
    *   A search bar with autocomplete for specialized specialty-specific templates.
    *   Resource toggles for external clinical guides.
*   **`documentation.txt`**: A high-level outline and checklist for building the clinical observation sections (Patient Identity, History, Clinical Exam, Paraclinical, etc.).
*   **`simplechecklist.html` (Mobile Optimized):** A lightweight, responsive version designed for quick use on mobile devices during ward rounds or bedside examinations.
*   **`observation.html` (Comprehensive Desktop):** A full-featured version for general practitioners, focusing on detailed clinical observation and report generation. Includes features for data export (DOCX/Google Docs integration).

# Project Structure

*   **`services/`**: Contains specialized checklist templates for various medical specialties.
    *   Each subfolder (e.g., `ccv/`, `hemato/`, `radio/`) contains a specialty-specific `.html` template and a `ressources [spe]/` folder for related clinical materials.
*   **`observation_ressources/`**: A structured directory containing the assets and data required for each section of the Normal Checklist (e.g., identity, history, physical exam).
*   **`simplechecklist_ressources/`**: Source materials, including PDFs and text extractions, used to build and update the simple mobile-optimized checklist.
*   **`clinXpert/`**: A collection of foundational clinical reference materials, including the "Guide de l'examen clinique", models of clinical observations, and specialized examination notes.
*   **`other/`**: Contains project documentation, development plans, and auxiliary files:
    *   `plan.txt`: Development roadmap and structural objectives.
    *   `idea.txt`: Feature brainstorming and future improvements.
    *   `documentation old.docx`: Earlier versions of the documentation.
*   **`backup/`**: Historical versions and archival files for reference. **Note:** Do not modify or delete these files.

# Development Status & Goals

The project is currently focusing on:
1.  **Mobile Optimization:** Ensuring the `simplechecklist.html` is fully responsive and bedside-ready.
2.  **Export Features:** Enhancing `observation.html` with better export capabilities (improving DOCX output and Google Docs clipboard integration).
3.  **Specialty Expansion:** Populating the `services/` directory with templates for all major medical specialties (Cardiology, Neurology, etc.) based on standard clinical guidelines.
4.  **Index Refinement:** Implementing a robust search and autocomplete system in `index.html` for easy access to specialty templates.

# Usage

*   **Quick Check:** Use `simplechecklist.html` on a mobile device for a fast bedside reference.
*   **Full Report:** Use `observation.html` on a desktop to generate a complete clinical observation record.
*   **Specialty Templates:** Access specific templates via the search/dropdown on `index.html` or by navigating to the corresponding folder in `services/`.
