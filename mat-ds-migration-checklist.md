# MAT+ → DS Lookbook Migration Checklist

*Detailed Gap Analysis & Task Prompts · March 2026*

**Source:** https://mainguyen1701.github.io/mat-management-prototype/  
**Target:** https://designsaplus.com/lookbook/inspect/projects/mat_plus/events  
**Goal:** Align UI with DS Lookbook, dev-ready state

---

## GAP ANALYSIS: Current vs. Target

### Current State (Your Prototype)
- **Structure:** Sidebar nav → Main content → Tables/forms
- **Visuals:** Custom styling (blue/gray theme, rounded tables)
- **Components:** Hand-rolled tables, custom filters, bespoke cards
- **Typography:** Inter-like but not exact DS match
- **Interactions:** Functional but inconsistent states

### Target State (DS Lookbook)
- **Structure:** Design21 Jan2026 component library
- **Visuals:** DS tokens (colors, spacing, elevation)
- **Components:** Event Card, Person Card, Form Controls, Tables
- **Typography:** DS font scale
- **Interactions:** Standardized states (hover, focus, active)

---

## PHASE 1: AUDIT & MAPPING (30 min)

### Task 1.1: Inventory Current Components
**Prompt:** Open your prototype and list every UI element you see.

**To-Do:**
- [ ] Screenshot the full page (Cmd+Shift+4 → Space → click window)
- [ ] Create list of components:
  - Navigation elements (sidebar, top bar)
  - Data display (tables, cards, stats)
  - Filters & controls (dropdowns, buttons)
  - Forms (inputs, selects, checkboxes)
  - Modals/drawers (if any)

**Output:** Spreadsheet or document listing every component with screenshot

---

### Task 1.2: Map to DS Components
**Prompt:** For each element in your list, find the equivalent in DS Lookbook.

**DS Components Available:**
- ✅ Event Card (for events list)
- ✅ Person Card (for family/parent info)
- ✅ Table (for data lists)
- ✅ Form Controls (inputs, selects, buttons)
- ✅ Dropdown (for filters)
- ✅ Drawer (for side panels)
- ✅ Badge (for status indicators)
- ✅ Breadcrumb (for navigation)
- ✅ Tabs (for content sections)
- ✅ Accordion (for expandable content)
- ✅ Notification (for alerts)

**To-Do:**
- [ ] Go to https://designsaplus.com/lookbook/inspect/components/
- [ ] For each component in your list, find DS equivalent
- [ ] Note any gaps (custom components not in DS)

**Output:** Mapping table:
| My Component | DS Equivalent | Gap? |
|--------------|---------------|------|
| Student table | Table | No |
| Status badge | Badge | No |
| Family card | Person Card | Minor adjustments |

---

## PHASE 2: VISUAL ALIGNMENT (4 hours)

### Task 2.1: Replace Color System
**Prompt:** Current uses custom blues, DS uses specific tokens.

**Current Colors (you have):**
- Primary blue: ~#4A90E2
- Background: ~#F5F7FA
- Text: various grays

**DS Colors (target):**
- Go to DS Lookbook > Colors > Comprehensive
- Note primary, secondary, background, text tokens

**To-Do:**
- [ ] Open DS Lookbook Colors page
- [ ] Screenshot color palette
- [ ] Replace in your CSS:
  ```css
  /* OLD */
  --primary: #4A90E2;
  
  /* NEW */
  --primary: [DS_PRIMARY_TOKEN];
  ```
- [ ] Update all background colors
- [ ] Update all text colors
- [ ] Check contrast ratios (WCAG AA)

**Verification:** Side-by-side screenshot comparison

---

### Task 2.2: Typography Scale
**Prompt:** DS has specific font sizes/weights.

**To-Do:**
- [ ] Open DS Lookbook > Typography (if available) or inspect text elements
- [ ] Document:
  - H1 size, weight, line-height
  - H2 size, weight, line-height
  - Body size, weight, line-height
  - Small/caption size
- [ ] Replace your font sizes to match
- [ ] Check: Are you using DS font family? (likely Inter)

**Code task:**
```css
/* Replace all font-size: 14px, 16px, 18px, etc. */
/* with DS tokens */
font-size: var(--ds-text-base);
font-weight: var(--ds-font-medium);
```

---

### Task 2.3: Spacing & Grid
**Prompt:** DS uses consistent spacing.

**To-Do:**
- [ ] Inspect DS components for padding/margin values
- [ ] Common DS spacing: 4px, 8px, 12px, 16px, 24px, 32px, 48px
- [ ] Replace hardcoded values:
  ```css
  /* OLD */
  padding: 20px;
  margin-bottom: 15px;
  
  /* NEW */
  padding: var(--ds-spacing-4); /* 16px */
  margin-bottom: var(--ds-spacing-3); /* 12px */
  ```
