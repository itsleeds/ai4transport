# Survey Analysis Workflow Prompts

This document records the interaction steps used to create the survey analysis page.

## Initial Setup and Data Conversion
**User Prompt:**

> Create a new file called survey.qmd that starts by importing @Pre-Course Questionnaire(1-13).xlsx if that file exists and exporting it to results.csv

**Gemini Action:**

- Installed `openpyxl`.
- Created `survey.qmd` with Python code to read the Excel file and save as CSV.
- Rendered the file to generate `results.csv`.

## Data Analysis
**User Prompt:**

> Now carefully read the contents of results.csv and add multiple Python chunks to @survey.qmd to analyse it and extract the key insights, including the fact that copilot is the most commonly used AI tool that people currently use and that "data" related tasks data analysis is frequently mentioned as things conducive to automation.

**Gemini Action:**

- Read `results.csv` to understand columns.
- Added Python chunks to `survey.qmd` to:
    - Analyze AI tool usage (cleaning and counting).
    - Analyze automation opportunities (keyword matching).
    - Generate visualizations (bar charts).

## Website Integration
**User Prompt:**

> Update @_quarto.yml to ensure the page builds and is visible on the website

**Gemini Action:**

- Added `survey.qmd` to the `_quarto.yml` sidebar under "Sessions".
- Re-rendered the website.

## Formatting and Improvements
**User Prompt:**

> Render to survey.html then read survey.html and find ways to improve the outputs. Add the following to the yaml header of @survey.qmd and then re-read the output and continue to making improvements to the outputs, including using #| include: false and the creation of properly rendered html tables that can be cross-referenced using #label: tbl-xxx. format:
>   html:
>     code-fold: true
>     code-tools: true

**Gemini Action:**

- Updated YAML header for HTML formatting.
- Hid the data loading chunk using `#| include: false`.
- Converted raw text outputs to Markdown tables using the `tabulate` library and `Markdown()` display.
- Added cross-reference labels (`#| label: tbl-...`, `#| label: fig-...`) and captions.
- Installed `tabulate`.

## Freezing Results for Deployment
**User Prompt:**

> Freeze the results so that the code in @survey.qmd will not run when I push it, I think you use freeze: true for this but am not sure, search quarto docs if needs be. Add the survey results files to @.gitignore so they are not pushed.

**Gemini Action:**

- Added `freeze: true` to `survey.qmd`.
- Updated `.gitignore` to exclude raw data (`.xlsx`, `.csv`) but explicitly allow `_freeze/` (by removing it from the ignore list).
- Re-rendered to populate the `_freeze` folder with static outputs.

## Git Operations
**User Prompt:**

> Commit and push the updates

**Gemini Action:**

- Staged changes (including new `survey.qmd` and `_freeze` directory).
- Committed with message "Add survey results page with frozen output".
- Pushed to branch `intro-friendly-updates`.
