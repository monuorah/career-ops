# Modo: pdf — Generación de PDF ATS-Optimizado

## MANDATORY: Dynamic Narrative Skills Generation

**ALWAYS generate narrative skills from cv.md, tailored to THIS JD. NEVER use comma-separated lists or hardcoded orderings.**

### Format (Non-Negotiable)

Each skill entry:
- `**Skill Category** - proof/context from cv.md; additional proof; context`
- 1-2 lines max (~100-180 characters)
- Examples from real CVs:
  - `**Python** - 3 production libraries shipped to Dell SDL team (37.5% coverage); Binary Ant Colony Algorithm in published research; Flask web interface for AI tool`
  - `**Docker & Infrastructure** - containerized parallel test execution across 3 VMware products at Dell; environment isolation design; Robot Framework integration into CI/CD pipeline`
  - `**AI & Automation** - AutoGen multi-agent pipeline with Llama 3.2 LLM; two-agent orchestration for code vulnerability detection; Firebase AI integration in consumer app`
- Generate 6-8 entries total
- Color the category name (rendered as `<span class="cat">Category</span>`)

### How to Build Narrative Skills (Step-by-Step)

**Step 1: Extract all skill contexts from cv.md**

Scan cv.md for every mention of a technology and extract what you actually did with it. Examples:

From Dell internship:
- **Python** → "Developed 3 custom Python libraries", "increased automated SDL test coverage by 37.5%"
- **Docker** → "Designed containerized security testing infrastructure", "enabling parallel test execution across VxRail, Configuration Portal, and DPC VMware products"
- **Robot Framework** → "Integrated Robot Framework test suites with existing CVF security tools"
- **AutoGen** → "Built an AI-powered security analysis tool using AutoGen multi-agent framework", "Llama 3.2 LLM"

From FoodLens project:
- **SwiftUI** → "Built native iOS nutrition tracking app with SwiftUI", "15+ views including multi-step onboarding, meal logging, trends visualization"
- **Firebase** → "Firebase backend (Auth, Firestore, Storage, Cloud Functions)"
- **APIs** → "Open Food Facts API integration", "USDA API", "barcode scanning"

From Museum project:
- **React** → "15+ MySQL tables, React frontend", "role-based access control across 4 user types"
- **Node.js/Express** → "Node/Express API", "real-time inventory deduction", "PDF report generation"
- **MySQL** → "15+ MySQL tables", "complex multi-table JOIN queries", "soft delete/restore patterns with audit logging"

**Step 2: Detect JD themes (what THIS job cares about)**

Read the JD and identify 3-5 major themes:
- Keywords: "backend", "infrastructure", "scalability" → Backend Engineer theme
- Keywords: "security", "vulnerability", "compliance", "SDL" → Security Engineer theme
- Keywords: "AI", "LLM", "agents", "automation" → AI/Automation theme
- Keywords: "React", "frontend", "UI", "component" → Frontend theme
- Keywords: "infrastructure", "Docker", "Kubernetes", "CI/CD" → DevOps/Infrastructure theme
- Keywords: "compliance", "regulated", "audit", "standards" → Compliance/Regulated Systems theme

**Step 3: Match cv.md skills to JD themes**

For each JD theme, find which skills from Step 1 support it:

Example: JD for Full Stack role emphasizes "e-commerce platform", "React frontend", "database design"
- Match to **React** (museum e-commerce platform, 4 user types, role-based UI)
- Match to **Node.js/Express** (museum REST API, checkout flow, inventory)
- Match to **MySQL** (15+ table schema, audit logging)
- Match to **Azure/Deployment** (deployed on Azure)

Example: JD for Security role emphasizes "SDL", "vulnerability scanning", "compliance"
- Match to **Python** (SDL automation, 3 libraries, 37.5% coverage)
- Match to **Docker & Infrastructure** (containerized testing across products)
- Match to **Regulated Systems** (SDL 7.3 compliance evidence, built tooling for changing control requirements)
- Match to **Robot Framework** (security test orchestration)

**Step 4: Rank matched skills by JD relevance**

Order the matched skills from Step 3 by how central they are to the JD:
1. Most relevant (appears in JD description multiple times, core to the role)
2. Moderately relevant (supports main theme)
3. Supporting (adds credibility, shows depth)

**Step 5: Build narrative entries**

For each matched skill (in ranked order), construct: `**Category** - proof1; proof2; proof3`