- [ ] Check grid alignment (12-column? 24-column?)

---

## PHASE 3: COMPONENT MIGRATION (5 hours)

### Task 3.1: Replace Student Table
**Current:** Custom HTML table with sorting/filtering
**Target:** DS Table component

**Prompt:** Your "Contact and Enquiries" table needs to match DS Table.

**To-Do:**
- [ ] Go to DS Lookbook > Table component
- [ ] Copy HTML structure (or inspect element)
- [ ] Replace your table markup
- [ ] Ensure:
  - Header row styling matches DS
  - Row hover states match DS
  - Status badges use DS Badge component
  - "View" links use DS link style
  - Pagination uses DS pattern (if shown)

**Critical check:**
- Does sortable header look like DS?
- Does selected row look like DS?
- Are action buttons in correct style?

---

### Task 3.2: Replace Family/Person Display
**Current:** Custom cards with family info
**Target:** DS Person Card

**Prompt:** "Family Details" section should use DS Person Card.

**To-Do:**
- [ ] Go to DS Lookbook > Person Card
- [ ] Analyze structure:
  - Avatar/name layout
  - Metadata display
  - Action buttons placement
- [ ] Refactor your family cards to match

**Example structure to match:**
```html
<!-- DS Person Card likely has: -->
<div class="ds-person-card">
  <img class="ds-avatar" src="..." />
  <div class="ds-person-info">
    <h3 class="ds-person-name">...</h3>
    <p class="ds-person-meta">...</p>
  </div>
  <div class="ds-person-actions">
    <button class="ds-button">...</button>
  </div>
</div>
```

---

### Task 3.3: Replace Status Badges
**Current:** Colored pills/labels
**Target:** DS Badge component

**To-Do:**
- [ ] Go to DS Lookbook > Badge
- [ ] Note: Variants (primary, secondary, success, warning, danger)
- [ ] Map your statuses:
  - "Enquiry" → [DS variant]
  - "Application Submitted" → [DS variant]
  - "Offer Made" → [DS variant]
  - etc.
- [ ] Replace all status displays with DS Badge

**Code task:**
```html
<!-- OLD -->
<span class="status-enquiry">Enquiry</span>

<!-- NEW -->
<span class="ds-badge ds-badge--[variant]">Enquiry</span>
```

---

### Task 3.4: Replace Forms & Filters
**Current:** Custom dropdowns, inputs
**Target:** DS Form Controls + Dropdown

**Prompt:** All filter dropdowns and form inputs must match DS.

**To-Do:**
- [ ] Go to DS Lookbook > Dropdown
- [ ] Go to DS Lookbook > Form Controls
- [ ] Replace filters:
  - "All Statuses" dropdown → DS Dropdown
  - "All Years of Entry" dropdown → DS Dropdown
  - "All Schools" dropdown → DS Dropdown
- [ ] Replace form inputs (if any inline forms):
  - Text inputs → DS Input
  - Selects → DS Select
  - Buttons → DS Button variants

**Critical:** Do dropdowns have:
- Correct hover states?
- Correct focus states?
- Proper spacing?
- Icons in correct position?

---

### Task 3.5: Replace Navigation Sidebar
**Current:** Custom sidebar with icons
**Target:** DS Navigation pattern

**To-Do:**
- [ ] Check DS for navigation/sidebar component
- [ ] Match:
  - Icon styling (size, color)
  - Active state indicator
  - Hover states
  - Typography
  - Spacing between items
- [ ] Ensure icons align with DS icon set (if specified)

---

## PHASE 4: INTERACTIONS & STATES (2 hours)

### Task 4.1: Hover States
**Prompt:** Every interactive element needs DS hover state.

**To-Do:**
- [ ] Buttons: Hover matches DS button hover
- [ ] Table rows: Hover matches DS table row hover
- [ ] Links: Hover matches DS link hover
- [ ] Cards: Hover elevation/shadow matches DS
- [ ] Dropdown items: Hover background matches DS

**Test method:** Hover over everything, screenshot, compare to DS

---

### Task 4.2: Focus States
**Prompt:** Accessibility requires visible focus states.

**To-Do:**
- [ ] Tab through entire interface
- [ ] Check: Is focus ring visible?
- [ ] Check: Does it match DS focus style?
- [ ] Check: Focus order is logical?

**Common pattern:**
```css
:focus {
  outline: 2px solid var(--ds-primary);
  outline-offset: 2px;
}
```

---

