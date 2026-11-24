# Problem Statement, Success Criteria & Prioritization Matrix
**Track:** UI/UX Design | **Task:** 01 — User Research and Accessibility Audit  
**Author:** Kamalini  

---

## 1. Problem Definition & Framing

### The Core Problem
Student interns on the EdVyro platform experience significant cognitive friction, submission anxiety, and task failure caused by:
1. **Ambiguous Information Architecture:** Critical submission criteria and downloadable resources are visually camouflaged within body copy.
2. **Deterministic Feedback Failure:** Form submission states lack real-time validation, loading indicators, and explicit completion receipts, resulting in accidental double-submissions.
3. **Assistive & Mobile Exclusion:** Sub-optimal contrast ratios, missing keyboard focus rings, broken modal focus traps, and sub-44px touch targets systematically disadvantage mobile and low-vision learners.
4. **Session Vulnerability:** Unsaved draft states penalize students operating under intermittent mobile connectivity or on shared family hardware.

---

## 2. "How Might We" (HMW) Statements

* **HMW 1 (Clarity & Guidance):** How might we structure task briefs so that students with limited time or technical vocabulary can immediately grasp passing requirements and locate materials in under 15 seconds?
* **HMW 2 (Submission Reassurance):** How might we provide unmistakable, real-time feedback during link upload to eliminate anxiety and prevent duplicate submissions?
* **HMW 3 (Session Resilience):** How might we preserve student progress silently in the background so interruptions or timeouts never destroy work?
* **HMW 4 (Universal Accessibility):** How might we ensure complete keyboard predictability and WCAG 2.1 AA visual contrast across all devices and magnification levels?
* **HMW 5 (Feedback Recovery):** How might we turn reviewer rejection into an actionable checklist of revisions rather than an ambiguous dead-end?

---

## 3. Measurable Success Criteria

To scientifically evaluate the upcoming redesign in Task 03 (Wireframes & Information Architecture), the following benchmark criteria are established:

| Category | Target Metric | Baseline (Audit) | Target Goal (Redesign) | Evaluation Method |
| :--- | :--- | :---: | :---: | :--- |
| **Accessibility** | WCAG 2.1 AA Violations | 9 Violations | **0 Violations (100% Pass)** | Automated axe-core & manual keyboard audit |
| **Usability** | System Usability Scale (SUS) | 58.5 / 100 | **≥ 82.0 / 100 ("A" Grade)** | 10-question SUS post-test survey |
| **Efficiency** | Time-on-Task (Resource Download) | 54 seconds | **≤ 15 seconds** | Moderated usability timing tests |
| **Reliability** | Duplicate Submission Error Rate | 38% | **< 2%** | Double-click prevention & disabled loading state |
| **Form Resilience** | Submission Abandonment Rate | 24% | **< 5%** | Client-side `localStorage` auto-draft recovery |
| **Touch Ergonomics**| Interactive Touch Target Size | 26px - 30px | **≥ 48px x 48px** | CSS layout measurement at 360px viewport |

---

## 4. Problem Prioritization Matrix (Portfolio Upgrade)

Using an **Impact vs. Effort** prioritization methodology, findings are categorized to maximize user value during initial wireframing sprints:

### Impact vs Effort 2x2 Grid

| Quadrant | High Impact | Low Impact |
| :---: | :--- | :--- |
| **Low Effort** <br> *(Quick Wins — Sprint 1)* | • Add explicit submit loading spinner & disable button on click.<br>• Implement `localStorage` draft saving on text inputs.<br>• Fix contrast on badges and input placeholder text.<br>• Add high-contrast `:focus-visible` outline rings. | • Adjust table cell padding.<br>• Add tooltip definitions for technical terms. |
| **High Effort** <br> *(Major Projects — Sprint 2)* | • Build accessible modal dialog system with strict focus trapping.<br>• Redesign submission flow with real-time URL validation.<br>• Implement interactive checklist for reviewer feedback recovery. | • Implement customizable dark mode theme.<br>• Multi-language localization support. |

---

## 5. Next Steps: Roadmap to Task 03

The research and audit directly inform the deliverables for **Task 03 (Information Architecture and Wireframes)**:

1. **Information Architecture (User Flow):**
   - Create a clean 3-step submission user flow: *Task Overview → Resource Download & Pre-check → Submit Proof & Receive Instant Receipt*.
2. **Responsive Low-Fidelity Wireframes:**
   - Design low-fi mobile (360px) and desktop (1440px) wireframes embodying the 7 required states:
     - **Loading State:** Skeleton loaders for briefs and submit spinner.
     - **Empty State:** First-time onboarding screen with guided hints.
     - **Error State:** High-contrast non-color-only inline validation errors.
     - **Success State:** Verified submission card with timestamp and review SLA.
     - **Disabled State:** Semantic `aria-disabled="true"` button state.
     - **Focus State:** 3px accessible focus ring.
     - **Narrow-Screen State:** 360px single-column layout with 48px touch targets.
