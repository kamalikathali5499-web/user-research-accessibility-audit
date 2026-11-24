# Detailed Accessibility Audit: EdVyro Student Support Portal
**Standard:** Web Content Accessibility Guidelines (WCAG) 2.1 Level AA  
**Auditor:** Kamalini (UI/UX Design Track)  
**Scope:** Assignment Briefs, Resource Download Hub, Submission Modal, and Reviewer Feedback Banner  
**Tested Viewports:** 360px (Mobile), 768px (Tablet), 1440px (Desktop), and 200% Zoom / 400% Zoom Reflow  

---

## 1. Executive Conformance Summary

| Conformance Principle | Tested Criteria | Pass | Fail | Warning | Score |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **1. Perceivable** | 9 | 5 | 3 | 1 | 55.5% |
| **2. Operable** | 8 | 5 | 3 | 0 | 62.5% |
| **3. Understandable** | 5 | 3 | 2 | 0 | 60.0% |
| **4. Robust** | 3 | 3 | 0 | 0 | 100% |
| **Total** | **25** | **16** | **8** | **1** | **64.0%** |

---

## 2. Navigation Audit

### 2.1 Bypass Blocks (WCAG 2.4.1 - Level A) — ❌ FAIL
* **Observation:** The portal lacks a "Skip to Content" mechanism.
* **Evidence:** Keyboard and screen reader users must navigate past 18 repetitive global header navigation links before reaching the `<main>` task brief content.
* **Impact:** High friction for motor-impaired and screen reader users (e.g., Ravi).
* **Remediation:** Add a skip link as the very first focusable element inside `<body>`:
  ```html
  <a href="#main-content" class="skip-link">Skip to main content</a>
  ```
  ```css
  .skip-link {
    position: absolute;
    top: -999px;
    left: 16px;
    background: #6d28d9;
    color: #ffffff;
    padding: 12px 20px;
    border-radius: 8px;
    z-index: 1000;
  }
  .skip-link:focus {
    top: 16px;
  }
  ```

### 2.2 Focus Order & Trap (WCAG 2.4.3 - Level A) — ❌ FAIL
* **Observation:** When the submission modal opens, keyboard focus remains stuck on the triggering button in the background page.
* **Evidence:** Pressing `Tab` cycles through links underlying the dimmed backdrop rather than entering the modal input fields.
* **Impact:** Severely disorienting for blind and visually impaired users.
* **Remediation:** Implement an accessible focus trap using the HTML `<dialog>` element or JavaScript focus listener that automatically focuses the first input upon open and traps `Tab` cycles within the modal until explicitly dismissed.

### 2.3 Focus Visible (WCAG 2.4.7 - Level AA) — ❌ FAIL
* **Observation:** The stylesheet contains global resets `outline: 0;` and `outline: none;` on `.button`, `.filter-pill`, and `input` elements.
* **Evidence:** Keyboard navigation gives no visual indicator of where cursor focus currently resides.
* **Remediation:** Restore high-contrast focus rings:
  ```css
  :focus-visible {
    outline: 3px solid #6d28d9;
    outline-offset: 2px;
  }
  ```

---

## 3. Readability & Typography Audit

### 3.1 Content Structure & Headings (WCAG 1.3.1 - Level A) — ⚠️ WARNING
* **Observation:** The page relies on visual styling (e.g., `<p class="eyebrow">` and `<strong>`) to simulate heading hierarchy instead of semantic heading tags.
* **Impact:** Screen reader rotor tools cannot generate an accurate table of contents for students scanning the document.
* **Remediation:** Nest headings strictly from `<h1>` down to `<h3>` without skipping levels.

### 3.2 Text Spacing & Reflow (WCAG 1.4.10 / 1.4.12 - Level AA) — ✅ PASS with Notes
* **Observation:** Body font size is `16px` with a line-height of `1.55`, which satisfies WCAG readability baselines.
* **Reflow Test at 400% Zoom (320px CSS equivalent):** The page content reflows into a single column without requiring two-dimensional scrolling.

### 3.3 Plain Language & Cognitive Readability
* **Automated Score:** Flesch-Kincaid Grade Level = **11.4** (College sophomore level).
* **Target Grade:** **7.0 - 8.5** (Inclusive secondary school standard).
* **Recommendation:** Eliminate ambiguous system jargon such as *"evidence envelope"*, *"rechallenge"*, and *"payload constraints"*, substituting plain language terms like *"proof link"*, *"submission details"*, and *"file size guidelines"*.