### Task 4.3: Active/Selected States
**Prompt:** Current selection must be clear.

**To-Do:**
- [ ] Selected table row → matches DS selected state
- [ ] Active nav item → matches DS active state
- [ ] Active button → matches DS active state
- [ ] Open dropdown → matches DS open state

---

## PHASE 5: ACCESSIBILITY & RESPONSIVE (2 hours)

### Task 5.1: Keyboard Navigation
**To-Do:**
- [ ] Tab through entire page (no mouse)
- [ ] Can you reach every interactive element?
- [ ] Is focus visible at all times?
- [ ] Does Enter/Space activate buttons?
- [ ] Does Escape close modals/dropdowns?
- [ ] Are there any keyboard traps?

---

### Task 5.2: Screen Reader Test
**To-Do:**
- [ ] Turn on VoiceOver (Mac: Cmd+F5) or NVDA
- [ ] Navigate your page
- [ ] Check: Are tables announced properly?
- [ ] Check: Are buttons labeled?
- [ ] Check: Are states announced (expanded/collapsed)?
- [ ] Check: Any unlabeled elements?

---

### Task 5.3: Responsive Check
**Prompt:** Must work on mobile, tablet, desktop.

**To-Do:**
- [ ] Mobile (375px width):
  - [ ] Sidebar becomes hamburger menu?
  - [ ] Table becomes horizontal scroll or cards?
  - [ ] Filters collapse?
  - [ ] Touch targets ≥44x44px
- [ ] Tablet (768px):
  - [ ] Layout adjusts gracefully
  - [ ] Sidebar may be collapsible
- [ ] Desktop (1440px):
  - [ ] Full layout visible
  - [ ] No horizontal scroll

**Test method:** Chrome DevTools → Device Toolbar

---

## PHASE 6: DEV HANDOFF PREP (1 hour)

### Task 6.1: Clean Code
**To-Do:**
- [ ] Remove unused CSS
- [ ] Organize: DS imports → custom overrides → page-specific
- [ ] Comment what's custom vs. DS
- [ ] Minify for production (optional)

---

### Task 6.2: Documentation
**Create README.md:**
```markdown
# MAT+ Events UI

## Design System
- Source: Design21 Jan2026 (DS Lookbook)
- URL: https://designsaplus.com/lookbook/

## Components Used
- Table (for student lists)
- Person Card (for family details)
- Badge (for status)
- Dropdown (for filters)
- Button (for actions)

## Custom Components
- [List any you built from scratch]

## Breakpoints
- Mobile: < 768px
- Tablet: 768px - 1024px
- Desktop: > 1024px

## Assets
- [List any images/icons used]
```

---

### Task 6.3: Screenshots for Dev
**To-Do:**
- [ ] Screenshot every state:
  - Default view
  - With filters applied
  - Table row hover
  - Table row selected
  - Modal/drawer open
  - Mobile view
  - Tablet view
- [ ] Annotate with measurements if needed
- [ ] Save in `/assets/screenshots/`

---

## FINAL CHECKLIST

Before saying "done":

- [ ] **Visual QA:** Side-by-side with DS Lookbook — matches?
- [ ] **Interaction QA:** All hover/focus/active states work?
- [ ] **Accessibility:** Keyboard nav + screen reader tested?
- [ ] **Responsive:** Mobile, tablet, desktop all good?
- [ ] **Code quality:** Clean, commented, organized?
- [ ] **Documentation:** README complete?
- [ ] **Assets:** Screenshots captured?

---

## TIMELINE

| Phase | Time | Cumulative |
|-------|------|------------|
| 1. Audit | 30 min | 30 min |
| 2. Visual | 4 hrs | 4.5 hrs |
| 3. Components | 5 hrs | 9.5 hrs |
| 4. Interactions | 2 hrs | 11.5 hrs |
| 5. A11y/Responsive | 2 hrs | 13.5 hrs |
| 6. Handoff | 1 hr | 14.5 hrs |

**Realistic:** 2 days (14-15 hours total)

---

## QUICK REFERENCE: DS URLs

- **Event Card:** https://designsaplus.com/lookbook/inspect/components/event_card/comprehensive
- **Person Card:** https://designsaplus.com/lookbook/inspect/components/person_card/comprehensive
- **Table:** https://designsaplus.com/lookbook/inspect/components/table/comprehensive
- **Badge:** https://designsaplus.com/lookbook/inspect/components/badge/comprehensive
- **Button:** https://designsaplus.com/lookbook/inspect/components/button/comprehensive
- **Colors:** https://designsaplus.com/lookbook/inspect/components/colors/comprehensive

---

*Good luck! 🎨*