- **Proof 1:** The biggest achievement or most relevant context from cv.md
- **Proof 2:** A supporting detail (another achievement, tool, metric, or breadth)
- **Proof 3:** Additional context if space allows (research, integration, deployment)

Keep each entry to 1-2 lines by concatenating proofs with semicolons.

Example construction:
- Matched skill: **Python** (for Security JD)
- Proofs from cv.md:
  1. "3 production libraries shipped to Dell enterprise SDL team"
  2. "37.5% increased automated test coverage"
  3. "Binary Ant Colony Algorithm in published research"
- Result: `**Python** - 3 production libraries shipped to Dell enterprise SDL team (37.5% coverage increase); Binary Ant Colony Algorithm in published research; Flask web interface for AI tool`

**Step 6: Generate HTML**

Output as:
```html
<ul class="skills-list">
  <li><span class="cat">Python</span> - proof1; proof2; proof3</li>
  <li><span class="cat">Docker & Infrastructure</span> - proof1; proof2</li>
  <!-- ... 6-8 total entries ... -->
</ul>
```

**Step 7: Inject into template**

Replace `{{SKILLS}}` with the HTML from Step 6.

---

### Key Rules (Non-Negotiable)

- **Never hardcode skill order.** Every PDF must be different based on the JD.
- **Extract proofs from cv.md only.** Never invent achievements or metrics.
- **Match JD themes to cv.md skills dynamically.** Don't rely on archetype tables; use the actual JD text.
- **Omit irrelevant skills.** If a skill doesn't match any JD theme, don't include it (even if it's in cv.md).
- **Minimum 5, maximum 8 entries.** Aim for 6-7.
- **One skill per entry.** Don't combine unrelated skills (e.g., `Python & JavaScript` together).
- **Focus on proof, not definition.** Not "Python — A programming language" but "Python — 3 production libraries shipped to Dell SDL team".

---

## PDF Generation Pipeline

1. **Read source files**
   - `cv.md` (all skill contexts, proofs, metrics)
   - `config/profile.yml` (name, contact, location)
   - JD (user provides URL or text)

2. **Detect job metadata**
   - Extract company name and job title from JD
   - Detect JD language → CV language (EN default)
   - Detect company location → paper format (US/Canada → letter, else → a4)

3. **Extract JD themes (for skill matching)**
   - Read JD text and identify 3-5 major themes
   - Examples: Backend/infrastructure, Security/compliance, AI/LLMs, Full-stack/frontend, DevOps
   - Note key repeated keywords and phrases

4. **Build narrative skills section** ← **KEY STEP (see detailed instructions above)**
   - Follow "How to Build Narrative Skills" section above
   - Extract skill contexts from cv.md (Step 1)
   - Match to JD themes (Step 3)
   - Rank by JD relevance (Step 4)
   - Build 6-8 narrative entries (Step 5)
   - Generate HTML (Step 6)
   - Result: HTML ready for `{{SKILLS}}` placeholder

5. **Generate other CV sections**
   - **Professional Summary:** Rewrite for role (3-4 sentences), inject top JD keywords + exit narrative bridge
   - **Core Competencies:** Extract 6-8 keyword phrases from JD requirements
   - **Work Experience:** Reorder bullets by JD relevance (most relevant first)
   - **Projects:** Select top 3-4 most relevant projects; reorder bullets within each
   - **Education & Leadership:** Keep as-is (static sections)

6. **Inject keywords ethically**
   - Use exact JD vocabulary when reformulating existing cv.md content
   - Example: JD says "RAG pipelines" + CV says "LLM workflows with retrieval" → rewrite as "RAG pipeline design and LLM orchestration workflows"
   - NEVER invent skills or achievements

7. **Generate HTML from template**
   - Read `templates/cv-user-template.html`
   - Replace all `{{...}}` placeholders with personalized content from Steps 4-5
   - Ensure `{{SKILLS}}` is replaced with the narrative skills HTML from Step 4

8. **Normalize candidate name**
   - Read `preferred_name` from `config/profile.yml`
   - Convert to kebab-case lowercase (e.g., "Muna Onuorah" → "muna-onuorah")
   - Use as `{candidate}` in filenames

9. **Write HTML to temp file**
   - Path: `/tmp/cv-{candidate}-{company}.html`
   - Ensure all fonts and styles are self-contained (ATS compatibility)

10. **Render to PDF**
    - Execute: `node generate-pdf.mjs /tmp/cv-{candidate}-{company}.html output/cv-{candidate}-{company}-{YYYY-MM-DD}.pdf --format={letter|a4}`
    - Verify file exists and is > 50KB

11. **Report results**
    - PDF file path
    - Page count
    - Verification: Confirm narrative skills appear in output
    - Note: JD theme coverage (which themes matched and were emphasized)

## Reglas ATS (parseo limpio)

- Layout single-column (sin sidebars, sin columnas paralelas)
- Headers estándar: "Professional Summary", "Work Experience", "Education", "Skills", "Certifications", "Projects"
- Sin texto en imágenes/SVGs
- Sin info crítica en headers/footers del PDF (ATS los ignora)
- UTF-8, texto seleccionable (no rasterizado)
- Sin tablas anidadas
- Keywords del JD distribuidas: Summary (top 5), primer bullet de cada rol, Skills section

## Diseño del PDF

- **Fonts**: Space Grotesk (headings, 600-700) + DM Sans (body, 400-500)
- **Fonts self-hosted**: `fonts/`
- **Header**: nombre en Space Grotesk 24px bold + línea gradiente `linear-gradient(to right, hsl(187,74%,32%), hsl(270,70%,45%))` 2px + fila de contacto
- **Section headers**: Space Grotesk 13px, uppercase, letter-spacing 0.05em, color cyan primary
- **Body**: DM Sans 11px, line-height 1.5
- **Company names**: color accent purple `hsl(270,70%,45%)`
- **Márgenes**: 0.6in
- **Background**: blanco puro

## Orden de secciones (optimizado "6-second recruiter scan")

1. Header (nombre grande, gradiente, contacto, link portfolio)
2. Professional Summary (3-4 líneas, keyword-dense)
3. Core Competencies (6-8 keyword phrases en flex-grid)
4. Work Experience (cronológico inverso)
5. Projects (top 3-4 más relevantes)
6. Education & Certifications
7. Skills (idiomas + técnicos)

## Estrategia de keyword injection (ético, basado en verdad)

Ejemplos de reformulación legítima:
- JD dice "RAG pipelines" y CV dice "LLM workflows with retrieval" → cambiar a "RAG pipeline design and LLM orchestration workflows"
- JD dice "MLOps" y CV dice "observability, evals, error handling" → cambiar a "MLOps and observability: evals, error handling, cost monitoring"
- JD dice "stakeholder management" y CV dice "collaborated with team" → cambiar a "stakeholder management across engineering, operations, and business"

**NUNCA añadir skills que el candidato no tiene. Solo reformular experiencia real con el vocabulario exacto del JD.**

## Template HTML

Usar el template en `cv-template.html`. Reemplazar los placeholders `{{...}}` con contenido personalizado:

| Placeholder | Contenido |
|-------------|-----------|
| `{{LANG}}` | `en` o `es` |
| `{{PAGE_WIDTH}}` | `8.5in` (letter) o `210mm` (A4) |
| `{{NAME}}` | (from profile.yml) |
| `{{PHONE}}` | (from profile.yml — include with its separator only when `profile.yml` has a non-empty `phone` value; omit both `<span>` and `<span class="separator">` otherwise) |
| `{{EMAIL}}` | (from profile.yml) |
| `{{LINKEDIN_URL}}` | [from profile.yml] |
| `{{LINKEDIN_DISPLAY}}` | [from profile.yml] |
| `{{PORTFOLIO_URL}}` | [from profile.yml] (o /es según idioma) |
| `{{PORTFOLIO_DISPLAY}}` | [from profile.yml] (o /es según idioma) |
| `{{LOCATION}}` | [from profile.yml] |
| `{{SECTION_SUMMARY}}` | Professional Summary / Resumen Profesional |
| `{{SUMMARY_TEXT}}` | Summary personalizado con keywords |
| `{{SECTION_COMPETENCIES}}` | Core Competencies / Competencias Core |
| `{{COMPETENCIES}}` | `<span class="competency-tag">keyword</span>` × 6-8 |
| `{{SECTION_EXPERIENCE}}` | Work Experience / Experiencia Laboral |
| `{{EXPERIENCE}}` | HTML de cada trabajo con bullets reordenados |
| `{{SECTION_PROJECTS}}` | Projects / Proyectos |
| `{{PROJECTS}}` | HTML de top 3-4 proyectos |
| `{{SECTION_EDUCATION}}` | Education / Formación |
| `{{EDUCATION}}` | HTML de educación |
| `{{SECTION_CERTIFICATIONS}}` | Certifications / Certificaciones |
| `{{CERTIFICATIONS}}` | HTML de certificaciones |
| `{{SECTION_SKILLS}}` | Skills / Competencias |
| `{{SKILLS}}` | HTML de skills |

## Canva CV Generation (optional)

If `config/profile.yml` has `canva_resume_design_id` set, offer the user a choice before generating:
- **"HTML/PDF (fast, ATS-optimized)"** — existing flow above
- **"Canva CV (visual, design-preserving)"** — new flow below

If the user has no `canva_resume_design_id`, skip this prompt and use the HTML/PDF flow.

### Canva workflow

#### Step 1 — Duplicate the base design

a. `export-design` the base design (using `canva_resume_design_id`) as PDF → get download URL
b. `import-design-from-url` using that download URL → creates a new editable design (the duplicate)
c. Note the new `design_id` for the duplicate

#### Step 2 — Read the design structure

a. `get-design-content` on the new design → returns all text elements (richtexts) with their content
b. Map text elements to CV sections by content matching:
   - Look for the candidate's name → header section
   - Look for "Summary" or "Professional Summary" → summary section
   - Look for company names from cv.md → experience sections
   - Look for degree/school names → education section
   - Look for skill keywords → skills section
c. If mapping fails, show the user what was found and ask for guidance

#### Step 3 — Generate tailored content

Same content generation as the HTML flow (Steps 1-11 above):
- Rewrite Professional Summary with JD keywords + exit narrative
- Reorder experience bullets by JD relevance
- Select top competencies from JD requirements
- Inject keywords naturally (NEVER invent)

**IMPORTANT — Character budget rule:** Each replacement text MUST be approximately the same length as the original text it replaces (within ±15% character count). If tailored content is longer, condense it. The Canva design has fixed-size text boxes — longer text causes overlapping with adjacent elements. Count the characters in each original element from Step 2 and enforce this budget when generating replacements.

#### Step 4 — Apply edits

a. `start-editing-transaction` on the duplicate design
b. `perform-editing-operations` with `find_and_replace_text` for each section:
   - Replace summary text with tailored summary
   - Replace each experience bullet with reordered/rewritten bullets
   - Replace competency/skills text with JD-matched terms
   - Replace project descriptions with top relevant projects
c. **Reflow layout after text replacement:**
   After applying all text replacements, the text boxes auto-resize but neighboring elements stay in place. This causes uneven spacing between work experience sections. Fix this:
   1. Read the updated element positions and dimensions from the `perform-editing-operations` response
   2. For each work experience section (top to bottom), calculate where the bullets text box ends: `end_y = top + height`
   3. The next section's header should start at `end_y + consistent_gap` (use the original gap from the template, typically ~30px)
   4. Use `position_element` to move the next section's date, company name, role title, and bullets elements to maintain even spacing
   5. Repeat for all work experience sections
d. **Verify layout before commit:**
   - `get-design-thumbnail` with the transaction_id and page_index=1
   - Visually inspect the thumbnail for: text overlapping, uneven spacing, text cut off, text too small
   - If issues remain, adjust with `position_element`, `resize_element`, or `format_text`
   - Repeat until layout is clean
d. Show the user the final preview and ask for approval
e. `commit-editing-transaction` to save (ONLY after user approval)

#### Step 5 — Export and download PDF

a. `export-design` the duplicate as PDF (format: a4 or letter based on JD location)
b. **IMMEDIATELY** download the PDF using Bash:
   ```bash
   curl -sL -o "output/cv-{candidate}-{company}-canva-{YYYY-MM-DD}.pdf" "{download_url}"
   ```
   The export URL is a pre-signed S3 link that expires in ~2 hours. Download it right away.
c. Verify the download:
   ```bash
   file output/cv-{candidate}-{company}-canva-{YYYY-MM-DD}.pdf
   ```
   Must show "PDF document". If it shows XML or HTML, the URL expired — re-export and retry.
d. Report: PDF path, file size, Canva design URL (for manual tweaking)

#### Error handling

- If `import-design-from-url` fails → fall back to HTML/PDF pipeline with message
- If text elements can't be mapped → warn user, show what was found, ask for manual mapping
- If `find_and_replace_text` finds no matches → try broader substring matching
- Always provide the Canva design URL so the user can edit manually if auto-edit fails

## Post-generación

Actualizar tracker si la oferta ya está registrada: cambiar PDF de ❌ a ✅.
