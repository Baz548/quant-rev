# QuantByProf (v2.0) — Mobile-First Quant Concept Revision & Question Bank

**QuantByProf** is a standalone, zero-backend, mobile-first Single-Page Web Application (`index.html`) built for rapid **Quantitative Aptitude** concept revision and exam-level practice. It is designed in an Instagram-style vertical card feed optimized for mobile screens with a responsive 3-column desktop layout for laptop usage.

## 1. Project Evolution & Context History

| Milestone | Scope & Architecture | Key Decisions & Outcome |
| :--- | :--- | :--- |
| **prof_v1.1** | Desktop Web Prototype (`index.html`) + Scraper Pipeline (`crawler.py`, `seed_questions.py`) | Built initial 3-section prototype covering Quantitative Aptitude (QA), Reading Comprehension (VA_RC split-pane), and Logical Reasoning (LR dual-pane with scratchpad). |
| **prof_v1.4** | Google Colab Integrated Testbench (`prof_v1.4_testbench.ipynb` + `bot.py`) | Integrated React 18 UI harness into Colab via `IPython.display.HTML` with inline JSON injection (`window.QUESTION_BANK`) to eliminate iframe CORS errors, paired with a Telegram bot companion module. |
| **QuantGram (v1.5)** | Mobile-First Scope Pivot | Narrowed scope strictly to **Quant Concept Revision** in an Instagram-style vertical feed with topical saved lists, removing VA_RC and LR split-screens to prioritize mobile ergonomics. |
| **QuantByProf (v2.0)** | Current Production Release (`index.html` on GitHub Pages) | Rebranded to **QuantByProf**, separated the top navigation into two distinct themed sections (**Revise** and **Questions**), made concept cards concise for instant readability (16 cards), and expanded the standalone Question Bank (20 questions) across 5 core Quant topics. |

## 2. Core Architecture & Visual Themes (v2.0)

The application lives entirely inside a single standalone file (`index.html`) using zero-compile modern ES6 JavaScript and Tailwind CSS via CDN, mounting in under 15ms without requiring a build server or external database.

### Dual-Section Architecture & Theme Separation

| Section | Purpose | Visual Theme & Palette | Sub-Filters Available |
| :--- | :--- | :--- | :--- |
| **📖 Revise** | Concise, clutter-free concept cards with core formulas, 2 recognition/trap bullets, and a 1-line memory hook. | **Royal Indigo & Warm Study Ivory** (`body.theme-revise`, background `#f6f5ff`, deep indigo formula cards `#1e1b4b → #3730a3`, gold highlights). | `All Concepts`, `🔖 Saved`, `⚡ Revise Queue`, `✅ Mastered` |
| **🎯 Questions** | Standalone interactive MCQ question bank with difficulty badges, instant option validation, retry buttons, and step-by-step shortcut drawers. | **Cyber Teal & Crisp Slate Arena** (`body.theme-questions`, background `#ecfeff`, dark teal header/accents `#042f2e → #0d9488`). | `All Questions`, `❓ Unattempted`, `❌ Needs Retry`, `🔖 Saved`, `✅ Correct` |

### Shared Topic Filters
Both **Revise** and **Questions** share the same horizontal scrollable topic filter bar:
1. **All Topics** (`All`)
2. **Algebra** (`Algebra`) — Cubic identities, reciprocal ladders, symmetric squares, AM-GM & quadratics.
3. **Number Theory** (`Number Theory`) — Euler's totient, Fermat's little theorem, factor counting, Legendre's factorial formula, binomial remainders.
4. **Geometry** (`Geometry`) — Apollonius theorem, right-triangle inradius/circumradius, power of a point, common tangents, similarity vs. shared-height area scaling.
5. **Ratio & Mixtures** (`Ratio & Mixtures`) — Componendo & Dividendo, equal ratios theorem, repeated dilution/replacement, alligation denominator rule.
6. **Arithmetic** (`Arithmetic`) — Successive percentage change, product constancy, false weight dishonesty, harmonic mean speed, after-meeting train rule.

