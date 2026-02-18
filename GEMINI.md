# Project Overview

This directory (`clinique_to_do`) contains a web-based interactive medical observation checklist. It serves as a guide for medical practitioners to ensure all essential points are covered during a patient consultation and examination. The project is being structured to provide multiple formats of the checklist and to be expandable with specialized templates.

# Key Files

*   `index.html`: The main entry point for the project. It will provide navigation to the different checklist versions and specialized templates.
*   `simplechecklist.html`: A simplified, mobile-friendly version of the checklist for quick reference.
*   `observation.html`: A comprehensive desktop version of the checklist.
*   `services/`: This directory will contain specialized checklist templates for different medical services (e.g., Cardiology, Neurology). Each specialty will have its own folder containing an HTML template and relevant resource files.
*   `README.md`: Provides a brief overview of the project's purpose.
*   `idea.txt`: Outlines the future development ideas for the project.
*   `plan.txt`: Details the development plan and new file structure.
*   `main/`: Contains source and reference materials for the checklists.
*   `backup/`: Contains historical versions and backups of files. **Note:** Do not delete or modify files in this directory. It is for archival purposes.
*   `ressources/`: Contains various reference materials like PDFs and guides.

# Usage

*   Open `index.html` in a web browser to access the main navigation page.
*   From the main page, you can choose:
    *   **Simple Checklist**: A version optimized for mobile use.
    *   **Normal Checklist**: A full-featured version for desktop use.
    *   **Specialized Templates**: A dropdown or search bar will allow you to select a checklist tailored to a specific medical specialty.

# Development Plan

The project will be developed according to the following plan:

1.  **Create `simplechecklist.html`**: A lightweight, responsive checklist for mobile devices.
2.  **Create `observation.html`**: A full-featured desktop version with enhanced capabilities, including better export options.
3.  **Develop `index.html`**: This will serve as the central hub, providing access to the simple and normal checklists, and a search/dropdown for specialty templates.
4.  **Populate `services/spe/`**: Create and organize specialty-specific checklists, starting with existing resources and progressively adding more. Each specialty's folder will contain its HTML file and a dedicated `ressources` subfolder.