---

## 4. Color Contrast Audit

All measurements performed against standard WCAG contrast luminance specifications:
- **Normal text (< 18pt or < 14pt bold):** Minimum ratio **4.5:1**
- **Large text (≥ 18pt or ≥ 14pt bold) & UI controls:** Minimum ratio **3.0:1**

| Element Tested | Foreground Hex | Background Hex | Contrast Ratio | WCAG AA Req. | Result | Remediation |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| **Header Title (h1)** | `#21152c` | `#ffffff` | **15.8:1** | 4.5:1 | ✅ Pass | Keep current value. |
| **Body Paragraph** | `#596274` | `#ffffff` | **6.1:1** | 4.5:1 | ✅ Pass | Keep current value. |
| **Download Button Text** | `#ffffff` | `#6d28d9` | **8.2:1** | 4.5:1 | ✅ Pass | Keep current value. |
| **Secondary Button** | `#56237a` | `#eee7f6` | **6.2:1** | 4.5:1 | ✅ Pass | Keep current value. |
| **Muted Meta Badges** | `#9ca3af` | `#faf8fc` | **2.6:1** | 4.5:1 | ❌ **FAIL** | Darken badge font to `#4b5563` (7.0:1). |
| **Input Placeholder** | `#b0b7c3` | `#ffffff` | **2.2:1** | 4.5:1 | ❌ **FAIL** | Increase placeholder contrast to `#64748b` (4.6:1). |
| **Cyan Brief Callout Border** | `#2fb3e3` | `#ffffff` | **1.9:1** | 3.0:1 | ❌ **FAIL** | Darken border to `#0284c7` (3.9:1) for UI boundary visibility. |
| **Warning Banner Text** | `#654b17` | `#fff9e9` | **7.4:1** | 4.5:1 | ✅ Pass | Keep current value. |

---

## 5. Forms & Interactive Elements Audit

### 5.1 Labels & Instructions (WCAG 3.3.2 - Level A) — ❌ FAIL
* **Observation:** Input fields in the submission modal lack explicit `<label for="...">` tags and instead use inline placeholder text: `<input placeholder="Enter link here">`.
* **Impact:** Once a student starts typing, the prompt vanishes. Screen readers identify the input solely as "Edit text, blank" without context.
* **Remediation:**
  ```html
  <div class="form-group">
    <label for="submission-url" class="form-label">
      Repository or View-Only Document URL <span class="required">*</span>
    </label>
    <input 
      type="url" 
      id="submission-url" 
      name="submission-url" 
      class="form-input" 
      required 
      aria-describedby="url-hint"
      placeholder="https://github.com/username/project">
    <span id="url-hint" class="form-hint">Must be public or view-only without login credentials.</span>
  </div>
  ```

### 5.2 Error Identification & Non-Color Dependence (WCAG 3.3.1 / 1.4.1) — ❌ FAIL
* **Observation:** When an invalid link or empty field is submitted, the input border simply turns red (`#ef4444`).
* **Impact:** Students with color vision deficiencies (protanopia/deuteranopia) cannot detect the error.
* **Remediation:** Provide an SVG alert icon, a bold error message, and `aria-invalid="true"` with `aria-live="polite"` feedback.

---

## 6. Mobile Usability Audit (360px Viewport)

### 6.1 Viewport Configuration (WCAG 1.4.4 - Level AA) — ✅ PASS
* **Meta tag:** `<meta name="viewport" content="width=device-width, initial-scale=1">` correctly specified.
* **Pinch-to-zoom:** Not blocked; users can zoom up to 500% freely.

### 6.2 Touch Target Sizes (WCAG 2.5.5 / 2.5.8 - Level AA) — ❌ FAIL
* **Measurement:**
  - Resource download links in checklists: **28px height** (Fail; requirement is ≥ 44px x 44px).
  - Modal dismiss "X" button: **30px x 30px** (Fail).
* **Thumb Zone Analysis:** Critical submission actions are positioned at the very top right of the mobile screen, forcing awkward one-handed stretching on devices with 6.5" displays.
* **Remediation:**
  - Pad touch targets to a minimum of **48px x 48px**.
  - Anchor primary CTA buttons to a sticky bottom navigation bar within natural thumb reach.