## 3. Data Schemas (For Adding Future Content)

### A. Concept Card Schema (`SEED_CONCEPTS`)
```json
{
  "id": "c_alg_1",
  "topic": "Algebra",
  "subtopic": "Cubic Identity",
  "title": "Euler's Conditional Identity (a + b + c = 0)",
  "formula": "a³ + b³ + c³ − 3abc = (a + b + c)(a² + b² + c² − ab − bc − ca)",
  "highlight": "If a + b + c = 0  ⟹  a³ + b³ + c³ = 3abc",
  "bullets": [
    "Fraction form: (a²/bc) + (b²/ca) + (c²/ab) = 3 whenever a + b + c = 0.",
    "Converse trap: a³ + b³ + c³ = 3abc means EITHER a + b + c = 0 OR a = b = c."
  ],
  "hook": "Zero sum kills the big bracket → cubes collapse to 3abc."
}
```

### B. Question Bank Schema (`SEED_QUESTIONS`)
```json
{
  "id": "q_alg_2",
  "topic": "Algebra",
  "subtopic": "Reciprocal Ladder",
  "difficulty": "Hard",
  "concept_ref": "c_alg_2",
  "question": "If x + 1/x = 3, what is the exact value of x⁵ + 1/x⁵?",
  "options": [
    "A) 120",
    "B) 123",
    "C) 126",
    "D) 129"
  ],
  "correct": 1,
  "explanation": "x² + 1/x² = 7 and x³ + 1/x³ = 18. Using x⁵ + 1/x⁵ = (x² + 1/x²)(x³ + 1/x³) − (x + 1/x) = 7 × 18 − 3 = 123."
}
```

## 4. State Persistence & Cross-Device Sync

All user interactions persist automatically in browser `localStorage` under the key **`quantbyprof_v2_state`**:
* `savedConcepts`: Map of bookmarked concept IDs (`{ [id]: true }`).
* `savedQuestions`: Map of bookmarked question IDs (`{ [id]: true }`).
* `conceptMastery`: Mastery tags per concept (`{ [id]: "mastered" | "revise" }`).
* `questionAnswers`: Selected option index per question (`{ [id]: number }`).
* `customConcepts` & `customQuestions`: User-created cards added via the in-app **+ Add** modal.

To transfer progress between phone and laptop, open the **Sync** modal, click **Copy Backup JSON**, and paste it into the **Sync** modal on the target device.

## 5. Deployment & Usage Instructions

1. **GitHub Pages Hosting:**
   * Upload `index.html` and this `README.md` to the root of your public GitHub repository.
   * Enable **Settings → Pages → Branch: `main` (`/root`)**.
   * Access the live app at `https://<your-username>.github.io/<repo-name>/`.
2. **Mobile App Installation:**
   * Open the live GitHub Pages URL on iOS Safari or Android Chrome and select **Add to Home Screen** to run QuantByProf in full-screen standalone mode.

## 6. AI Continuation Prompt (Copy-Paste to Resume in Any New Chat)

When starting a new AI session or connecting a Gemini Notebook, paste this block along with `README.md` (and `index.html` if editing code):

> We are building **QuantByProf (v2.0)**, a standalone mobile-first single-file web application (`index.html`) hosted on GitHub Pages for Quantitative Aptitude revision and question practice.
> 
> Current architecture in `index.html`:
> 1. Two top-level sections with distinct visual themes: **Revise** (Royal Indigo study theme, 16 concise concept cards) and **Questions** (Cyber Teal arena theme, 20 interactive MCQ questions).
> 2. Shared topic filters across both sections: `All`, `Algebra`, `Number Theory`, `Geometry`, `Ratio & Mixtures`, and `Arithmetic`.
> 3. Zero-compile ES6 JavaScript + Tailwind CSS CDN with `localStorage` persistence (`quantbyprof_v2_state`), custom card creation modal (`+ Add`), and JSON export/restore (`Sync`).
> 
> Please review the attached `README.md` (and `index.html`) and help me implement the next set of updates while preserving the existing state schema and mobile-first layout.
