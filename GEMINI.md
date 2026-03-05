# Project Overview

`clinique_to_do` is a web-based, interactive medical observation ecosystem designed for practitioners and students. It bridges the gap between bedside examination and formal clinical reporting, offering a mobile-optimized checklist and a desktop-based report generator with integrated medical decision support (mnemonics, scores, and biological reference ranges).

# Key Components

*   **`index.html` (Navigation Hub):**
    *   **Search & Autocomplete:** Uses a JavaScript `specialtyMap` to route users to specialty-specific templates (e.g., `ccv`, `hemato`, `radio`).
    *   **Unified Access:** Provides one-click access to the two primary modes (Mobile Checklist vs. Desktop Generator).
*   **`simplechecklist.html` (Mobile Bedside Tool):**
    *   **UX Design:** Features a "Floating Island" header with progress tracking, real-time date/time, and quick links to external reference PDFs.
    *   **Interactive Flow:** Organized by clinical systems (General, Abdominal, Cardio, Neuro, etc.) with integrated logic for conditional field visibility (e.g., selecting a situation familial automatically updates checkboxes).
*   **`observation.html` (Comprehensive Report Generator):**
    *   **Technology:** Leverages `docx.js` for client-side generation of professional clinical reports.
    *   **Medical Logic:**
        *   **Mnemonics:** Integrated "SITI FADMA" (Siège, Irradiation, Type, Impact, Facteurs, Accalmie, Durée, Mode, Amélioration) for pain characterization and "3A + F" (Asthénie, Anorexie, Amaigrissement + Fièvre) for general signs.
        *   **Scoring Systems:** Automated Age calculation from DOB, IMC/BMI calculator, and ECOG/OMS Performance Status picker.
        *   **Biological Validator:** A structured paraclinical section with real-time validation against reference ranges (Normal/Low/High color-coding) for Hematology, Ionograms, Renal/Hepatic function, etc.
    *   **Export Options:** Supports "Word (.docx)" export and "Google Docs" clipboard integration for seamless transition to hospital EMRs.

# Project Structure

*   **`services/`**: Specialized templates.
    *   `ccv/`, `hemato/`, `radio/`: Each contains a specialty-specific `.html` file and a `ressources/` folder for niche clinical data.
*   **`observation_ressources/`**: Asset library for the main generator, organized by section (0. Clinician Info to 8. Prescription).
*   **`simplechecklist_ressources/`**: Source text and PDFs used for the mobile version's logic and content.
*   **`clinXpert/`**: Foundational reference library. Contains the core "Guide de l'examen clinique" (PDF/DOCX) and specific clinical notes for every major system.
*   **`other/`**: Development metadata.
    *   `plan.txt` & `idea.txt`: Roadmap for features like multi-service expansion and export refinement.
    *   `documentation.txt`: The structural blueprint for the observation logic (Identity -> History -> Exam -> Conclusion).

# Clinical Methodologies Integrated

The project enforces standard semiological practices:
1.  **Administrative Anamnesis:** Detailed patient profiling including social coverage (AMO/CNSS/CNOPS/etc.).
2.  **Symptom Characterization:** Systematic breakdown of the "Histoire de la Maladie" using standardized descriptors.
3.  **Physical Examination:** Systematic "Inspection, Palpation, Percussion, Auscultation" (IPPA) workflow.
4.  **Differential Diagnosis:** A dedicated hypothesis table for weighing arguments "Pro" and "Contra" each diagnostic possibility.

# Development Goals

1.  **Specialty Completion:** Expanding the `services/` directory to cover all modules in the "Livret Vert" and "Guide de l'externe".
2.  **Enhanced Export:** Improving the styling of the generated `.docx` files to match official hospital observation headers.
3.  **Cross-Reference Integration:** Mapping the `clinXpert` library directly into the checklists as context-sensitive help icons.
