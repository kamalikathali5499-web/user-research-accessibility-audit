# User Research Report: Student Support Portal
**Track:** UI/UX Design | **Task:** 01 — User Research and Accessibility Audit  
**Author:** Kamalini  
**Methodology:** Semi-structured user interviews, task-based usability testing (n=3), and heuristic evaluation.

---

## 1. Research Objectives

1. Identify the friction points students experience when reviewing task briefs and downloading necessary templates/datasets.
2. Uncover the anxieties and errors associated with uploading proof links and submitting assignments under real-world constraints (poor data connectivity, shared devices, assistive devices).
3. Evaluate how students interpret reviewer rejection feedback and determine what design elements prevent successful resubmission.

---

## 2. Participant Personas

### Persona 1: Asha (19) — The Mobile-First Intern
* **Demographics:** 1st year engineering student; Tier-2 city; using a budget Android smartphone with intermittent 3G/4G connectivity.
* **Tech Literacy:** Comfortable with social mobile apps, but first time navigating an enterprise/internship submission dashboard.
* **Core Need:** Plain instructions, minimal data footprint, and immediate feedback confirming file receipt.
* **Quote:** *"If there is no progress wheel, I think the app froze, so I tap again."*

### Persona 2: Ravi (22) — The Assistive Tech User
* **Demographics:** Final year student; severe visual impairment (low vision); uses screen magnification (200%-300%) and keyboard navigation on a Windows laptop.
* **Tech Literacy:** High technical proficiency, but frustrated by poorly constructed web components.
* **Core Need:** High-contrast visual focus indicators, scalable text that doesn't break page layouts, and predictable tab flow.
* **Quote:** *"When the outline disappears, I have to guess which button will activate when I press Enter."*

### Persona 3: Meera (20) — The Time-Constrained Sharer
* **Demographics:** Working student; shares a single family tablet and home desktop with siblings; study slots limited to 20-30 minute windows.
* **Tech Literacy:** Moderate; multi-tasks between home duties and study.
* **Core Need:** Automatic draft saving, seamless session recovery, and clear indicators of what remains before final submission.
* **Quote:** *"Losing 20 minutes of written work because the tab timed out makes me want to quit for the day."*

---

## 3. Five Core Interview & Survey Questions

1. **Question 1 (Expectation & Comprehension):**
   *"When you first land on an assignment or project brief page, what information do you look for within the first 10 seconds, and how confident are you about what constitutes a passing submission?"*
2. **Question 2 (Resource Discovery):**
   *"Can you describe any difficulty you had finding the starter kits, checklists, or datasets required for your task? What visual cues were missing?"*
3. **Question 3 (Submission Confidence):**
   *"Walk me through what happens when you paste your proof link and click submit. Did the platform make you feel 100% sure your submission was safely stored and queued for review?"*
4. **Question 4 (Error Recovery & Feedback):**
   *"If your submission is rejected or needs revisions, how clear is the feedback? Do you know exactly which criteria failed and how to resubmit without starting over?"*
5. **Question 5 (Physical & Environmental Friction):**
   *"What physical or device-specific barriers (e.g. tiny touch buttons, invisible focus, screen timeouts, poor contrast in sunlight) have caused you to abandon a session?"*

---

## 4. Usability Testing & Empirical Participant Responses

### Session 1: Asha (Device: Redmi 10 Android, Chrome Mobile, 3G Network)
* **Assigned Tasks:**
  1. Find the starter checklist download.
  2. Enter a simulated GitHub repository link and submit.
* **Observations:**
  - Took 42 seconds to locate the checklist link. She scrolled past it twice because the link was styled as an inline purple phrase without button borders or an icon.
  - On the submission modal, she pasted the link and pressed "Submit". Because the 3G network latency was ~1800ms and the button displayed no spinner or disabled state, Asha tapped the button a second time.
  - The second click triggered an uncaught exception: *"Error 409: Duplicate submission detected"*, creating immense panic.
* **Participant Feedback:**
  > *"I felt like I broke the portal. I didn't know if my work went through or if I was disqualified for submitting twice. A simple loading wheel would have stopped me from tapping again."*

### Session 2: Ravi (Device: Windows 11 Laptop, Chrome, 200% Zoom, Keyboard Only)
* **Assigned Tasks:**
  1. Navigate to the task instructions using the `Tab` key.
  2. Tab into the submission modal, complete the link field, and dismiss the modal.
* **Observations:**
  - Upon pressing `Tab`, there was no skip link, requiring 18 repetitive tab presses to get past the navigation header.
  - When tabbing onto the "Download Starter Checklist" button, the visual outline vanished (`outline: none` in CSS), forcing Ravi to inspect the browser status bar at the bottom to verify focus.
  - When opening the modal dialog, focus remained behind the modal on the background page. When Ravi pressed `Tab`, focus shifted to links outside the viewport rather than the URL input box inside the dialog.
* **Participant Feedback:**
  > *"When the focus outline is turned off, the web page becomes invisible to keyboard users. At 200% zoom, if focus jumps behind a popup dialog, I am completely lost."*

### Session 3: Meera (Device: Shared iPad Air, Safari Mobile)
* **Assigned Tasks:**
  1. Open task submission dialog.
  2. Fill out personal reflection notes (50 words) and proof link.
  3. Close browser tab to simulate family interruption, reopen after 15 minutes.
* **Observations:**
  - Meera spent 12 minutes drafting a detailed methodology explanation in the text area.
  - When forced to close the tab and reopen it, the portal had logged out the session. Upon logging in, the form fields were completely blank. No `localStorage` draft backup existed.
* **Participant Feedback:**
  > *"I have 30 minutes between helping my family. If the website doesn't remember what I typed when the session refreshes, it wastes my entire study window."*

---

## 5. Synthesis of Research Findings

1. **Submission Feedback Void (Critical):** Users suffer severe anxiety due to an absence of immediate visual confirmation (spinners, disabled submit buttons, confirmation receipts).
2. **Keyboard & Assistive Accessibility Traps (Critical):** Low-vision and keyboard-only users encounter missing focus rings, absent skip navigation, and modal focus traps.
3. **Absence of State Persistence (Critical):** Novice and shared-device users risk complete loss of typed explanations upon network dropouts or session timeouts.
4. **Discoverability Deficit (Moderate):** Key assets (checklists, seed data) blend into copy rather than presenting high-visibility interactive affordances.
