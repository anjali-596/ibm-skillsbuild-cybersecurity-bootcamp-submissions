# Troubleshooting Your Code: Roast Toast Coast Café

**Author:** Anjali  
**Program:** IBM SkillsBuild – *Use IBM Bob to Troubleshoot Your Code*

## Project Overview

*Roast Toast Coast Café* is a fictional business with a one-page website built with HTML, CSS and JavaScript. The page should show a welcome message, a tagline, an image and an **Our Menu** button that reveals the menu items. When previewed, the image does not display and the button does nothing.

This project finds and fixes those errors. It follows the lab workflow (review → analyze → fix → reflect) and adds a reproducible Python notebook that analyzes the page, groups the errors by severity and type, applies minimal fixes, and verifies the result.

## Dataset / Source Files

This project has no dataset. The input is a single source file provided by the lab:

- **Lab instructions:** <https://github.com/academic-initiative/skillsbuild/blob/main/ibm-bob/troubleshoot-your-code/troubleshoot-your-code.md>
- **Input file (`Menu.html`):** <https://github.com/academic-initiative/skillsbuild/blob/main/ibm-bob/troubleshoot-your-code/file/Menu.html>

## Technologies Used

| Area | Tools |
|---|---|
| Web page under review | HTML5, CSS3, JavaScript |
| AI assistant (lab workflow) | IBM Bob in **Code mode**, inside Visual Studio Code |
| Analysis notebook | Python 3, Jupyter Notebook |
| Libraries | `beautifulsoup4` (HTML/CSS-selector matching), `pandas` (report table), standard library `re`, `difflib`, `json` |

## What Was Found and Fixed

The analyzer found **10 issues** (2 critical, 2 high, 3 medium, 3 low).

| Severity | Type | Issue | Fix |
|---|---|---|---|
| Critical | Syntax | `background-image: url('…';` is missing the closing `)`, so the image never displays | Add the `)` |
| Critical | Functionality | JavaScript uses `.menu-item` but the HTML class is `.menu-items`, so `querySelector` returns `null` and the menu never opens | Change the selector to `.menu-items` |
| High | Structure | CSS rules `header h1` and `header p` match nothing (there is no `<header>`; the wrapper is `div.header-container`) | Re-target to `.header-container h1` / `.header-container p` |
| Medium | Functionality | `background: wheat;` overrides the translucent `background-color` and would hide the light text once the selectors are fixed | Remove the line |
| Medium | Functionality | Result of `querySelector` is used without a null check | Add `if (!menuItems) { return; }` |
| Medium | Structure | Missing `<meta charset>` and `<meta viewport>` | Add both tags |
| Low | Structure | Commented-out duplicate `.menu-section` rule | Remove it |
| Low | Structure | Clickable `<h2>` is not keyboard accessible; image has no text alternative | Recommended only (not auto-applied, to keep the original structure) |

After the fixes the analyzer reports no critical, high or medium issues; only the two low-severity accessibility recommendations remain.

## Repository Contents

```
├── YourName_TroubleshootYourCode.ipynb   # Main notebook (analysis, fixes, verification)
├── requirements.txt                      # Python dependencies
├── YourName_ProjectReport.docx           # Full project report
├── README.md                             # This file
└── output/                               # Created when the notebook runs
    ├── Menu_original.html
    ├── Menu_fixed.html
    └── findings.json
```

## Setup and Run Instructions

1. **Install Python 3.9 or later.**
2. **(Optional) Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate        # Windows: venv\Scripts\activate
   ```
3. **Install the dependencies**
   ```bash
   pip install -r requirements.txt
   ```
4. **Open the notebook**
   ```bash
   jupyter notebook YourName_TroubleshootYourCode.ipynb
   ```
5. **Run all cells** (*Run → Run All Cells*). The notebook contains an embedded copy of the lab's `Menu.html`. To analyze your own copy instead, save it as `Menu.html` in the same folder as the notebook before running.
6. **Check the results** in the `output/` folder, especially `Menu_fixed.html`. Open it in a browser to see the working page (the lab itself does not require rendering).

## Running the Lab in IBM Bob

1. Install VS Code and IBM Bob, then open `Menu.html` in VS Code.
2. Select **Code mode** in the IBM Bob panel.
3. Paste the analysis prompt (replace the file path):
   ```text
   Can you identify all syntax and functional errors in this HTML file:
   "[your-file-path]/Menu.html"?

   Perform a thorough analysis.
   Group the findings by severity (critical, high, medium, low).
   Indicate whether each issue is related to syntax, functionality, or structure.
   Identify anything that could prevent the page from rendering or behaving correctly.
   ```
4. Approve file access, review the categorized results, then send:
   ```text
   Rewrite this file to fix the identified issues.
   Apply the recommendations from your previous analysis.
   Preserve the original structure where possible.
   ```
5. Approve the edit, review the side-by-side diff and save.

## Key Information

- The notebook's analyzer is a **rule-based Python re-implementation** of the review, so results can be reproduced without the IDE. It is not a substitute for running the lab in IBM Bob.
- Line numbers in the reports refer to the embedded copy of `Menu.html` (141 lines).
- The page loads its font and image from external CDNs, so an internet connection is needed to see them in the browser.
- Main takeaway: one-character naming mismatches and a single missing parenthesis are enough to block entire features. A structured prompt, a severity-grouped report and a before/after diff make troubleshooting systematic.
