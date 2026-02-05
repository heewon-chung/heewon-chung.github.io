# Research Page Update

## TL;DR

> **Quick Summary**: Rewrite `content/research/index.html` — replace the fully commented-out Korean content with 4 research topics (3 regular cards + 1 MPC section with nested sub-cards for PSO/PIR/FSS) in the site's dark mode style.
> 
> **Deliverables**:
> - Updated `content/research/index.html` with 4 research topics (MPC section has nested sub-cards)
> 
> **Estimated Effort**: Quick
> **Parallel Execution**: NO — single task
> **Critical Path**: Task 1 (only task)

---

## Context

### Original Request
User wants to update research topics briefly with:
- Zero-Knowledge Proofs & Verifiable Computation
- Blockchains (Applications of ZKP)
- MPC (Private Set Operation, Private Information Retrieval, Function Secret Sharing, ...)
- Fully Homomorphic Encryption

User said: "briefly", "you can rearrange the topics."

### Interview Summary
**Key Discussions**:
- Description level: Title + short paragraph (3-5 sentences) per topic
- Old Korean content: Remove entirely (clean slate)
- MPC structure: MPC section header with overview text, then nested sub-cards for PSO, PIR, FSS (each with their own brief description)

**Research Findings**:
- Current `content/research/index.html` is 100% commented out (230 lines in `<!-- -->`) — page renders blank
- Site uses consistent dark mode: `#22272e` bg, `#e0e0e0` text, `#23272b` cards, `#4da6ff` accent
- Publications and About pages share same CSS patterns (container, card, font stack)
- Homepage bio (`layouts/index.html:19-35`) describes research interests — use as source for accurate descriptions
- User's notable work: Bulletproofs+ adopted by Monero (mentioned on homepage)

### Metis Review
**Identified Gaps** (addressed):
- Content accuracy risk: Descriptions must draw from user's own homepage bio language, not invented claims
- Brevity enforcement: Hard cap of 4 sentences per topic (user said "briefly")
- `<html lang>` inconsistency: Other pages use `lang="ko"` but content is English; new page should use `lang="en"`
- CSS approach: Publications uses CSS variables, About uses hardcoded hex — standardize on CSS variables
- Topic ordering: ZKP&VC → Blockchains → MPC → FHE for narrative flow (proofs → application → computation → encryption)

---

## Work Objectives

### Core Objective
Replace the blank/commented-out research page with a clean, dark-mode-styled page showing 4 research topics with brief English descriptions.

### Concrete Deliverables
- `content/research/index.html` — complete rewrite

### Definition of Done
- [ ] `hugo --minify` builds successfully
- [ ] Page at `/research/` displays all 4 research topics
- [ ] No Korean content or HTML comment remnants from old version
- [ ] Visual style matches About and Publications pages

### Must Have
- 4 research topic areas displayed
- ZKP&VC, Blockchains, FHE as regular topic cards (title + 3-4 sentence description)
- MPC as a section with overview text + 3 nested sub-cards (PSO, PIR, FSS), each sub-card with its own brief description (2-3 sentences)
- Dark mode styling matching site conventions
- Responsive design (mobile-friendly)
- Blockchains topic framed as "Applications of ZKP" (not general blockchain)

### Must NOT Have (Guardrails)
- NO JavaScript — page is static content
- NO external CDN dependencies (no Google Fonts, no icon libraries)
- NO placeholder images or `<img>` tags
- NO links to publications (not requested)
- NO emoji/icons in cards
- NO accordion/toggle/animation features
- NO descriptions longer than 4 sentences per topic
- NO invented research claims — draw ONLY from homepage bio text (`layouts/index.html:19-35`)
- NO Hugo front matter — content files in this project are raw HTML without YAML/TOML front matter

---

## Verification Strategy

> **UNIVERSAL RULE: ZERO HUMAN INTERVENTION**
> ALL verification is executed by the agent using tools. No human action permitted.

### Test Decision
- **Infrastructure exists**: NO (Hugo static site, no test framework)
- **Automated tests**: None
- **Agent-Executed QA**: ALWAYS (mandatory)

