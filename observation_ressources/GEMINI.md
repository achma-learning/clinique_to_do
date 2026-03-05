# Observation Ressources: Modular Development Context

This folder serves as the modular staging area for the **ClinXpert** report generator (`observation.html`). The architectural strategy is to develop, refine, and test individual clinical sections as standalone HTML fragments before fusing them into the primary application.

## Core Role & Workflow

1.  **Modular Prototyping:** Each numbered HTML file (e.g., `1a_identite_patient.html`, `4_examen_clinique.html`) represents a self-contained section of the medical observation.
2.  **The "Fusion" Process:** Once a modular part is finalized, its internal container logic and specific JavaScript functions are merged into the root `observation.html`. 
3.  **Source of Truth:** The `.txt` and `.md` files in subdirectories (like `7. paraclinique/`) contain the medical reference data (biological ranges, mnemonics) used to populate the HTML templates.

## Engineering & UI Standards

To ensure seamless integration during the merge process, all files in this directory must adhere to these constraints:

### 1. UI Architecture (Modular Mode)
*   **Header Exclusion:** Do **NOT** include the `.floating-island` navigation header in these files. They are designed to be viewed as partials or within iframes.
*   **Vertical Space:** Use `padding-top: 20px` in the `body` CSS (instead of the 80px used in the root file) to reclaim space.
*   **Consistency:** Keep ID and `name` attributes identical to those in the root `observation.html` to ensure that export logic (`docx.js`) and progress tracking remain functional after fusion.

### 2. Linguistic & Technical Integrity
*   **Language:** Strictly French (Français). Maintain high-quality medical terminology.
*   **Encoding:** Strictly **UTF-8 without BOM**.
*   **Accents:** Ensure proper handling of French characters (é, è, à, ç, etc.). Never use HTML entities (like `&eacute;`) if literal UTF-8 characters can be used safely.

### 3. Medical Logic
*   **Mnemonics:** Always implement "SITI FADMA" for symptom characterization and "3A + F" for general signs.
*   **Biological Validation:** Paraclinical sections must use the sex-dependent reference ranges consolidated in `valeurs_biologiques.md`.

## Directory Map
*   `0_...` to `6_...`: Current active HTML modules.
*   `main/`: Legacy text blueprints and stage guides.
*   `7. paraclinique/`: Reference data for the biological validator.
*   `organise this/`: Raw source material (PDFs/images) awaiting conversion into HTML logic.
