# Research Page Update - Learnings

## Completed: 2026-02-05

### Task Summary
Rewrote `content/research/index.html` from scratch, replacing 230 lines of commented-out Korean HTML with 160 lines of clean English content featuring 4 research topics with the MPC section having nested sub-cards.

### Patterns Successfully Applied

#### CSS Architecture
- **CSS Variables**: Used `:root` block for theme colors (`--bg-color`, `--accent-color`, `--secondary-color`)
- **Dark Mode**: `html, body { background: #22272e !important; }` override required to theme Gokarna
- **Card System**: 
  - Regular cards: `#23272b` background, `#4da6ff` titles
  - Sub-cards: Same background but with `border-left: 3px solid #7fdde9` and `#7fdde9` titles
- **Typography**: `'Noto Sans KR', 'Segoe UI', Arial, sans-serif` consistent across site

#### Content Guidelines
- Drew descriptions from user's own homepage bio (`layouts/index.html`)
- Hard limits: 4 sentences max for main topics, 3 for sub-cards
- No invented claims — only used language user already wrote about themselves

#### HTML Structure
- Raw HTML without Hugo front matter (site convention)
- `<html lang="en">` (content is English, matches `hugo.toml` setting)
- Responsive with `@media (max-width: 768px)`

### Verification Results
- ✅ Hugo build: SUCCESS (exit code 0)
- ✅ All 4 topics present in rendered HTML
- ✅ MPC sub-cards (PSO, PIR, FSS) all present
- ✅ No Korean content
- ✅ No script/img tags
- ✅ Dark mode colors applied

### File Changes
- `content/research/index.html`: Complete rewrite (+159, -222 lines)

### Commit Ready
Message: `content(research): rewrite research page with 4 topic cards in English`


## Final Status

**Completed**: 2026-02-05
**Commit**: b8d2185
**Message**: content(research): rewrite research page with 4 topic cards in English
**Files Changed**: content/research/index.html (+151, -222)

### Scope Correction
Subagent initially reformatted publications and teaching pages (unintended scope creep). Reverted those changes to maintain single-file focus per plan requirements.

### All Acceptance Criteria Met
- [x] Hugo builds successfully
- [x] All 4 research topics displayed
- [x] MPC section has 3 nested sub-cards (PSO, PIR, FSS)
- [x] No Korean content
- [x] Dark mode styling matches site conventions
- [x] Responsive design included
- [x] No JavaScript, images, or external dependencies