---

## TODOs

- [x] 1. Rewrite research page with 4 topic cards

  **What to do**:
  - Replace the ENTIRE content of `content/research/index.html` (remove all 230 lines of commented-out Korean HTML)
  - Write a fresh HTML page with the following structure:

  **HTML Structure** (follow patterns from `content/about/index.html`):
  ```
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Research</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
      /* CSS variables from publications/index.html:10-20 */
      /* html, body override from about/index.html:8-12 (with !important) */
      /* Container: max-width: 1000px from about/index.html:19-23 */
      /* Card styles from about/index.html:42-49 */
      /* Title color: #4da6ff from about/index.html:51 */
      /* Font: 'Noto Sans KR', 'Segoe UI', Arial, sans-serif */
      /* Responsive @media query for mobile */
    </style>
  </head>
  <body>
    <div class="container">
      <h2>Research</h2>
      <p class="intro">Brief 1-sentence research intro</p>

      <!-- Regular card: ZKP & VC -->
      <!-- Regular card: Blockchains -->

      <!-- MPC section: section-title header + overview text -->
      <!--   Sub-card: PSO -->
      <!--   Sub-card: PIR -->
      <!--   Sub-card: FSS -->

      <!-- Regular card: FHE -->
    </div>
  </body>
  </html>
  ```

  **Topic Order and Content** (draw language from `layouts/index.html:19-35`):

  1. **Zero-Knowledge Proofs & Verifiable Computation**
     - Core topic: proving statements without revealing underlying information
     - Mention: succinct proofs, efficient verification, Bulletproofs+ contribution
     - Connect to: privacy guarantees, blockchain applications
     - Max 4 sentences

  2. **Blockchains (Applications of ZKP)**
     - Frame as: applying ZKP to blockchain scalability and privacy
     - Mention: confidential transactions, scalability improvements
     - Reference: Bulletproofs+ adoption by Monero as concrete example
     - Max 4 sentences

  3. **Secure Multi-Party Computation (MPC)** — NESTED LAYOUT
     - **Section header**: "Secure Multi-Party Computation (MPC)" styled as a section title (like `.section-title` in about page)
     - **Overview text**: 2-3 sentences introducing MPC (multiple parties jointly computing functions without revealing individual inputs, privacy-enhancing protocols)
     - **3 nested sub-cards** underneath, each with:
       - **Private Set Operations (PSO)**: 2-3 sentences. Computing set operations (intersection, union, etc.) on private datasets without revealing individual elements.
       - **Private Information Retrieval (PIR)**: 2-3 sentences. Querying a database without revealing which item was requested.
       - **Function Secret Sharing (FSS)**: 2-3 sentences. Splitting a function into secret shares so that multiple servers can evaluate it on inputs without learning the function itself.
     - Sub-cards should be visually distinct from main cards: slightly smaller, possibly indented or with a subtle left border, using `--secondary-color` (#7fdde9) for sub-card titles instead of `--accent-color`

  4. **Fully Homomorphic Encryption (FHE)**
     - Core topic: computing on encrypted data without decryption
     - Connect to: user's PhD focus (FHE and practical applications)
     - Mention: cloud computing, privacy-preserving data analysis
     - Max 4 sentences

  **CSS Specifics** (exact values to use):
  - `html, body { background: #22272e !important; }` — from `about/index.html:8-10`
  - CSS variables: `--bg-color: #22272e; --text-color: #e0e0e0; --card-bg: #23272b; --accent-color: #4da6ff; --secondary-color: #7fdde9; --muted-color: #b0b0b0;` — from `publications/index.html:10-20`
  - Container: `max-width: 1000px; margin: 0 auto; padding: 0 4px 24px 4px;` — from `about/index.html:19-23`
  - **Regular cards** (ZKP&VC, Blockchains, FHE): `background: var(--card-bg); border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.08); padding: 16px 14px 12px 14px; margin-bottom: 14px;` — from `about/index.html:42-49`
  - Regular card title: `color: var(--accent-color); font-size: 1.05rem; font-weight: bold;` — from `about/index.html:50-54`
  - **MPC section title**: Use `.section-title` pattern from `about/index.html:30-36`: `color: #bdd3de; font-size: 1.2rem; font-weight: bold; margin-top: 2.5rem; margin-bottom: 1.2rem;`
  - **MPC sub-cards** (PSO, PIR, FSS): Same card base styling BUT with visual differentiation:
    - Slightly smaller padding: `padding: 12px 14px 10px 14px;`
    - Left border accent: `border-left: 3px solid var(--secondary-color);`
    - Sub-card title color: `color: var(--secondary-color);` (#7fdde9) — distinguishes from main topic cards which use `--accent-color` (#4da6ff)
    - Optionally wrap sub-cards in a container with `margin-left: 12px;` for subtle indentation
  - Description: `color: var(--text-color); font-size: 0.98rem;` — from `about/index.html:63-66`
  - Font: `'Noto Sans KR', 'Segoe UI', Arial, sans-serif` — consistent across pages
  - Page heading: `color: #fff; font-size: 1.8rem; letter-spacing: -1px;` — from `about/index.html:24-29`
  - Responsive: `@media (max-width: 768px)` — adjust padding/font sizes, remove sub-card left margin on mobile

  **Must NOT do**:
  - Do NOT add JavaScript
  - Do NOT add images or external CDN links
  - Do NOT add links to publications page
  - Do NOT exceed 4 sentences per main topic description, 3 sentences per sub-card description
  - Do NOT add Hugo front matter (no `---` YAML block)
  - Do NOT invent research claims beyond what's on the homepage bio
  - Do NOT add emoji or icons

  **Recommended Agent Profile**:
  - **Category**: `quick`
    - Reason: Single file content update with well-defined styling patterns to follow
  - **Skills**: [`frontend-ui-ux`]
    - `frontend-ui-ux`: Needed for matching dark mode CSS patterns and responsive layout

  **Parallelization**:
  - **Can Run In Parallel**: NO (single task)
  - **Parallel Group**: N/A
  - **Blocks**: None
  - **Blocked By**: None

  **References**:

  **Pattern References** (existing code to follow):
  - `content/about/index.html:1-80` — Full HTML document structure, dark mode body override, container pattern, card styling, font stack, section titles. This is the PRIMARY template to follow.
  - `content/publications/index.html:8-26` — CSS variables definition (`:root` block). Use this approach for color definitions.
  - `content/about/index.html:42-66` — Card classes (`.card`, `.card-title`, `.card-desc`). Replicate this card pattern for research topics.

  **Content References** (source of truth for descriptions):
  - `layouts/index.html:19-35` — User's own research description in their own words. ALL topic descriptions must draw from this language. Key phrases: "privacy-enhancing technologies", "secure multiparty computation", "fully homomorphic encryption", "zero-knowledge proofs", "private set operations", "theoretical foundations of blockchain security", "efficient cryptographic protocols", "blockchain scalability", "Bulletproofs+", "bridge the gap between cryptographic theory and practical deployment".

  **WHY Each Reference Matters**:
  - `about/index.html` — THE styling template. Copy its HTML structure, CSS patterns, and card layout exactly.
  - `publications/index.html` — CSS variable approach. Use `:root` variables instead of hardcoded hex values.
  - `layouts/index.html` — Content accuracy. Every research description must use language the user already wrote about themselves. Do NOT invent claims.

  **Acceptance Criteria**:

  > **AGENT-EXECUTABLE VERIFICATION ONLY**

  - [ ] File `content/research/index.html` exists and is NOT commented out
  - [ ] File contains NO Korean characters (한국어)
  - [ ] File contains NO `<!-- ... -->` comment blocks from old content
  - [ ] File contains `<html lang="en">`
  - [ ] File contains `<meta name="viewport"`
  - [ ] File contains `#22272e` (dark mode background)
  - [ ] File contains all 4 topic titles: "Zero-Knowledge Proofs", "Blockchain", "Multi-Party Computation" (or "Multiparty Computation"), "Fully Homomorphic Encryption"
  - [ ] File contains 3 MPC sub-card titles: "Private Set Operation", "Private Information Retrieval", "Function Secret Sharing"
  - [ ] MPC sub-cards are visually nested (have `border-left` styling or similar visual grouping)
  - [ ] File contains NO `<script>` tags
  - [ ] File contains NO `<img>` tags
  - [ ] `hugo --minify` exits with code 0

  **Agent-Executed QA Scenarios (MANDATORY):**

  ```
  Scenario: Hugo builds successfully with new research page
    Tool: Bash
    Preconditions: Hugo installed, theme submodule initialized
    Steps:
      1. Run: hugo --minify
      2. Assert: exit code is 0
      3. Assert: stdout contains "Total in" (build summary)
      4. Assert: public/research/index.html exists
    Expected Result: Clean build with no errors
    Evidence: Build output captured

  Scenario: Research page displays all 4 topics
    Tool: Bash (curl)
    Preconditions: Hugo dev server running
    Steps:
      1. Run: hugo server -D --port 1314 & (background)
      2. Wait: 3 seconds for server startup
      3. Run: curl -s http://localhost:1314/research/
      4. Assert: response contains "Zero-Knowledge"
      5. Assert: response contains "Blockchain"
      6. Assert: response contains "Computation" (for both MPC and VC)
      7. Assert: response contains "Homomorphic"
      8. Assert: response contains "Private Set Operation"
      9. Assert: response contains "Private Information Retrieval"
      10. Assert: response contains "Function Secret Sharing"
      11. Kill: hugo server process
    Expected Result: All 4 topics and MPC subtopics present
    Evidence: curl response body captured

  Scenario: No Korean content or old comment remnants
    Tool: Bash (grep)
    Preconditions: content/research/index.html written
    Steps:
      1. Run: grep -cP '[\x{AC00}-\x{D7AF}]' content/research/index.html
      2. Assert: count is 0 (no Korean characters)
      3. Run: grep -c '고급 암호' content/research/index.html
      4. Assert: count is 0 (old title gone)
    Expected Result: No Korean content remains
    Evidence: grep output captured

  Scenario: Page renders with correct dark mode styling (visual check)
    Tool: Playwright (playwright skill)
    Preconditions: Hugo dev server running on localhost:1314
    Steps:
      1. Navigate to: http://localhost:1314/research/
      2. Wait for: .container visible (timeout: 5s)
      3. Assert: page background color is approximately #22272e
      4. Assert: at least 4 card elements visible
      5. Assert: card titles are visible and in accent color
      6. Screenshot: .sisyphus/evidence/task-1-research-page-desktop.png
      7. Set viewport: 375x812 (mobile)
      8. Screenshot: .sisyphus/evidence/task-1-research-page-mobile.png
      9. Assert: no horizontal overflow on mobile
    Expected Result: Dark mode cards render correctly on desktop and mobile
    Evidence: .sisyphus/evidence/task-1-research-page-desktop.png, .sisyphus/evidence/task-1-research-page-mobile.png
  ```

  **Evidence to Capture:**
  - [ ] Screenshots in .sisyphus/evidence/ for desktop and mobile views
  - [ ] Build output from `hugo --minify`
  - [ ] curl response body from /research/

  **Commit**: YES
  - Message: `content(research): rewrite research page with 4 topic cards in English`
  - Files: `content/research/index.html`
  - Pre-commit: `hugo --minify`

---

## Commit Strategy

| After Task | Message | Files | Verification |
|------------|---------|-------|--------------|
| 1 | `content(research): rewrite research page with 4 topic cards in English` | `content/research/index.html` | `hugo --minify` |

---

## Success Criteria

### Verification Commands
```bash
hugo --minify  # Expected: builds with exit code 0
```

### Final Checklist
- [ ] All 4 research topics displayed with brief English descriptions
- [ ] Dark mode styling matches About and Publications pages
- [ ] Responsive on mobile viewports
- [ ] No Korean content, no commented-out old code
- [ ] No JavaScript, no images, no external dependencies
- [ ] Hugo builds cleanly
