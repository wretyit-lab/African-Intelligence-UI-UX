[DESIGN (2).md](https://github.com/user-attachments/files/33730085/DESIGN.2.md)[design-v2.md](https://github.com/user-attachments/files/33730081/design-v2.md)[design.md](https://github.com/user-attachments/files/33730029/design.md)
# African Intelligence — Platform UI/UX Design System & Master Prompts

## Executive Overview
This document compiles the complete UI/UX specifications, visual identity design tokens, interaction flows, and developer-ready front-end prompts for the **African Intelligence** exam prep and graduation platform. 

Designed specifically for Nigerian students preparing for national examinations (**WAEC SSCE/BECE**, **NECO SSCE/BECE**, **JAMB/UTME**, and **Custom Academic Tracks**), the platform acts as a trusted **academic coach rather than a shortcut ghostwriter** [1, 2]. The design system prioritizes a warm, paper-inspired aesthetic, cultural resonance through traditional Adire textile patterns, and technical optimizations for low-data usage and battery conservation on budget Android devices [3].

---

## Table of Contents
1. [Global Visual Identity & Token Architecture](#1-global-visual-identity--token-architecture)
2. [Module 1: Onboarding & Sign-Up Flow (Streamlined 60-Second Setup)](#2-module-1-onboarding--sign-up-flow)
3. [Module 2: Goal-Led Dashboard (Progress Home)](#3-module-2-goal-led-dashboard-progress-home)
4. [Module 3: Exam Hub Architectures & Track Design](#4-module-3-exam-hub-architectures--track-design)
5. [Master Front-End Build Prompt: WAEC & NECO Module (Pages 1–8)](#5-master-front-end-build-prompt-waec--neco-module-pages-18)
6. [Animation, Accessibility & PWA Performance Standards](#6-animation-accessibility--pwa-performance-standards)

---

## 1. Global Visual Identity & Token Architecture

Grounded in the **African Intelligence Visual Identity Guide**, the interface avoids generic corporate blues and cold technology greys in favor of warm paper-like neutrals, indigo dye traditions (Adire), red-earth Laterite soil, Marigold, and Leaf green [3].

```css
:root {
  /* Surface & Background Neutrals */
  --bg: #FBF7F0;          /* Chalk paper neutral */
  --surface: #FFFFFF;     /* Clean surface card */
  --surface-2: #F3ECE0;   /* Sand raised surface & input field fill */
  --border: #E3DACB;      /* Card outline & divider line */
  --text: #1E1B2E;        /* Primary high-contrast text */
  --text-muted: #5B5670;  /* Secondary text & captions */

  /* Brand & Module Specific Tokens */
  --primary: #3A2E9A;      /* Adire Indigo (primary actions, links) */
  --on-primary: #FFFFFF;   /* Text on primary buttons */
  --primary-tint: #ECE9FB; /* Active card highlight & soft fill */
  --exam-accent: #B97700;  /* Exam Marigold (headers, progress rings) */
  --highlight: #F2A91B;    /* Marigold milestone & streak accent */

  /* Feedback & Validation States */
  --success: #1B7F45;     /* Leaf Green (correct answer, verified item) */
  --try-again: #C4532D;   /* Laterite Soil (incorrect answer / "Not yet" coaching) */
  --error: #C0263F;       /* Reserved strictly for system/payment failures */
  --focus: #3A2E9A;       /* Focus ring with 2px offset */

  /* Geometry & Radii */
  --radius-card: 12px;    /* Card & modal corner radius */
  --radius-btn: 10px;     /* Button corner radius */
  --radius-chip: 999px;   /* Selection chip & pill radius */

  /* Typography Families */
  --font-head: "Fraunces", Georgia, serif;                        /* Soft, academic serif */
  --font-body: "Nunito Sans", system-ui, -apple-system, sans-serif;/* Open, rounded sans-serif */
  --font-mono: ui-monospace, SFMono-Regular, "Courier New", monospace; /* Tabular numerals */
}

/* Dark Mode Theme Mapping (Soft ink-tinted sheets) */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --bg: #14122B;          /* Night Ink background */
    --surface: #1D1A3A;     /* Deep Indigo sheet */
    --surface-2: #272349;   /* Raised indigo surface */
    --border: #38335E;      /* Dark border outline */
    --text: #F1EDE4;        /* Soft paper white text */
    --text-muted: #B3AEC6;  /* Muted dark caption */
    --primary: #A79BFF;      /* Indigo Glow */
    --on-primary: #14122B;  /* Dark text on glowing button */
    --primary-tint: #2C2663; /* Soft indigo selected state */
    --exam-accent: #F6B93B;  /* Soft Exam Marigold */
    --highlight: #F6B93B;    /* Milestone gold */
    --success: #5FD08C;     /* Soft Leaf Green */
    --try-again: #F08A63;   /* Soft Laterite */
    --error: #FF7A8F;       /* Soft system error red */
  }
}

/* Manual OLED Battery Saver Mode Override */
:root[data-theme="battery"] {
  --bg: #0B0A18; /* True Dark OLED black for power conservation */
}
```

### Typography & Layout Rules
* **Headings**: Fraunces (SemiBold 600 / Bold 700) for academic warmth [3].
* **Body & Options**: Nunito Sans (Regular 400 / SemiBold 600) [3].
* **Exam Question Body**: Set to **18px font size with 28px line-height** (Nunito Sans 400) for maximum legibility under timed examination pressure.
* **Timers, Scores & Currency**: System Monospace font with **tabular numerals** so countdown digits do not jump during execution. Native support for the **₦ (Naira)** glyph (`₦ 2,500`) [3].
* **Ergonomic Touch Targets**: Minimum **48px height** for all primary buttons, social auth triggers, and option choices; minimum **44px** for secondary pills and skip links.

---

## 2. Module 1: Onboarding & Sign-Up Flow

### Overview
A low-friction, progressive onboarding process designed to complete in **under 60 seconds** [2]. It gathers the user's preferred name and primary target exam, while keeping secondary details (department, exam date) optional and skippable.

### Master Prompt: Onboarding Screens
```markdown
# UI/UX & FRONT-END BUILD PROMPT: STREAMLINED ONBOARDING FLOW

## SCREEN 1: LIGHT SIGN-UP & PREFERRED NAME
- Header: Logo with Marigold (`#F2A91B`) spark icon. Headline (Fraunces 25px): "Welcome to Your Graduation Companion".
- Input 1: Preferred Name field ("What should your AI Coach call you?").
- Primary Auth Stack (48px Buttons, 10px Radius):
  - "Continue with Google"
  - "Continue with WhatsApp / Phone"
  - "Continue with Apple / Email"
- Microcopy: "By continuing, your progress and uploaded materials are protected under NDPA standards."

## SCREEN 2: EXAM TARGET SETUP & PRACTICE PLAN
- Step Indicator: Top bar in Marigold (`#F2A91B`) indicating "Step 2 of 2".
- Headline (Fraunces 25px): "Set Your Exam Target". Sub-headline: "Select your primary exam focus. You can change or add targets anytime."
- Question 1 (MANDATORY - 2x3 Grid View Layout):
  1. 🎓 WAEC / SSCE: West African Senior School Certificate Examination.
  2. ⚡ JAMB / UTME: Joint Admissions and Matriculation Board CBT.
  3. 📚 NECO / BECE: National Examinations Council past questions & syllabus.
  4. 🏫 Junior SSCE / BECE: Junior secondary transition exam prep.
  5. 🧪 Custom Subject Space: Upload your own lecture notes, PDF, or syllabus.
  6. 🌐 Wide Scope Prep: Simultaneous multi-exam preparation.
- Question 2: Department / Field of Study (OPTIONAL)
  - Horizontal scroll pills: `🔬 Science` | `💼 Commercial` | `🎨 Arts` | `🛠️ Technical`
  - Right-aligned text button: "Skip for now" (44px touch target).
- Question 3: Target Exam Date (OPTIONAL)
  - Dropdown selector (e.g., "April 2027", "May 2027", "Self-Paced").
  - Right-aligned text button: "Skip for now" (44px touch target).
- Primary CTA Button (48px height, `--primary` background): "Complete Setup & Go to Dashboard".

## AESTHETIC & PATTERN STYLING
- Background: Chalk neutral (`#FBF7F0`) with faint repeating geometric Adire textile SVG pattern (4% to 6% opacity).
- Card Elevation: Surface white (`#FFFFFF`) cards with 1px soft border (`#E3DACB`) and soft ambient shadows.
```

---

## 3. Module 2: Goal-Led Dashboard (Progress Home)

### Overview
A goal-driven home screen that serves as the student's central command center [1, 2]. It features a **Graduation-Readiness Ring**, an active study plan switcher, exam track hubs, practice analytics, and persistent access to the **Sidekick AI Coach**.

### Master Prompt: Dashboard
```markdown
# DESIGN PROMPT: GOAL-LED DASHBOARD (PROGRESS HOME)

## OVERVIEW & GOAL
Create a warm, encouraging home dashboard for "African Intelligence". The page acts as a personal command center answering: "How ready am I to graduate and pass my exams?"

## KEY SECTIONS (TOP TO BOTTOM)

1. TOP BAR & WELCOME:
   - Greeting: "Welcome back, Temi!" and department tag ("Science Track").
   - Controls: Battery Saver Mode toggle (`#0B0A18`) and Data Saver status indicator.

2. STUDY PLAN SWITCHER BANNER:
   - Active Plan Card: "Active Plan: JAMB 2027 Engineering (Week 4 of 12)".
   - Today's Task: "Today's Focus: Physics - Optics & Waves (45 mins left)".
   - Actions: "Resume Today's Study" (Primary Indigo) & "Switch Study Plan" dropdown.

3. GRADUATION-READINESS WHEEL:
   - Multi-segment progress ring ("68% Ready to Graduate") showing stepping stones ending in a graduation cap icon.

4. EXAM SYSTEM SCOPE (2x2 GRID):
   - 📚 WAEC / SSCE Hub
   - ⚡ JAMB / UTME Hub
   - 📝 NECO / BECE Hub
   - 🧪 Custom Exam Studio (Upload lecture notes/PDFs)

5. PRACTICE ANALYTICS & RECENT ACTIVITIES:
   - "Recent Drill: Physics Waves – Score 8/10 (80%)"
   - "Weak Topic Flagged: Optics – Added to today's review"
   - "Uploaded File: Organic_Chemistry_Notes.pdf (Processed)"
   - Action: "View Full Analytics" link.

6. AI TUTOR & COMMUNITY QUICK-ACCESS BAR:
   - 💬 "Chat with Sidekick Coach" (1-tap AI assistance).
   - 👥 "Join Department Study Group" (Peer discussion channels).
```

---

## 4. Module 3: Exam Hub Architectures & Track Design

### Architectural Matrix

| Dimension | WAEC & NECO Hubs (Dual-Mode) | JAMB / UTME Hub (Speed CBT) | Custom Exam Studio Track |
| :--- | :--- | :--- | :--- |
| **Exam Levels** | Senior SSCE & Junior BECE | UTME / University Entrance | User-defined / Tertiary / Professional |
| **Paper Formats** | **Paper 1**: Objective (MCQ)<br>**Paper 2**: Essay / Theory | **Pure Objective (MCQ)** across 4 subjects | Flexible (Objective, Essay, or Mixed) |
| **Input Interface** | 48px Radio choices (P1); **Rich Text Editor** with formula tools (P2) | Fast touch targets + Question Grid Palette | Radio buttons or Rich Text Editor |
| **Special Tools** | Formula helper (`x₂`, `x²`, chemical reactions) | **On-Screen System Calculator** | Subject-dependent tools |
| **Grading Engine** | Auto-score (P1); **Rubric-Based AI Coach** (P2) | Rapid CBT score & speed analytics | AI-generated answer key evaluation |

---

## 5. Master Front-End Build Prompt: WAEC & NECO Module (Pages 1–8)

```markdown
# MASTER FRONT-END & UI/UX BUILD PROMPT: WAEC & NECO EXAM MODULE (PAGES 1–8)
# TARGET PLATFORM: AFRICAN INTELLIGENCE PWA (PROGRESSIVE WEB APP)

---

### PAGE 1: WAEC & NECO HUB LANDING & SUBJECT SELECTOR
- Level Switcher Pills: `Senior WAEC SSCE` | `Senior NECO SSCE` | `Junior WAEC / BECE` | `Junior NECO BECE`.
- Offline Pack Status Banner: Download button with tray icon to cache 500+ past questions locally via PWA Workbox.
- Subject Grid: 9 Departmental subjects (Senior Science, Commercial, Arts) or Junior foundational pillars (Basic STEM, Business Studies, Humanities). Shows question count and topic mastery percentage per subject card.

---

### PAGE 2: PRACTICE SESSION CONFIGURATOR
- Mode Selector Cards:
  1. 🔘 Instant Quiz Mode: Real-time feedback and step-by-step AI Coach breakdown per question.
  2. ⭕ Quick Drill ("Single Sway"): Rapid question sweeping; queue hard items into a "Review Later" tray.
  3. ⭕ Timed Exam Simulator: Official time limits; deferred scoring until submission.
- Parameter Controls:
  - Question Volume: Admin default vs. Custom Slider (5 to 50 Qs).
  - Timer Rules: Official Exam Timer vs. Custom Minutes vs. Untimed Relaxed Mode.
  - Content Focus: Verified Questions (2015–2025) vs. Critical Gaps Only.

---

### PAGE 3: DIAGNOSTIC GAP ANALYSIS TEST PAGE
- Assessment: 10 targeted adaptive diagnostic questions.
- Display: 18px Nunito Sans question text with inline SVG vector diagrams (2px stroke, zero bitmap images).
- Output: Post-test Diagnostic Gap Summary displaying topic mastery bars (e.g., Mechanics: 100%, Optics: 33% Critical Gap). Weak topics are auto-routed to the user's active Study Plan.

---

### PAGE 4: PAPER 1 — OBJECTIVE (MCQ) PRACTICE SCREEN
- Top Bar: Subject title, question counter ("Question 8 of 50"), Monospace timer (`42:15`), and "Verified Question" shield badge.
- Question Container: 18px / 28px Nunito Sans text card (`#FFFFFF`).
- Choice Buttons (A, B, C, D): Minimum 48px height.
  - Correct Selection: `--success` Leaf Green border (`#1B7F45`), checkmark SVG draw animation, and "+1 Mark" badge.
  - Incorrect Selection: `--try-again` Laterite Soil border (`#C4532D`), circular arrow icon, and encouraging microcopy ("Not yet. Let's look at this concept together."). NEVER use punitive red screens.
- Sidekick Coach Drawer: Retractable drawer for instant hints, formulas, and syllabus summaries.

---

### PAGE 5: PAPER 2 — ESSAY & THEORY PRACTICE SCREEN (RICH TYPING & AI RUBRIC GRADING)
- Prompt Card: Official WAEC/NECO theory prompt displaying sub-sections and mark allocations (e.g., `(3 Marks)`).
- Rich Response Editor:
  - Minimum height 220px, Sand background (`#F3ECE0`), 1px border.
  - Toolbar: Bold, Italic, Subscript (`x₂`), Superscript (`x²`), and Formula/Chemical Reaction insertion helper.
  - Live word and character counter.
- Rubric-Based AI Coach Evaluation Container (Appears post-submission):
  - Overall score (e.g., `11/12 Marks`).
  - Sub-question point breakdown matched against official WAEC/NECO marking schemes.
  - "Coach Tip" box explaining exact phrasing needed to gain full examiner credit.

---

### PAGE 6: QUICK DRILL ("SINGLE SWAY") & QUEUE SCREEN
- Stack Card Layout: Swipe/sway or click "Add to Review Queue" (moves card into Review Later tray with a `200ms` sway motion) or "Answer Now" (expands choice options).
- Offline Sync Badge: Shows local PWA session storage status.

---

### PAGE 7: TIMED EXAM SIMULATION SCREEN (CBT MODE)
- Zero-Distraction Rule: High-contrast interface without background textile pattern overlays during simulation.
- Top Bar: Monospace countdown timer (`02:29:45`) with tabular numerals and embedded system calculator toggle button.
- Question Palette Drawer: Bottom/side grid showing Answered (Green), Unanswered (White), and Flagged (Marigold) questions.

---

### PAGE 8: SUBJECT PERFORMANCE & DIAGNOSTIC ANALYTICS DASHBOARD
- Mastery Heatmap: Color-coded topic health bars (Strong, Needs Review, Critical Gap).
- Paper 1 vs. Paper 2 Analytics: Comparison chart showing MCQ speed/accuracy vs. written theory mark retention.
- Past Script Attempt Viewer: Re-opens any past typed essay submission to review typed answers side-by-side with official WAEC/NECO marking schemes and AI coach feedback.
```

---

## 6. Animation, Accessibility & PWA Performance Standards

### Vector & Motion Framework (Zero Bitmap Images)
To ensure fast rendering, low mobile data consumption, and offline execution on budget Android devices, **no raster bitmap images (PNG/JPG)** are used [3]. All graphics are rendered as lightweight inline SVGs and CSS keyframe animations:

```css
/* Lightweight CSS Motion Framework (150ms - 250ms gentle easing) */
@keyframes pulseCoach {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.05); opacity: 0.85; }
}

@keyframes swayCard {
  0% { transform: translateX(0) rotate(0deg); }
  50% { transform: translateX(12px) rotate(1.5deg); }
  100% { transform: translateX(0) rotate(0deg); }
}

@keyframes drawSuccessCheck {
  0% { stroke-dashoffset: 24; }
  100% { stroke-dashoffset: 0; }
}

/* Reduced Motion Override for Accessibility */
@media (prefers-reduced-motion: reduce) {
  *, ::before, ::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;

[design (1).md](https://github.com/user-attachments/files/33730066/design.1.md)

---

## 5. Module 4: JAMB / UTME Speed CBT Subsystem (5-Page Architecture)

### Overview
The **JAMB (Joint Admissions and Matriculation Board / UTME)** subsystem is engineered specifically for fast-paced, high-speed Computer-Based Testing (CBT). Unlike WAEC/NECO, JAMB is **purely objective (Multiple Choice Questions only)** and requires candidates to manage **4 subjects simultaneously** (Use of English compulsory + 3 departmental picks) within a strict **120-minute countdown timer** (180 questions total, averaging ~40 seconds per question).

---

### JAMB Page Inventory (5 Dedicated Pages)

#### Page 1: JAMB Hub Landing & 4-Subject Combination Builder
* **Purpose**: Entry portal for JAMB prep; allows students to configure their official 4-subject combination.
* **Key Features**:
  * **Department Preset Builder**: Quick select presets (e.g., *Engineering: English + Math + Physics + Chemistry*; *Medicine: English + Biology + Chemistry + Physics*; *Law: English + Literature + Government + CRS*).
  * **Custom 4-Subject Switcher**: Custom selection dropdowns for non-traditional combinations.
  * **2015–2025 Verified Question Bank Selector** & PWA Offline Pack Downloader.

#### Page 2: JAMB Session & CBT Configurator
* **Purpose**: Pre-test setup to configure practice parameters.
* **Key Features**:
  * **Mode Selection**: *Full 4-Subject UTME Mock (180 Qs / 120 Mins)*, *Single-Subject Speed Drill (40 Qs / 30 Mins)*, or *Instant Quiz Mode*.
  * **Constraint Controls**: Admin default vs. Custom question volume slider (10 to 180 Qs), custom countdown timers, or untimed practice.
  * **Calculated Speed Target Indicator**: Displays target time per question (e.g., "Target: 40 seconds / question").

#### Page 3: Integrated 4-Subject Speed CBT Simulator (Core Exam Screen)
* **Purpose**: High-fidelity, zero-distraction UTME screen simulation featuring a built-in system calculator.
* **Key Features**:
  * **Top Bar**: Monospace master countdown timer (), 4-Subject Tab Switcher (*Use of English | Mathematics | Physics | Chemistry*), and On-Screen System Calculator toggle button.
  * **Question Area**: High-readability 18px / 28px Nunito Sans text with 48px touch targets for choices A–D.
  * **Embedded System Calculator Modal**: Accessible 8-digit / 4-function tabular calculator card for arithmetic subjects.
  * **Question Palette Drawer**: 180-item grid drawer showing Answered (Green), Unanswered (White), and Flagged for Review (Marigold).

#### Page 4: JAMB Instant Quiz & Speed Drill Screen (Single-Subject Mode)
* **Purpose**: Targeted single-subject drill interface with real-time feedback and AI coaching.
* **Key Features**:
  * **Real-Time Feedback**: Correct choices highlight in Leaf Green (); incorrect choices highlight in Laterite Soil () with encouraging guidance.
  * **Sidekick AI Coach Drawer**: Retractable drawer offering instant speed strategies, formula shortcuts, and syllabus breakdowns.

#### Page 5: JAMB UTME Score & Diagnostic Analytics Dashboard
* **Purpose**: Detailed score report and performance diagnostic scaled out of 400 marks.
* **Key Features**:
  * **UTME 400-Point Score Summary**: Displays scores per subject (e.g., *English: 72/100, Physics: 68/100, Chemistry: 75/100, Math: 80/100 = Total: 295/400*).
  * **Speed vs. Accuracy Matrix**: Tabular chart comparing average time per question against accuracy percentage.
  * **Weak Topic Routing**: Automatically exports low-mastery topics into the student's active **Multi-Study Plan**.

---

### Master Build Prompt: JAMB / UTME Module

--bg#FBF7F0#14122B--surface#FFFFFF#1D1A3A--primary#3A2E9A#A79BFF--exam-accent#B97700--success#1B7F45--try-again#C4532D#0B0A18--surface--border--radius-card: 12px--font-mono150ms slideUp--primary150msEnglish: 42/60


  }
}
```

### Accessibility & PWA Constraints
1. **Contrast & Touch Metrics**: All text meets WCAG AA standards (minimum **4.5:1 ratio**). Interactive elements adhere strictly to **48px touch target height**.
2. **Offline-First PWA Sync**: Built with Workbox PWA service workers to cache downloadable question packs, allowing full offline practice during network drops or power outages [2, 3].
3. **Empathetic Coaching Microcopy**: All feedback avoids punitive language ("Failed", "Wrong"). Mistakes trigger supportive guidance in Laterite Soil (`#C4532D`) [3].


[Uploading design-v2.md…](# African Intelligence — Platform UI/UX Design System & Master Prompts

## Executive Overview
This document compiles the complete UI/UX specifications, visual identity design tokens, interaction flows, and developer-ready front-end prompts for **African Intelligence**. 

Designed specifically for Nigerian students preparing for national examinations (**WAEC SSCE/BECE**, **NECO SSCE/BECE**, **JAMB/UTME**, and **Custom Academic Tracks**), the platform acts as a trusted **academic coach rather than a shortcut ghostwriter**. The design system prioritizes a warm, paper-inspired aesthetic, cultural resonance through traditional Adire textile patterns, and technical optimizations for low-data usage and battery conservation on budget Android devices.

---

## Table of Contents
1. [Global Visual Identity & Token Architecture](#1-global-visual-identity--token-architecture)
2. [Module 1: Onboarding & Sign-Up Flow (Streamlined 60-Second Setup)](#2-module-1-onboarding--sign-up-flow)
3. [Module 2: Goal-Led Dashboard (Progress Home)](#3-module-2-goal-led-dashboard-progress-home)
4. [Module 3: WAEC & NECO Dual-Mode Subsystem (Pages 1–8)](#4-module-3-waec--neco-dual-mode-subsystem-pages-18)
5. [Module 4: JAMB / UTME Speed CBT Subsystem (Pages 1–5)](#5-module-4-jamb--utme-speed-cbt-subsystem-pages-15)
6. [Module 5: Custom Exam Studio Subsystem (Pages 1–5)](#6-module-5-custom-exam-studio-subsystem-pages-15)
7. [Module 6: Technical Architecture, Motion Framework & PWA Standards](#7-module-6-technical-architecture-motion-framework--pwa-standards)

---

## 1. Global Visual Identity & Token Architecture

Grounded in the **African Intelligence Visual Identity Guide**, the interface avoids generic corporate blues and cold technology greys in favor of warm paper-like neutrals, indigo dye traditions (Adire), red-earth Laterite soil, Marigold, and Leaf green.

```css
:root {
  /* Surface & Background Neutrals */
  --bg: #FBF7F0;          /* Chalk paper neutral background */
  --surface: #FFFFFF;     /* Clean white card surface */
  --surface-2: #F3ECE0;   /* Sand raised surface & input field fill */
  --border: #E3DACB;      /* Soft card outline & divider line */
  --text: #1E1B2E;        /* Primary high-contrast text */
  --text-muted: #5B5670;  /* Secondary caption & label text */

  /* Brand & Module Specific Tokens */
  --primary: #3A2E9A;      /* Adire Indigo (primary CTAs & links) */
  --on-primary: #FFFFFF;   /* Text on primary active state */
  --primary-tint: #ECE9FB; /* Soft Adire highlight fill */
  --exam-accent: #B97700;  /* Exam Marigold (headers & progress rings) */
  --highlight: #F2A91B;    /* Warm Marigold milestone accent */

  /* Feedback & State Indicators */
  --success: #1B7F45;     /* Leaf Green (correct answer, verified item) */
  --try-again: #C4532D;   /* Laterite Soil (incorrect answer / "not yet" coaching) */
  --error: #C0263F;       /* Reserved strictly for system/payment failures */

  /* Element Geometry */
  --radius-card: 12px;    /* Card corner radius */
  --radius-btn: 10px;     /* Button corner radius */
  --radius-chip: 999px;   /* Fully rounded pill radius */

  /* Typography Families */
  --font-head: "Fraunces", Georgia, serif;                        /* Soft academic serif */
  --font-body: "Nunito Sans", system-ui, -apple-system, sans-serif;/* Readable open sans-serif */
  --font-mono: ui-monospace, SFMono-Regular, "Courier New", monospace; /* Tabular numerals */
}

/* Dark Mode Theme Mapping (Soft Night Ink Sheets) */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --bg: #14122B;          /* Night Ink background */
    --surface: #1D1A3A;     /* Deep Indigo sheet */
    --surface-2: #272349;   /* Raised indigo surface */
    --border: #38335E;      /* Dark border outline */
    --text: #F1EDE4;        /* Soft paper white text */
    --text-muted: #B3AEC6;  /* Muted caption text */
    --primary: #A79BFF;      /* Indigo Glow */
    --on-primary: #14122B;  /* Dark text on glowing button */
    --primary-tint: #2C2663; /* Soft indigo selected fill */
    --exam-accent: #F6B93B;  /* Soft Exam Marigold */
    --success: #5FD08C;     /* Soft Leaf Green */
    --try-again: #F08A63;   /* Soft Laterite */
  }
}

/* Manual Battery Saver Mode Override */
:root[data-theme="battery"] {
  --bg: #0B0A18; /* True Dark OLED black for power conservation */
}
```

### Typography & Formatting Rules
* **Headings**: Fraunces (SemiBold 600 / Bold 700) for academic warmth.
* **Body & Options**: Nunito Sans (Regular 400 / SemiBold 600).
* **Exam Question Body**: Set to **18px font size with 28px line-height** (Nunito Sans 400) for maximum legibility under timed examination pressure.
* **Timers, Scores & Currency**: System Monospace font with **tabular numerals** so countdown digits do not jump during execution. Native rendering support for the **₦ (Naira)** glyph (`₦ 2,500`).
* **Ergonomic Touch Targets**: Minimum **48px height** for all primary buttons, choice options, and social auth triggers; minimum **44px** for secondary pills and skip links.

---

## 2. Module 1: Onboarding & Sign-Up Flow

### Overview
A low-friction, progressive onboarding process designed to complete in **under 60 seconds**. It gathers the user's preferred name and primary target exam, while keeping secondary details (department, exam date) optional and skippable.

### Master Prompt: Onboarding Screens
```markdown
# UI/UX & FRONT-END BUILD PROMPT: STREAMLINED ONBOARDING FLOW

## SCREEN 1: LIGHT SIGN-UP & PREFERRED NAME
- Header: Brand Logo with Marigold (`#F2A91B`) spark icon. Headline (Fraunces 25px): "Welcome to Your Graduation Companion".
- Input 1: Preferred Name field ("What should your AI Coach call you?").
- Primary Auth Stack (48px Buttons, 10px Radius):
  - "Continue with Google"
  - "Continue with WhatsApp / Phone"
  - "Continue with Apple / Email"
- Microcopy: "By continuing, your progress and uploaded materials are protected under NDPA standards."

## SCREEN 2: EXAM TARGET SETUP & PRACTICE PLAN
- Step Indicator: Top bar in Marigold (`#F2A91B`) indicating "Step 2 of 2".
- Headline (Fraunces 25px): "Set Your Exam Target". Sub-headline: "Select your primary exam focus. You can change or add targets anytime in your dashboard."
- Question 1 (MANDATORY - 2x3 Grid View Layout):
  1. 🎓 WAEC / SSCE: West African Senior School Certificate Examination.
  2. ⚡ JAMB / UTME: Joint Admissions and Matriculation Board CBT.
  3. 📚 NECO / BECE: National Examinations Council past questions & syllabus.
  4. 🏫 Junior SSCE / BECE: Junior secondary transition exam prep (Junior WAEC/NECO).
  5. 🧪 Custom Subject Space: Upload your own lecture notes, PDF, or syllabus.
  6. 🌐 Wide Scope Prep: Simultaneous multi-exam preparation.
- Question 2: Department / Field of Study (OPTIONAL)
  - Horizontal scroll pills: `🔬 Science` | `💼 Commercial` | `🎨 Arts` | `🛠️ Technical`
  - Right-aligned text button: "Skip for now" (44px touch target).
- Question 3: Target Exam Date (OPTIONAL)
  - Dropdown selector (e.g., "April 2027", "May 2027", "Self-Paced").
  - Right-aligned text button: "Skip for now" (44px touch target).
- Primary CTA Button (48px height, `--primary` background): "Complete Setup & Go to Dashboard".

## AESTHETIC & PATTERN STYLING
- Background: Chalk neutral (`#FBF7F0`) with faint repeating geometric Adire textile SVG pattern (4% to 6% opacity).
- Card Elevation: Surface white (`#FFFFFF`) cards with 1px soft border (`#E3DACB`) and soft ambient shadows.
```

---

## 3. Module 2: Goal-Led Dashboard (Progress Home)

### Overview
A goal-driven home screen that serves as the student's central command center. It features a **Graduation-Readiness Ring**, an active study plan switcher, exam track hubs, practice analytics, and persistent access to the **Sidekick AI Coach**.

### Master Prompt: Dashboard
```markdown
# DESIGN PROMPT: GOAL-LED DASHBOARD (PROGRESS HOME)

## OVERVIEW & GOAL
Create a warm, encouraging home dashboard for "African Intelligence". The page acts as a personal command center answering: "How ready am I to graduate and pass my exams?"

## KEY SECTIONS (TOP TO BOTTOM)

1. TOP BAR & WELCOME:
   - Greeting: "Welcome back, Temi!" and department tag ("Science Track").
   - Controls: Battery Saver Mode toggle (`#0B0A18`) and Data Saver status indicator.

2. STUDY PLAN SWITCHER BANNER:
   - Active Plan Card: "Active Plan: JAMB 2027 Engineering (Week 4 of 12)".
   - Today's Task: "Today's Focus: Physics - Optics & Waves (45 mins left)".
   - Actions: "Resume Today's Study" (Primary Indigo) & "Switch Study Plan" dropdown.

3. GRADUATION-READINESS WHEEL:
   - Multi-segment progress ring ("68% Ready to Graduate") showing stepping stones ending in a graduation cap icon.

4. EXAM SYSTEM SCOPE (2x2 GRID):
   - 📚 WAEC / SSCE Hub (Senior & Junior BECE)
   - ⚡ JAMB / UTME Hub (Speed CBT Simulator)
   - 📝 NECO / BECE Hub (National Syllabus)
   - 🧪 Custom Exam Studio (Upload lecture notes/PDFs)

5. PRACTICE ANALYTICS & RECENT ACTIVITIES:
   - "Recent Drill: Physics Waves – Score 8/10 (80%)"
   - "Weak Topic Flagged: Optics – Added to today's review"
   - "Uploaded File: Organic_Chemistry_Notes.pdf (Processed)"
   - Action: "View Full Analytics" link.

6. AI TUTOR & COMMUNITY QUICK-ACCESS BAR:
   - 💬 "Chat with Sidekick Coach" (1-tap AI assistance).
   - 👥 "Join Department Study Group" (Peer discussion channels).
```

---

## 4. Module 3: WAEC & NECO Dual-Mode Subsystem (Pages 1–8)

### Subsystem Overview
WAEC and NECO are two distinct national examination bodies that share a dual-paper structure: **Paper 1 (Objective MCQ)** for speed and retrieval, and **Paper 2 (Essay / Theory)** for structured written answers. This module covers both **Senior Secondary (WAEC/NECO SSCE)** and **Junior Secondary (Junior WAEC/NECO BECE)** levels across 8 dedicated pages.

### Master Build Prompt: WAEC & NECO Subsystem (Pages 1–8)

```markdown
# MASTER FRONT-END BUILD PROMPT: WAEC & NECO DUAL-MODE EXAM MODULE (PAGES 1–8)
# TARGET PLATFORM: AFRICAN INTELLIGENCE PWA (PROGRESSIVE WEB APP)

---

### PAGE 1: WAEC & NECO HUB LANDING & SUBJECT SELECTOR
- Level Switcher Pills: `Senior WAEC SSCE` | `Senior NECO SSCE` | `Junior WAEC / BECE` | `Junior NECO BECE`.
- Offline Pack Status Banner: Download button with tray icon to cache 500+ past questions locally via PWA Workbox background sync.
- Subject Grid: 9 Departmental subjects (Senior Science, Commercial, Arts) or Junior foundational pillars (Basic STEM, Business Studies, Humanities). Shows question count and topic mastery percentage per subject card.
- Interaction Motion: Tapping a card elevates it with a 2px Adire Indigo stroke, primary tint background fill (`#ECE9FB`), `1.02x` micro-scale transform, and an animated Leaf Green checkmark SVG draw.

---

### PAGE 2: PRACTICE SESSION CONFIGURATOR
- Mode Selector Cards:
  1. 🔘 Instant Quiz Mode: Real-time feedback and step-by-step AI Coach breakdown per question.
  2. ⭕ Quick Drill ("Single Sway"): Rapid question sweeping; queue hard items into a "Review Later" tray.
  3. ⭕ Timed Exam Simulator: Official time limits; deferred scoring until submission.
- Parameter Controls:
  - Question Volume: Admin default vs. Custom Slider (5 to 50 Qs).
  - Timer Rules: Official Exam Timer vs. Custom Minutes vs. Untimed Relaxed Mode.
  - Content Focus: Verified Questions (2015–2025) vs. Critical Gaps Only.

---

### PAGE 3: DIAGNOSTIC GAP ANALYSIS TEST PAGE
- Assessment: 10 targeted adaptive diagnostic questions.
- Display: 18px Nunito Sans question text with inline SVG vector diagrams (2px stroke, zero bitmap images).
- Output: Post-test Diagnostic Gap Summary displaying topic mastery bars (e.g., Mechanics: 100%, Optics: 33% Critical Gap). Weak topics are auto-routed to the user's active Study Plan.

---

### PAGE 4: PAPER 1 — OBJECTIVE (MCQ) PRACTICE SCREEN
- Top Bar: Subject title, question counter ("Question 8 of 50"), Monospace timer (`42:15`), and "Verified Question" shield badge.
- Question Container: 18px / 28px Nunito Sans text card (`#FFFFFF`).
- Choice Buttons (A, B, C, D): Minimum 48px height.
  - Correct Selection: `--success` Leaf Green border (`#1B7F45`), checkmark SVG draw animation, and "+1 Mark" badge.
  - Incorrect Selection: `--try-again` Laterite Soil border (`#C4532D`), circular arrow icon, and encouraging microcopy ("Not yet. Let's look at this concept together."). NEVER use punitive red screens.
- Sidekick Coach Drawer: Retractable drawer for instant hints, formulas, and syllabus summaries.

---

### PAGE 5: PAPER 2 — ESSAY & THEORY PRACTICE SCREEN (RICH TYPING & AI RUBRIC GRADING)
- Prompt Card: Official WAEC/NECO theory prompt displaying sub-sections and mark allocations (e.g., `(3 Marks)`).
- Rich Response Editor:
  - Minimum height 220px, Sand background (`#F3ECE0`), 1px border.
  - Toolbar: Bold, Italic, Subscript (`x₂`), Superscript (`x²`), and Formula/Chemical Reaction insertion helper (`➕ Add Symbol`).
  - Live word and character counter.
- Rubric-Based AI Coach Evaluation Container (Appears post-submission):
  - Overall score (e.g., `11/12 Marks`).
  - Sub-question point breakdown matched against official WAEC/NECO marking schemes.
  - "Coach Tip" box explaining exact phrasing needed to gain full examiner credit.

---

### PAGE 6: QUICK DRILL ("SINGLE SWAY") & QUEUE SCREEN
- Stack Card Layout: Swipe/sway or click "Add to Review Queue" (moves card into Review Later tray with a `200ms` sway motion) or "Answer Now" (expands choice options).
- Offline Sync Badge: Shows local PWA session storage status.

---

### PAGE 7: TIMED EXAM SIMULATION SCREEN (CBT MODE)
- Zero-Distraction Rule: High-contrast interface without background textile pattern overlays during simulation.
- Top Bar: Monospace countdown timer (`02:29:45`) with tabular numerals and embedded system calculator toggle button.
- Question Palette Drawer: Bottom/side grid showing Answered (Green), Unanswered (White), and Flagged (Marigold) questions.

---

### PAGE 8: SUBJECT PERFORMANCE & DIAGNOSTIC ANALYTICS DASHBOARD
- Mastery Heatmap: Color-coded topic health bars (Strong, Needs Review, Critical Gap).
- Paper 1 vs. Paper 2 Analytics: Comparison chart showing MCQ speed/accuracy vs. written theory mark retention.
- Past Script Attempt Viewer: Re-opens any past typed essay submission to review typed answers side-by-side with official WAEC/NECO marking schemes and AI coach feedback.
```

---

## 5. Module 4: JAMB / UTME Speed CBT Subsystem (Pages 1–5)

### Subsystem Overview
Unlike WAEC and NECO, **JAMB (UTME)** is a purely objective (MCQ) Computer-Based Test emphasizing extreme speed and time management. Candidates answer **180 questions across 4 subjects in 120 minutes** (~40s per question) with access to an on-screen system calculator. This module spans 5 dedicated pages.

### Master Build Prompt: JAMB Subsystem (Pages 1–5)

```markdown
# MASTER FRONT-END BUILD PROMPT: JAMB / UTME SPEED CBT MODULE (PAGES 1–5)

---

### PAGE 1: JAMB HUB LANDING & 4-SUBJECT COMBINATION BUILDER
- Preset Combination Selectors: 1-tap setup for popular tracks:
  - ⚙️ Engineering: Use of English + Mathematics + Physics + Chemistry
  - 🩺 Medicine / Pharmacy: Use of English + Biology + Chemistry + Physics
  - ⚖️ Law / Humanities: Use of English + Literature + Government + CRS/IRS
  - 💼 Commercial / Social Sciences: Use of English + Economics + Accounting + Commerce
- Custom Subject Switcher: Flexible dropdowns for custom 4-subject combinations.
- Question Bank Selector: 2015–2025 Verified JAMB Past Questions & PWA Offline Pack Downloader.

---

### PAGE 2: JAMB SESSION & CBT CONFIGURATOR
- Practice Mode Selection:
  - 🔘 Full 4-Subject UTME Mock: Complete 180 Questions / 120 Minutes simulation.
  - ⭕ Single-Subject Speed Drill: 40 Questions / 30 Minutes targeted drill.
  - ⭕ Instant Quiz Mode: Question-by-question scoring with AI Coach speed tips.
- Target Speed Indicator: Displays real-time pacing benchmark (e.g., "Target: 40 seconds / question").
- Custom Constraints: Slider controls for custom question volumes (10 to 180 Qs) and timer limits.

---

### PAGE 3: INTEGRATED 4-SUBJECT SPEED CBT SIMULATOR (CORE EXAM SCREEN)
- Top Navigation Bar:
  - Monospace Countdown Timer: `01:59:45` with tabular numerals.
  - 4-Subject Tab Switcher: Horizontal tabs (`[Use of English (42/60)] [Mathematics (18/40)] [Physics (0/40)] [Chemistry (0/40)]`) with active indicator animation (`150ms`).
  - On-Screen System Calculator Modal Trigger: Calculator icon button.
- Embedded System Calculator Modal:
  - Geometry: 240px width modal card, Sand fill (`#F3ECE0`), 1px border, 12px radius.
  - Display: Single-line digital display using monospace font.
  - Keypad: 4x4 button grid (Digits 0–9, +, -, ×, ÷, =, C, ±, .) with minimum 44px touch targets.
- Question Container: 18px / 28px Nunito Sans text card with 48px touch targets for options A–D.
- Question Palette Grid Drawer: 180-button overlay showing Answered (Leaf Green), Unanswered (Chalk White), and Flagged for Review (Exam Marigold).

---

### PAGE 4: JAMB INSTANT QUIZ & SPEED DRILL SCREEN (SINGLE-SUBJECT PRACTICE)
- Single-Subject Speed Layout: Rapid multiple-choice question card with real-time feedback.
- Correct State: Leaf Green (`#1B7F45`) border + "+1 Mark" badge.
- Incorrect State: Laterite Soil (`#C4532D`) border + "Not yet" coaching guidance.
- Sidekick Coach Drawer: Retractable drawer providing instant time-saving shortcuts, formula breakdowns, and rule summaries.

---

### PAGE 5: JAMB UTME SCORE & DIAGNOSTIC ANALYTICS DASHBOARD (400 MARKS)
- UTME 400-Point Score Report: Individual breakdown out of 100 per subject (e.g., English: 72, Physics: 68, Chemistry: 75, Math: 80 = Total: 295 / 400 Marks).
- Speed vs. Accuracy Matrix: Chart plotting time spent per question against accuracy to detect time-management bottlenecks.
- Diagnostic Gap Routing: Low-mastery topics are exported into the student's active Multi-Study Plan with 1 tap.
```

---

## 6. Module 5: Custom Exam Studio Subsystem (Pages 1–5)

### Subsystem Overview
The Custom Exam Studio enables students to upload personal lecture notes, slides, PDFs, or whiteboard photos, converting raw study materials into structured practice exams for subjects outside national syllabi. This module spans 5 dedicated pages.

### Master Build Prompt: Custom Exam Studio (Pages 1–5)

```markdown
# MASTER FRONT-END BUILD PROMPT: CUSTOM EXAM STUDIO (PAGES 1–5)

---

### PAGE 1: DOCUMENT UPLOAD DROPZONE & NOTE LIBRARY
- Multi-Format Drag & Drop Zone: Accepts PDF lecture slides, DOCX syllabus files, raw text pasting, and mobile photos of handwritten notes/whiteboards.
- Live Parsing Status: Animated processing state ("Processing PDF...", "Extracting key concepts...", "Ready for question generation").
- My Uploads Library: Grid of processed documents organized by custom subject folders (e.g., GST 101, ACC 201, CSC 301).

---

### PAGE 2: AI QUESTION GENERATOR & PARAMETER CONFIGURATOR
- Question Format Switcher: Multiple Choice (MCQ), Short Answer / Theory, or Mixed Format.
- Cognitive Depth Selector (Bloom's Taxonomy):
  - Recall & Definitions (Terminology & quick facts)
  - Conceptual Application (Scenario-based problem solving)
  - Advanced Problem Solving (Multi-step calculations & analysis)
- Grounded AI Constraint: Ensures generated answer keys cite exact page numbers and sections from the uploaded file ("coach, not ghostwriter" policy).

---

### PAGE 3: QUESTION BANK REVIEW & VERIFICATION STUDIO
- Inspection Grid: Side-by-side view of generated question prompts, distractor choices, answer keys, and source text quotes.
- Editorial Controls: Edit question phrasing, replace distractors, or regenerate individual items.
- Community Verification Queue: Submit custom question sets to peer review channels to earn a Verified Question Badge.

---

### PAGE 4: CUSTOM PRACTICE SESSION EXECUTION (MCQ & THEORY)
- Interactive Test Engine: Supports both Instant Quiz and Timed Exam modes for user materials.
- Rich Text Response Editor: Includes formula tools for theory questions.
- Sidekick AI Coach Integration: Provides hints grounded strictly in the uploaded document text.

---

### PAGE 5: CUSTOM MATERIAL ANALYTICS & CONCEPT MASTERY
- Document Concept Breakdown: Topic mastery bars for extracted document chapters/sections.
- Gap Export: Automatically routes low-mastery custom topics into the primary Multi-Study Plan.
```

---

## 7. Module 6: Technical Architecture, Motion Framework & PWA Standards

### Vector & Motion Framework (Zero Bitmap Images)
To ensure fast rendering, low mobile data consumption, and offline execution on budget Android devices, **no raster bitmap images (PNG/JPG)** are used. All graphics are rendered as lightweight inline SVGs and CSS keyframe animations:

```css
/* Lightweight CSS Motion Framework (150ms - 250ms gentle easing) */
@keyframes slidePill {
  from { transform: translateX(-4px); opacity: 0.8; }
  to { transform: translateX(0); opacity: 1; }
}

@keyframes pulseSync {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.08); opacity: 0.8; }
}

@keyframes swayCard {
  0% { transform: translateX(0) rotate(0deg); }
  50% { transform: translateX(12px) rotate(1.5deg); }
  100% { transform: translateX(0) rotate(0deg); }
}

@keyframes drawSuccessCheck {
  0% { stroke-dashoffset: 24; }
  100% { stroke-dashoffset: 0; }
}

/* Reduced Motion Override for Accessibility */
@media (prefers-reduced-motion: reduce) {
  *, ::before, ::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

### Accessibility & PWA Performance Standards
1. **Contrast & Touch Metrics**: All text meets WCAG AA standards (minimum **4.5:1 ratio**). Interactive choices and buttons adhere strictly to a **48px touch target height**.
2. **Offline-First PWA Sync**: Built with Workbox PWA service workers to cache downloadable question packs, allowing full offline practice during network drops or power outages.
3. **Empathetic Coaching Microcopy**: All feedback avoids punitive language ("Failed", "Wrong"). Mistakes trigger supportive guidance in Laterite Soil (`#C4532D` light / `#F08A63` dark).---
name: Warm Editorial Scholar
colors:
  surface: '#fdf9f2'
  surface-dim: '#dddad3'
  surface-bright: '#fdf9f2'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f7f3ec'
  surface-container: '#f1ede6'
  surface-container-high: '#ebe8e1'
  surface-container-highest: '#e6e2db'
  on-surface: '#1c1c18'
  on-surface-variant: '#474552'
  inverse-surface: '#31302c'
  inverse-on-surface: '#f4f0e9'
  outline: '#787584'
  outline-variant: '#c8c4d4'
  surface-tint: '#594fba'
  primary: '#230e84'
  on-primary: '#ffffff'
  primary-container: '#3a2e9a'
  on-primary-container: '#a9a2ff'
  inverse-primary: '#c5c0ff'
  secondary: '#805600'
  on-secondary: '#ffffff'
  secondary-container: '#fdb327'
  on-secondary-container: '#6b4800'
  tertiary: '#531400'
  on-tertiary: '#ffffff'
  tertiary-container: '#792100'
  on-tertiary-container: '#ff8d68'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#e4dfff'
  primary-fixed-dim: '#c5c0ff'
  on-primary-fixed: '#140067'
  on-primary-fixed-variant: '#4035a1'
  secondary-fixed: '#ffddaf'
  secondary-fixed-dim: '#ffba43'
  on-secondary-fixed: '#281800'
  on-secondary-fixed-variant: '#614000'
  tertiary-fixed: '#ffdbd0'
  tertiary-fixed-dim: '#ffb59e'
  on-tertiary-fixed: '#3a0b00'
  on-tertiary-fixed-variant: '#842501'
  background: '#fdf9f2'
  on-background: '#1c1c18'
  surface-variant: '#e6e2db'
typography:
  headline-xl:
    fontFamily: EB Garamond
    fontSize: 40px
    fontWeight: '600'
    lineHeight: 48px
  headline-xl-mobile:
    fontFamily: EB Garamond
    fontSize: 30px
    fontWeight: '600'
    lineHeight: 38px
  headline-lg:
    fontFamily: EB Garamond
    fontSize: 32px
    fontWeight: '600'
    lineHeight: 40px
  headline-lg-mobile:
    fontFamily: EB Garamond
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  headline-md:
    fontFamily: EB Garamond
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  headline-sm:
    fontFamily: EB Garamond
    fontSize: 20px
    fontWeight: '600'
    lineHeight: 28px
  body-lg:
    fontFamily: Nunito Sans
    fontSize: 18px
    fontWeight: '400'
    lineHeight: 28px
  body-md:
    fontFamily: Nunito Sans
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-sm:
    fontFamily: Nunito Sans
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  label-lg:
    fontFamily: Nunito Sans
    fontSize: 15px
    fontWeight: '700'
    lineHeight: 20px
    letterSpacing: 0.01em
  label-md:
    fontFamily: Nunito Sans
    fontSize: 13px
    fontWeight: '600'
    lineHeight: 18px
    letterSpacing: 0.02em
  label-sm:
    fontFamily: Nunito Sans
    fontSize: 11px
    fontWeight: '700'
    lineHeight: 16px
    letterSpacing: 0.04em
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  gutter: 1rem
  gutter-tablet: 1.5rem
  gutter-desktop: 2rem
  margin: 1rem
  margin-tablet: 2rem
  margin-desktop: 3rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 1rem
  space-lg: 1.5rem
  space-xl: 2.25rem
---

## Brand & Style

This design system serves secondary school finalists preparing for rigorous national exams (WAEC, JAMB/UTME, NECO). It moves away from cold, stress-inducing testing software into an encouraging, scholarly, and culturally rooted learning companion.

The aesthetic fuses tactile, warm editorial study materials with modern digital precision:
- **Paper-First Materiality:** Surfaces emulate warm chalk paper, fine exercise books, and archival stationery rather than harsh digital screens.
- **Cultural Grounding:** Visual highlights derive from Yoruba Adire textile geometry (measured chevron, diamond, and crosshatching accents) subtly applied to badges, empty states, and section borders.
- **Calm Mastery:** Color choices relieve eye strain during late-night study drills while delivering sharp visual hierarchy for formulas, past questions, and explanatory walkthroughs.

## Colors

The palette establishes an organic academic environment with clear semantic contrast:

- **Primary (`#3A2E9A` Adire Indigo):** Anchors core actions, active navigation, brand elements, and high-priority progress stats.
- **Primary Tint (`#ECE9FB` Soft Adire):** Supplies background fills for active interactive states, selected answer containers, and focus tags.
- **Secondary Accent (`#F2A91B` Marigold):** Denotes test streaks, timers, review flags, and motivational achievements.
- **Tertiary Accent (`#C4532D` Laterite Soil):** Signals critical alerts, incorrect options in review mode, and urgent time thresholds.
- **Success (`#1B7F45` Leaf Green):** Reserved strictly for correct question outcomes, verified answers, and syllabus completion markers.
- **Background & Surfaces:**
  - Canvas Base: `#FBF7F0` (Chalk Paper)
  - Card/Module Surface: `#FFFFFF` (Pure White)
  - Secondary/Inset Surface: `#F3ECE0` (Warm Sand)
  - Structural Borders: `#E3DACB` (Organic Parchment Border)
- **Typography & Ink:**
  - Main Text: `#1E1B2E` (Deep Indigo-Black for high legibility without pitch-black harshness)
  - Muted Text: `#5B5670` (Secondary metadata, year labels, and explanations)

## Typography

The type system balances warm scholarly presence with rapid-scan digital performance.

- **Headings (EB Garamond):** Used for test module headers, exam names (JAMB Chemistry, WAEC English Literature), and major milestones. Brings the dignity and permanence of classic textbooks.
- **Body & Controls (Nunito Sans):** Soft, rounded grotesque providing superior readability for long reading passages, comprehension questions, mathematical notations, and touch-screen answer selection.
- **Stem & Question Styling:** Examination stems use `body-lg` at 18px with deliberate line-height (28px) to eliminate line-jumping errors during timed drills.

## Layout & Spacing

A 12-column fluid grid accommodates diverse device scenarios: from entry-level Android smartphones with narrow screens to large classroom desktops and tablets.

- **Canvas Breakpoints:**
  - **Mobile (<768px):** 4-column layout, 16px margins, compact gutters. Bottom sheet action trays for question controls and rapid option taps.
  - **Tablet (768px - 1024px):** 8-column layout, split-pane view (left: reading passage or question list; right: active question and scratchpad).
  - **Desktop (>1024px):** 12-column layout with a constrained maximum width of 1240px to preserve comfortable optical line lengths for academic passages.
- **Exam Mode Constraints:** Mock test layouts enforce single-focus workspaces; secondary sidebars collapse into a warm sand drawer to preserve executive attention.

## Elevation & Depth

This design system avoids harsh artificial drop shadows, relying instead on warm physical stationery layering:

- **Level 0 (Parchment Foundation):** Background base (`#FBF7F0`) rendered flat with subtle, warm ambient tone.
- **Level 1 (Paper Cards & Question Tiles):** `#FFFFFF` surfaces nested over `#FBF7F0`, bounded by a single structural line in `#E3DACB` (1px solid). An ultra-diffuse warm shadow adds physical presence: `0 2px 6px -1px rgba(58, 46, 154, 0.04), 0 1px 3px -1px rgba(30, 27, 46, 0.03)`.
- **Level 2 (Active Modals, Timer Bars, Flyouts):** Lifted cards framed by `#E3DACB` with increased ambient depth: `0 8px 24px -4px rgba(58, 46, 154, 0.08), 0 4px 10px -2px rgba(30, 27, 46, 0.04)`.
- **Adire Micro-Depth:** Important section dividers, score headers, and exam completion ribbons feature a 3px micro-stripe border-bottom showing an alternating geometric indigo/marigold pattern.

## Shapes

The interface embraces organic, comfortable roundness (`level 2`) to counteract test anxiety:

- Standard buttons, option selection blocks, and input fields use `0.5rem` (8px).
- Content cards, diagnostic review sections, and modal sheets carry `1rem` (16px) corners.
- Badges, status markers (e.g., "JAMB 2022 Past Question"), and key score counters utilize full pill radiuses (`9999px`).

## Components

### Buttons
- **Primary Action (e.g., "Submit Answer", "Start CBT Drill"):** Deep Adire Indigo (`#3A2E9A`) fill, pure white text, 8px radius. Hover: `#2D237A`. Active: slight 1px scale depression.
- **Secondary/Review Action (e.g., "Flag for Later", "Explain Step"):** Chalk paper background with Sand fill (`#F3ECE0`), border `1px solid #E3DACB`, text `#1E1B2E`.
- **Accent Action (e.g., "Review Streak", "JAMB Score Booster"):** Marigold fill (`#F2A91B`), text `#1E1B2E` font-weight 700.

### Question Option Cards (MCQ / CBT Choices)
- Default: White surface (`#FFFFFF`), `1px solid #E3DACB`, typography `Nunito Sans` 16px.
- Hover: Border switches to `#3A2E9A`, background becomes `#FBF7F0`.
- Selected: Soft Adire Tint (`#ECE9FB`), border `2px solid #3A2E9A`, option letters (A, B, C, D) contained in a solid indigo circular pill with white lettering.
- Correct Review State: Leaf Green tint background (`#E8F5EE`), border `2px solid #1B7F45`.
- Incorrect Review State: Laterite Soil tint background (`#FAEEEA`), border `2px solid #C4532D`.

### Checkboxes & Radio Selectors
- Circular radiomarks featuring a custom 3px interior gap when checked in `#3A2E9A`. High-contrast check indicator on `#1B7F45` for multi-select syllabus checklists.

### Input Fields
- Background `#FFFFFF`, border `1px solid #E3DACB`. Focus state rings the input in a 2px outer aura of `#ECE9FB` with an immediate stroke of `#3A2E9A`. Placeholder in `#5B5670`.

### Cards & Study Trackers
- Subject and topic cards utilize `#FFFFFF` base layers with an inset top strip in `#F3ECE0`. Topic progress bars use `#3A2E9A` track with `#F2A91B` milestone pips.

### Exam-Specific Specialized Components
- **CBT Floating Timer Bar:** Sand background (`#F3ECE0`), bordered by `#E3DACB`, displaying digital time with a Laterite Soil (`#C4532D`) flashing badge when under 5 minutes.
- **Adire Accent Ribbon:** Used across test summary headers, a thin 4px geometric band alternating Indigo triangles and Marigold dots that honors regional craft without compromising UI clarity.
)[Uploading DE---     [DESIGN (2).md](https://github.com/user-attachments/files/33730105/DESIGN.2.md)

name: Warm Editorial Scholar
colors:
  surface: '#fdf9f2'
  surface-dim: '#dddad3'
  surface-bright: '#fdf9f2'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f7f3ec'
  surface-container: '#f1ede6'
  surface-container-high: '#ebe8e1'
  surface-container-highest: '#e6e2db'
  on-surface: '#1c1c18'
  on-surface-variant: '#474552'
  inverse-surface: '#31302c'
  inverse-on-surface: '#f4f0e9'
  outline: '#787584'
  outline-variant: '#c8c4d4'
  surface-tint: '#594fba'
  primary: '#230e84'
  on-primary: '#ffffff'
  primary-container: '#3a2e9a'
  on-primary-container: '#a9a2ff'
  inverse-primary: '#c5c0ff'
  secondary: '#805600'
  on-secondary: '#ffffff'
  secondary-container: '#fdb327'
  on-secondary-container: '#6b4800'
  tertiary: '#531400'
  on-tertiary: '#ffffff'
  tertiary-container: '#792100'
  on-tertiary-container: '#ff8d68'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#e4dfff'
  primary-fixed-dim: '#c5c0ff'
  on-primary-fixed: '#140067'
  on-primary-fixed-variant: '#4035a1'
  secondary-fixed: '#ffddaf'
  secondary-fixed-dim: '#ffba43'
  on-secondary-fixed: '#281800'
  on-secondary-fixed-variant: '#614000'
  tertiary-fixed: '#ffdbd0'
  tertiary-fixed-dim: '#ffb59e'
  on-tertiary-fixed: '#3a0b00'
  on-tertiary-fixed-variant: '#842501'
  background: '#fdf9f2'
  on-background: '#1c1c18'
  surface-variant: '#e6e2db'
typography:
  headline-xl:
    fontFamily: EB Garamond
    fontSize: 40px
    fontWeight: '600'
    lineHeight: 48px
  headline-xl-mobile:
    fontFamily: EB Garamond
    fontSize: 30px
    fontWeight: '600'
    lineHeight: 38px
  headline-lg:
    fontFamily: EB Garamond
    fontSize: 32px
    fontWeight: '600'
    lineHeight: 40px
  headline-lg-mobile:
    fontFamily: EB Garamond
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  headline-md:
    fontFamily: EB Garamond
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  headline-sm:
    fontFamily: EB Garamond
    fontSize: 20px
    fontWeight: '600'
    lineHeight: 28px
  body-lg:
    fontFamily: Nunito Sans
    fontSize: 18px
    fontWeight: '400'
    lineHeight: 28px
  body-md:
    fontFamily: Nunito Sans
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-sm:
    fontFamily: Nunito Sans
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  label-lg:
    fontFamily: Nunito Sans
    fontSize: 15px
    fontWeight: '700'
    lineHeight: 20px
    letterSpacing: 0.01em
  label-md:
    fontFamily: Nunito Sans
    fontSize: 13px
    fontWeight: '600'
    lineHeight: 18px
    letterSpacing: 0.02em
  label-sm:
    fontFamily: Nunito Sans
    fontSize: 11px
    fontWeight: '700'
    lineHeight: 16px
    letterSpacing: 0.04em
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  gutter: 1rem
  gutter-tablet: 1.5rem
  gutter-desktop: 2rem
  margin: 1rem
  margin-tablet: 2rem
  margin-desktop: 3rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 1rem
  space-lg: 1.5rem
  space-xl: 2.25rem
---

## Brand & Style

This design system serves secondary school finalists preparing for rigorous national exams (WAEC, JAMB/UTME, NECO). It moves away from cold, stress-inducing testing software into an encouraging, scholarly, and culturally rooted learning companion.

The aesthetic fuses tactile, warm editorial study materials with modern digital precision:
- **Paper-First Materiality:** Surfaces emulate warm chalk paper, fine exercise books, and archival stationery rather than harsh digital screens.
- **Cultural Grounding:** Visual highlights derive from Yoruba Adire textile geometry (measured chevron, diamond, and crosshatching accents) subtly applied to badges, empty states, and section borders.
- **Calm Mastery:** Color choices relieve eye strain during late-night study drills while delivering sharp visual hierarchy for formulas, past questions, and explanatory walkthroughs.

## Colors

The palette establishes an organic academic environment with clear semantic contrast:

- **Primary (`#3A2E9A` Adire Indigo):** Anchors core actions, active navigation, brand elements, and high-priority progress stats.
- **Primary Tint (`#ECE9FB` Soft Adire):** Supplies background fills for active interactive states, selected answer containers, and focus tags.
- **Secondary Accent (`#F2A91B` Marigold):** Denotes test streaks, timers, review flags, and motivational achievements.
- **Tertiary Accent (`#C4532D` Laterite Soil):** Signals critical alerts, incorrect options in review mode, and urgent time thresholds.
- **Success (`#1B7F45` Leaf Green):** Reserved strictly for correct question outcomes, verified answers, and syllabus completion markers.
- **Background & Surfaces:**
  - Canvas Base: `#FBF7F0` (Chalk Paper)
  - Card/Module Surface: `#FFFFFF` (Pure White)
  - Secondary/Inset Surface: `#F3ECE0` (Warm Sand)
  - Structural Borders: `#E3DACB` (Organic Parchment Border)
- **Typography & Ink:**
  - Main Text: `#1E1B2E` (Deep Indigo-Black for high legibility without pitch-black harshness)
  - Muted Text: `#5B5670` (Secondary metadata, year labels, and explanations)

## Typography

The type system balances warm scholarly presence with rapid-scan digital performance.

- **Headings (EB Garamond):** Used for test module headers, exam names (JAMB Chemistry, WAEC English Literature), and major milestones. Brings the dignity and permanence of classic textbooks.
- **Body & Controls (Nunito Sans):** Soft, rounded grotesque providing superior readability for long reading passages, comprehension questions, mathematical notations, and touch-screen answer selection.
- **Stem & Question Styling:** Examination stems use `body-lg` at 18px with deliberate line-height (28px) to eliminate line-jumping errors during timed drills.

## Layout & Spacing

A 12-column fluid grid accommodates diverse device scenarios: from entry-level Android smartphones with narrow screens to large classroom desktops and tablets.

- **Canvas Breakpoints:**
  - **Mobile (<768px):** 4-column layout, 16px margins, compact gutters. Bottom sheet action trays for question controls and rapid option taps.
  - **Tablet (768px - 1024px):** 8-column layout, split-pane view (left: reading passage or question list; right: active question and scratchpad).
  - **Desktop (>1024px):** 12-column layout with a constrained maximum width of 1240px to preserve comfortable optical line lengths for academic passages.
- **Exam Mode Constraints:** Mock test layouts enforce single-focus workspaces; secondary sidebars collapse into a warm sand drawer to preserve executive attention.

## Elevation & Depth

This design system avoids harsh artificial drop shadows, relying instead on warm physical stationery layering:

- **Level 0 (Parchment Foundation):** Background base (`#FBF7F0`) rendered flat with subtle, warm ambient tone.
- **Level 1 (Paper Cards & Question Tiles):** `#FFFFFF` surfaces nested over `#FBF7F0`, bounded by a single structural line in `#E3DACB` (1px solid). An ultra-diffuse warm shadow adds physical presence: `0 2px 6px -1px rgba(58, 46, 154, 0.04), 0 1px 3px -1px rgba(30, 27, 46, 0.03)`.
- **Level 2 (Active Modals, Timer Bars, Flyouts):** Lifted cards framed by `#E3DACB` with increased ambient depth: `0 8px 24px -4px rgba(58, 46, 154, 0.08), 0 4px 10px -2px rgba(30, 27, 46, 0.04)`.
- **Adire Micro-Depth:** Important section dividers, score headers, and exam completion ribbons feature a 3px micro-stripe border-bottom showing an alternating geometric indigo/marigold pattern.

## Shapes

The interface embraces organic, comfortable roundness (`level 2`) to counteract test anxiety:

- Standard buttons, option selection blocks, and input fields use `0.5rem` (8px).
- Content cards, diagnostic review sections, and modal sheets carry `1rem` (16px) corners.
- Badges, status markers (e.g., "JAMB 2022 Past Question"), and key score counters utilize full pill radiuses (`9999px`).

## Components

### Buttons
- **Primary Action (e.g., "Submit Answer", "Start CBT Drill"):** Deep Adire Indigo (`#3A2E9A`) fill, pure white text, 8px radius. Hover: `#2D237A`. Active: slight 1px scale depression.
- **Secondary/Review Action (e.g., "Flag for Later", "Explain Step"):** Chalk paper background with Sand fill (`#F3ECE0`), border `1px solid #E3DACB`, text `#1E1B2E`.
- **Accent Action (e.g., "Review Streak", "JAMB Score Booster"):** Marigold fill (`#F2A91B`), text `#1E1B2E` font-weight 700.

### Question Option Cards (MCQ / CBT Choices)
- Default: White surface (`#FFFFFF`), `1px solid #E3DACB`, typography `Nunito Sans` 16px.
- Hover: Border switches to `#3A2E9A`, background becomes `#FBF7F0`.
- Selected: Soft Adire Tint (`#ECE9FB`), border `2px solid #3A2E9A`, option letters (A, B, C, D) contained in a solid indigo circular pill with white lettering.
- Correct Review State: Leaf Green tint background (`#E8F5EE`), border `2px solid #1B7F45`.
- Incorrect Review State: Laterite Soil tint background (`#FAEEEA`), border `2px solid #C4532D`.

### Checkboxes & Radio Selectors
- Circular radiomarks featuring a custom 3px interior gap when checked in `#3A2E9A`. High-contrast check indicator on `#1B7F45` for multi-select syllabus checklists.

### Input Fields
- Background `#FFFFFF`, border `1px solid #E3DACB`. Focus state rings the input in a 2px outer aura of `#ECE9FB` with an immediate stroke of `#3A2E9A`. Placeholder in `#5B5670`.

### Cards & Study Trackers
- Subject and topic cards utilize `#FFFFFF` base layers with an inset top strip in `#F3ECE0`. Topic progress bars use `#3A2E9A` track with `#F2A91B` milestone pips.

### Exam-Specific Specialized Components
- **CBT Floating Timer Bar:** Sand background (`#F3ECE0`), bordered by `#E3DACB`, displaying digital time with a Laterite Soil (`#C4532D`) flashing badge when under 5 minutes.
- **Adire Accent Ribbon:** Used across test summary headers, a thin 4px geometric band alternating Indigo triangles and Marigold dots that honors regional craft without compromising UI clarity.SIGN (2).md…]()

[DESIGN (2).md](https://github.com/user-attachments/files/33730125/DESIGN.2.md)
[design-v5.md](https://github.com/user-attachments/files/33730129/design-v5.md)# African Intelligence — Platform UI/UX Design System & Master Prompts

## Executive Overview
This document compiles the complete UI/UX specifications, visual identity design tokens, interaction flows, and developer-ready front-end prompts for **African Intelligence**. 

Designed specifically for Nigerian students preparing for national examinations (**WAEC SSCE/BECE**, **NECO SSCE/BECE**, **JAMB/UTME**, and **Custom Academic Tracks**), the platform acts as a trusted **academic coach rather than a shortcut ghostwriter**. The design system prioritizes a warm, paper-inspired aesthetic, cultural resonance through traditional Adire textile patterns, and technical optimizations for low-data usage and battery conservation on budget Android devices.

---

## Table of Contents
1. [Global Visual Identity & Token Architecture](#1-global-visual-identity--token-architecture)
2. [Module 1: Onboarding & Sign-Up Flow (Streamlined 60-Second Setup)](#2-module-1-onboarding--sign-up-flow)
3. [Module 2: Goal-Led Dashboard (Progress Home)](#3-module-2-goal-led-dashboard-progress-home)
4. [Module 3: WAEC & NECO Dual-Mode Subsystem (Pages 1–8)](#4-module-3-waec--neco-dual-mode-subsystem-pages-18)
5. [Module 4: JAMB / UTME Speed CBT Subsystem (Pages 1–5)](#5-module-4-jamb--utme-speed-cbt-subsystem-pages-15)
6. [Module 5: Custom Exam Studio Subsystem (Pages 1–5)](#6-module-5-custom-exam-studio-subsystem-pages-15)
7. [Module 6: Multi-Study Plan Manager (Single-Page Interactive View)](#7-module-6-multi-study-plan-manager-single-page-interactive-view)
8. [Module 7: Full Syllabus Diagnostic Heatmap Page](#8-module-7-full-syllabus-diagnostic-heatmap-page)
9. [Module 8: Technical Architecture, Motion Framework & PWA Standards](#9-module-8-technical-architecture-motion-framework--pwa-standards)
10. [Module 9: Sidekick AI Coach, Community Workspace & In-Thread Tagging](#10-module-9-sidekick-ai-coach-community-workspace--in-thread-tagging)

---

## 1. Global Visual Identity & Token Architecture

Grounded in the **African Intelligence Visual Identity Guide**, the interface avoids generic corporate blues and cold technology greys in favor of warm paper-like neutrals, indigo dye traditions (Adire), red-earth Laterite soil, Marigold, and Leaf green.

```css
:root {
  /* Surface & Background Neutrals */
  --bg: #FBF7F0;          /* Chalk paper neutral background */
  --surface: #FFFFFF;     /* Clean white card surface */
  --surface-2: #F3ECE0;   /* Sand raised surface & input field fill */
  --border: #E3DACB;      /* Soft card outline & divider line */
  --text: #1E1B2E;        /* Primary high-contrast text */
  --text-muted: #5B5670;  /* Secondary caption & label text */

  /* Brand & Module Specific Tokens */
  --primary: #3A2E9A;      /* Adire Indigo (primary CTAs & links) */
  --on-primary: #FFFFFF;   /* Text on primary active state */
  --primary-tint: #ECE9FB; /* Soft Adire highlight fill */
  --exam-accent: #B97700;  /* Exam Marigold (headers & progress rings) */
  --highlight: #F2A91B;    /* Warm Marigold milestone accent */

  /* Feedback & State Indicators */
  --success: #1B7F45;     /* Leaf Green (correct answer, verified item) */
  --try-again: #C4532D;   /* Laterite Soil (incorrect answer / "not yet" coaching) */
  --error: #C0263F;       /* Reserved strictly for system/payment failures */

  /* Element Geometry */
  --radius-card: 12px;    /* Card corner radius */
  --radius-btn: 10px;     /* Button corner radius */
  --radius-chip: 999px;   /* Fully rounded pill radius */

  /* Typography Families */
  --font-head: "Fraunces", Georgia, serif;                        /* Soft academic serif */
  --font-body: "Nunito Sans", system-ui, -apple-system, sans-serif;/* Readable open sans-serif */
  --font-mono: ui-monospace, SFMono-Regular, "Courier New", monospace; /* Tabular numerals */
}

/* Dark Mode Theme Mapping (Soft Night Ink Sheets) */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --bg: #14122B;          /* Night Ink background */
    --surface: #1D1A3A;     /* Deep Indigo sheet */
    --surface-2: #272349;   /* Raised indigo surface */
    --border: #38335E;      /* Dark border outline */
    --text: #F1EDE4;        /* Soft paper white text */
    --text-muted: #B3AEC6;  /* Muted caption text */
    --primary: #A79BFF;      /* Indigo Glow */
    --on-primary: #14122B;  /* Dark text on glowing button */
    --primary-tint: #2C2663; /* Soft indigo selected fill */
    --exam-accent: #F6B93B;  /* Soft Exam Marigold */
    --success: #5FD08C;     /* Soft Leaf Green */
    --try-again: #F08A63;   /* Soft Laterite */
  }
}

/* Manual Battery Saver Mode Override */
:root[data-theme="battery"] {
  --bg: #0B0A18; /* True Dark OLED black for power conservation */
}
```

### Typography & Formatting Rules
* **Headings**: Fraunces (SemiBold 600 / Bold 700) for academic warmth.
* **Body & Options**: Nunito Sans (Regular 400 / SemiBold 600).
* **Exam Question Body**: Set to **18px font size with 28px line-height** (Nunito Sans 400) for maximum legibility under timed examination pressure.
* **Timers, Scores & Currency**: System Monospace font with **tabular numerals** so countdown digits do not jump during execution. Native rendering support for the **₦ (Naira)** glyph (`₦ 2,500`).
* **Ergonomic Touch Targets**: Minimum **48px height** for all primary buttons, choice options, and social auth triggers; minimum **44px** for secondary pills and skip links.

---

## 2. Module 1: Onboarding & Sign-Up Flow

### Overview
A low-friction, progressive onboarding process designed to complete in **under 60 seconds**. It gathers the user's preferred name and primary target exam, while keeping secondary details (department, exam date) optional and skippable.

### Master Prompt: Onboarding Screens
```markdown
# UI/UX & FRONT-END BUILD PROMPT: STREAMLINED ONBOARDING FLOW

## SCREEN 1: LIGHT SIGN-UP & PREFERRED NAME
- Header: Brand Logo with Marigold (`#F2A91B`) spark icon. Headline (Fraunces 25px): "Welcome to Your Graduation Companion".
- Input 1: Preferred Name field ("What should your AI Coach call you?").
- Primary Auth Stack (48px Buttons, 10px Radius):
  - "Continue with Google"
  - "Continue with WhatsApp / Phone"
  - "Continue with Apple / Email"
- Microcopy: "By continuing, your progress and uploaded materials are protected under NDPA standards."

## SCREEN 2: EXAM TARGET SETUP & PRACTICE PLAN
- Step Indicator: Top bar in Marigold (`#F2A91B`) indicating "Step 2 of 2".
- Headline (Fraunces 25px): "Set Your Exam Target". Sub-headline: "Select your primary exam focus. You can change or add targets anytime in your dashboard."
- Question 1 (MANDATORY - 2x3 Grid View Layout):
  1. 🎓 WAEC / SSCE: West African Senior School Certificate Examination.
  2. ⚡ JAMB / UTME: Joint Admissions and Matriculation Board CBT.
  3. 📚 NECO / BECE: National Examinations Council past questions & syllabus.
  4. 🏫 Junior SSCE / BECE: Junior secondary transition exam prep (Junior WAEC/NECO).
  5. 🧪 Custom Subject Space: Upload your own lecture notes, PDF, or syllabus.
  6. 🌐 Wide Scope Prep: Simultaneous multi-exam preparation.
- Question 2: Department / Field of Study (OPTIONAL)
  - Horizontal scroll pills: `🔬 Science` | `💼 Commercial` | `🎨 Arts` | `🛠️ Technical`
  - Right-aligned text button: "Skip for now" (44px touch target).
- Question 3: Target Exam Date (OPTIONAL)
  - Dropdown selector (e.g., "April 2027", "May 2027", "Self-Paced").
  - Right-aligned text button: "Skip for now" (44px touch target).
- Primary CTA Button (48px height, `--primary` background): "Complete Setup & Go to Dashboard".

## AESTHETIC & PATTERN STYLING
- Background: Chalk neutral (`#FBF7F0`) with faint repeating geometric Adire textile SVG pattern (4% to 6% opacity).
- Card Elevation: Surface white (`#FFFFFF`) cards with 1px soft border (`#E3DACB`) and soft ambient shadows.
```

---

## 3. Module 2: Goal-Led Dashboard (Progress Home)

### Overview
A goal-driven home screen that serves as the student's central command center. It features a **Graduation-Readiness Ring**, an active study plan switcher, exam track hubs, practice analytics, and persistent access to the **Sidekick AI Coach**.

### Master Prompt: Dashboard
```markdown
# DESIGN PROMPT: GOAL-LED DASHBOARD (PROGRESS HOME)

## OVERVIEW & GOAL
Create a warm, encouraging home dashboard for "African Intelligence". The page acts as a personal command center answering: "How ready am I to graduate and pass my exams?"

## KEY SECTIONS (TOP TO BOTTOM)

1. TOP BAR & WELCOME:
   - Greeting: "Welcome back, Temi!" and department tag ("Science Track").
   - Controls: Battery Saver Mode toggle (`#0B0A18`) and Data Saver status indicator.

2. STUDY PLAN SWITCHER BANNER:
   - Active Plan Card: "Active Plan: JAMB 2027 Engineering (Week 4 of 12)".
   - Today's Task: "Today's Focus: Physics - Optics & Waves (45 mins left)".
   - Actions: "Resume Today's Study" (Primary Indigo) & "Switch Study Plan" dropdown.

3. GRADUATION-READINESS WHEEL:
   - Multi-segment progress ring ("68% Ready to Graduate") showing stepping stones ending in a graduation cap icon.

4. EXAM SYSTEM SCOPE (2x2 GRID):
   - 📚 WAEC / SSCE Hub (Senior & Junior BECE)
   - ⚡ JAMB / UTME Hub (Speed CBT Simulator)
   - 📝 NECO / BECE Hub (National Syllabus)
   - 🧪 Custom Exam Studio (Upload lecture notes/PDFs)

5. PRACTICE ANALYTICS & RECENT ACTIVITIES:
   - "Recent Drill: Physics Waves – Score 8/10 (80%)"
   - "Weak Topic Flagged: Optics – Added to today's review"
   - "Uploaded File: Organic_Chemistry_Notes.pdf (Processed)"
   - Action: "View Full Analytics" link.

6. AI TUTOR & COMMUNITY QUICK-ACCESS BAR:
   - 💬 "Chat with Sidekick Coach" (1-tap AI assistance).
   - 👥 "Join Department Study Group" (Peer discussion channels).
```

---

## 4. Module 3: WAEC & NECO Dual-Mode Subsystem (Pages 1–8)

### Subsystem Overview
WAEC and NECO are two distinct national examination bodies that share a dual-paper structure: **Paper 1 (Objective MCQ)** for speed and retrieval, and **Paper 2 (Essay / Theory)** for structured written answers. This module covers both **Senior Secondary (WAEC/NECO SSCE)** and **Junior Secondary (Junior WAEC/NECO BECE)** levels across 8 dedicated pages.

### Master Build Prompt: WAEC & NECO Subsystem (Pages 1–8)

```markdown
# MASTER FRONT-END BUILD PROMPT: WAEC & NECO DUAL-MODE EXAM MODULE (PAGES 1–8)
# TARGET PLATFORM: AFRICAN INTELLIGENCE PWA (PROGRESSIVE WEB APP)

---

### PAGE 1: WAEC & NECO HUB LANDING & SUBJECT SELECTOR
- Level Switcher Pills: `Senior WAEC SSCE` | `Senior NECO SSCE` | `Junior WAEC / BECE` | `Junior NECO BECE`.
- Offline Pack Status Banner: Download button with tray icon to cache 500+ past questions locally via PWA Workbox background sync.
- Subject Grid: 9 Departmental subjects (Senior Science, Commercial, Arts) or Junior foundational pillars (Basic STEM, Business Studies, Humanities). Shows question count and topic mastery percentage per subject card.
- Interaction Motion: Tapping a card elevates it with a 2px Adire Indigo stroke, primary tint background fill (`#ECE9FB`), `1.02x` micro-scale transform, and an animated Leaf Green checkmark SVG draw.

---

### PAGE 2: PRACTICE SESSION CONFIGURATOR
- Mode Selector Cards:
  1. 🔘 Instant Quiz Mode: Real-time feedback and step-by-step AI Coach breakdown per question.
  2. ⭕ Quick Drill ("Single Sway"): Rapid question sweeping; queue hard items into a "Review Later" tray.
  3. ⭕ Timed Exam Simulator: Official time limits; deferred scoring until submission.
- Parameter Controls:
  - Question Volume: Admin default vs. Custom Slider (5 to 50 Qs).
  - Timer Rules: Official Exam Timer vs. Custom Minutes vs. Untimed Relaxed Mode.
  - Content Focus: Verified Questions (2015–2025) vs. Critical Gaps Only.

---

### PAGE 3: DIAGNOSTIC GAP ANALYSIS TEST PAGE
- Assessment: 10 targeted adaptive diagnostic questions.
- Display: 18px Nunito Sans question text with inline SVG vector diagrams (2px stroke, zero bitmap images).
- Output: Post-test Diagnostic Gap Summary displaying topic mastery bars (e.g., Mechanics: 100%, Optics: 33% Critical Gap). Weak topics are auto-routed to the user's active Study Plan.

---

### PAGE 4: PAPER 1 — OBJECTIVE (MCQ) PRACTICE SCREEN
- Top Bar: Subject title, question counter ("Question 8 of 50"), Monospace timer (`42:15`), and "Verified Question" shield badge.
- Question Container: 18px / 28px Nunito Sans text card (`#FFFFFF`).
- Choice Buttons (A, B, C, D): Minimum 48px height.
  - Correct Selection: `--success` Leaf Green border (`#1B7F45`), checkmark SVG draw animation, and "+1 Mark" badge.
  - Incorrect Selection: `--try-again` Laterite Soil border (`#C4532D`), circular arrow icon, and encouraging microcopy ("Not yet. Let's look at this concept together."). NEVER use punitive red screens.
- Sidekick Coach Drawer: Retractable drawer for instant hints, formulas, and syllabus summaries.

---

### PAGE 5: PAPER 2 — ESSAY & THEORY PRACTICE SCREEN (RICH TYPING & AI RUBRIC GRADING)
- Prompt Card: Official WAEC/NECO theory prompt displaying sub-sections and mark allocations (e.g., `(3 Marks)`).
- Rich Response Editor:
  - Minimum height 220px, Sand background (`#F3ECE0`), 1px border.
  - Toolbar: Bold, Italic, Subscript (`x₂`), Superscript (`x²`), and Formula/Chemical Reaction insertion helper (`➕ Add Symbol`).
  - Live word and character counter.
- Rubric-Based AI Coach Evaluation Container (Appears post-submission):
  - Overall score (e.g., `11/12 Marks`).
  - Sub-question point breakdown matched against official WAEC/NECO marking schemes.
  - "Coach Tip" box explaining exact phrasing needed to gain full examiner credit.

---

### PAGE 6: QUICK DRILL ("SINGLE SWAY") & QUEUE SCREEN
- Stack Card Layout: Swipe/sway or click "Add to Review Queue" (moves card into Review Later tray with a `200ms` sway motion) or "Answer Now" (expands choice options).
- Offline Sync Badge: Shows local PWA session storage status.

---

### PAGE 7: TIMED EXAM SIMULATION SCREEN (CBT MODE)
- Zero-Distraction Rule: High-contrast interface without background textile pattern overlays during simulation.
- Top Bar: Monospace countdown timer (`02:29:45`) with tabular numerals and embedded system calculator toggle button.
- Question Palette Drawer: Bottom/side grid showing Answered (Green), Unanswered (White), and Flagged (Marigold) questions.

---

### PAGE 8: SUBJECT PERFORMANCE & DIAGNOSTIC ANALYTICS DASHBOARD
- Mastery Heatmap: Color-coded topic health bars (Strong, Needs Review, Critical Gap).
- Paper 1 vs. Paper 2 Analytics: Comparison chart showing MCQ speed/accuracy vs. written theory mark retention.
- Past Script Attempt Viewer: Re-opens any past typed essay submission to review typed answers side-by-side with official WAEC/NECO marking schemes and AI coach feedback.
```

---

## 5. Module 4: JAMB / UTME Speed CBT Subsystem (Pages 1–5)

### Subsystem Overview
Unlike WAEC and NECO, **JAMB (UTME)** is a purely objective (MCQ) Computer-Based Test emphasizing extreme speed and time management. Candidates answer **180 questions across 4 subjects in 120 minutes** (~40s per question) with access to an on-screen system calculator. This module spans 5 dedicated pages.

### Master Build Prompt: JAMB Subsystem (Pages 1–5)

```markdown
# MASTER FRONT-END BUILD PROMPT: JAMB / UTME SPEED CBT MODULE (PAGES 1–5)

---

### PAGE 1: JAMB HUB LANDING & 4-SUBJECT COMBINATION BUILDER
- Preset Combination Selectors: 1-tap setup for popular tracks:
  - ⚙️ Engineering: Use of English + Mathematics + Physics + Chemistry
  - 🩺 Medicine / Pharmacy: Use of English + Biology + Chemistry + Physics
  - ⚖️ Law / Humanities: Use of English + Literature + Government + CRS/IRS
  - 💼 Commercial / Social Sciences: Use of English + Economics + Accounting + Commerce
- Custom Subject Switcher: Flexible dropdowns for custom 4-subject combinations.
- Question Bank Selector: 2015–2025 Verified JAMB Past Questions & PWA Offline Pack Downloader.

---

### PAGE 2: JAMB SESSION & CBT CONFIGURATOR
- Practice Mode Selection:
  - 🔘 Full 4-Subject UTME Mock: Complete 180 Questions / 120 Minutes simulation.
  - ⭕ Single-Subject Speed Drill: 40 Questions / 30 Minutes targeted drill.
  - ⭕ Instant Quiz Mode: Question-by-question scoring with AI Coach speed tips.
- Target Speed Indicator: Displays real-time pacing benchmark (e.g., "Target: 40 seconds / question").
- Custom Constraints: Slider controls for custom question volumes (10 to 180 Qs) and timer limits.

---

### PAGE 3: INTEGRATED 4-SUBJECT SPEED CBT SIMULATOR (CORE EXAM SCREEN)
- Top Navigation Bar:
  - Monospace Countdown Timer: `01:59:45` with tabular numerals.
  - 4-Subject Tab Switcher: Horizontal tabs (`[Use of English (42/60)] [Mathematics (18/40)] [Physics (0/40)] [Chemistry (0/40)]`) with active indicator animation (`150ms`).
  - On-Screen System Calculator Modal Trigger: Calculator icon button.
- Embedded System Calculator Modal:
  - Geometry: 240px width modal card, Sand fill (`#F3ECE0`), 1px border, 12px radius.
  - Display: Single-line digital display using monospace font.
  - Keypad: 4x4 button grid (Digits 0–9, +, -, ×, ÷, =, C, ±, .) with minimum 44px touch targets.
- Question Container: 18px / 28px Nunito Sans text card with 48px touch targets for options A–D.
- Question Palette Grid Drawer: 180-button overlay showing Answered (Leaf Green), Unanswered (Chalk White), and Flagged for Review (Exam Marigold).

---

### PAGE 4: JAMB INSTANT QUIZ & SPEED DRILL SCREEN (SINGLE-SUBJECT PRACTICE)
- Single-Subject Speed Layout: Rapid multiple-choice question card with real-time feedback.
- Correct State: Leaf Green (`#1B7F45`) border + "+1 Mark" badge.
- Incorrect State: Laterite Soil (`#C4532D`) border + "Not yet" coaching guidance.
- Sidekick Coach Drawer: Retractable drawer providing instant time-saving shortcuts, formula breakdowns, and rule summaries.

---

### PAGE 5: JAMB UTME SCORE & DIAGNOSTIC ANALYTICS DASHBOARD (400 MARKS)
- UTME 400-Point Score Report: Individual breakdown out of 100 per subject (e.g., English: 72, Physics: 68, Chemistry: 75, Math: 80 = Total: 295 / 400 Marks).
- Speed vs. Accuracy Matrix: Chart plotting time spent per question against accuracy to detect time-management bottlenecks.
- Diagnostic Gap Routing: Low-mastery topics are exported into the student's active Multi-Study Plan with 1 tap.
```

---

## 6. Module 5: Custom Exam Studio Subsystem (Pages 1–5)

### Subsystem Overview
The Custom Exam Studio enables students to upload personal lecture notes, slides, PDFs, or whiteboard photos, converting raw study materials into structured practice exams for subjects outside national syllabi. This module spans 5 dedicated pages.

### Master Build Prompt: Custom Exam Studio (Pages 1–5)

```markdown
# MASTER FRONT-END BUILD PROMPT: CUSTOM EXAM STUDIO (PAGES 1–5)

---

### PAGE 1: DOCUMENT UPLOAD DROPZONE & NOTE LIBRARY
- Multi-Format Drag & Drop Zone: Accepts PDF lecture slides, DOCX syllabus files, raw text pasting, and mobile photos of handwritten notes/whiteboards.
- Live Parsing Status: Animated processing state ("Processing PDF...", "Extracting key concepts...", "Ready for question generation").
- My Uploads Library: Grid of processed documents organized by custom subject folders (e.g., GST 101, ACC 201, CSC 301).

---

### PAGE 2: AI QUESTION GENERATOR & PARAMETER CONFIGURATOR
- Question Format Switcher: Multiple Choice (MCQ), Short Answer / Theory, or Mixed Format.
- Cognitive Depth Selector (Bloom's Taxonomy):
  - Recall & Definitions (Terminology & quick facts)
  - Conceptual Application (Scenario-based problem solving)
  - Advanced Problem Solving (Multi-step calculations & analysis)
- Grounded AI Constraint: Ensures generated answer keys cite exact page numbers and sections from the uploaded file ("coach, not ghostwriter" policy).

---

### PAGE 3: QUESTION BANK REVIEW & VERIFICATION STUDIO
- Inspection Grid: Side-by-side view of generated question prompts, distractor choices, answer keys, and source text quotes.
- Editorial Controls: Edit question phrasing, replace distractors, or regenerate individual items.
- Community Verification Queue: Submit custom question sets to peer review channels to earn a Verified Question Badge.

---

### PAGE 4: CUSTOM PRACTICE SESSION EXECUTION (MCQ & THEORY)
- Interactive Test Engine: Supports both Instant Quiz and Timed Exam modes for user materials.
- Rich Text Response Editor: Includes formula tools for theory questions.
- Sidekick AI Coach Integration: Provides hints grounded strictly in the uploaded document text.

---

### PAGE 5: CUSTOM MATERIAL ANALYTICS & CONCEPT MASTERY
- Document Concept Breakdown: Topic mastery bars for extracted document chapters/sections.
- Gap Export: Automatically routes low-mastery custom topics into the primary Multi-Study Plan.
```

---

## 7. Module 6: Multi-Study Plan Manager (Single-Page Interactive View)

### Overview
A clean, single-page interactive schedule manager that maps syllabus topics across weeks while allowing students to switch between multiple active plans with a single tap. It uses an adaptive timeline that automatically integrates diagnostic gaps and offers 1-tap AI schedule rebalancing without penalizing missed days.

### Master Build Prompt: Study Plan Page
```markdown
# UI/UX & FRONT-END BUILD PROMPT: MULTI-STUDY PLAN MANAGER

## OVERVIEW & DESIGN PHILOSOPHY
Create a warm, single-page interactive Study Plan Manager for "African Intelligence". The page acts as a personalized academic timeline that keeps students on track for their target exam date without overwhelming them with long forms or cluttered calendar grids.

It follows a paper-inspired aesthetic with warm neutrals, Adire textile pattern overlays, and empathetic microcopy ("coach, not ghostwriter").

---

## 1. DESIGN TOKENS & VISUAL SYSTEM

### Color Tokens (Light, Dark, and Battery Saver Modes)
- App Background (`--bg`): `#FBF7F0` (Chalk paper neutral) | Dark: `#14122B` (Night Ink)
- Surface Cards (`--surface`): `#FFFFFF` (Clean white) | Dark: `#1D1A3A` (Deep Indigo Sheet)
- Secondary Surface (`--surface-2`): `#F3ECE0` (Sand raised fill) | Dark: `#272349`
- Card Outlines (`--border`): `#E3DACB` | Dark: `#38335E`
- Primary Brand Action (`--primary`): `#3A2E9A` (Adire Indigo) | Dark: `#A79BFF` (Indigo Glow)
- Milestone & Progress Accent (`--highlight`): `#F2A91B` (Warm Marigold)
- Success & Completed State (`--success`): `#1B7F45` (Leaf Green)
- Gap Alert & Encouraging State (`--try-again`): `#C4532D` (Laterite Soil red-earth, never harsh red)
- Battery Saver Theme Override: `#0B0A18` (True Dark OLED black)

### Typography & Element Geometry
- Headings: "Fraunces" (SemiBold 600 / Bold 700) for academic warmth.
- Body & Labels: "Nunito Sans" (Regular 400 / SemiBold 600).
- Dates, Countdown & Percentages: System Monospace with tabular numerals.
- Geometry: Card Radius = `12px`, Primary Button Radius = `10px`, Selection Chips = `999px`.
- Touch Targets: Minimum **48px height** across all buttons, dropdowns, and accordion cards.

---

## 2. PAGE LAYOUT & INTERACTIVE COMPONENTS (TOP TO BOTTOM)

### SECTION 1: HEADER & ACTIVE PLAN SWITCHER
- Header Title (Fraunces 24px): "📅 Study Plan Manager".
- Active Plan Dropdown: Clean selector button (`48px` height, `--surface-2` background) displaying the current active plan:
  - Label: "📌 Active: JAMB 2027 Engineering Track (Week 4 of 12) ▼"
- Quick Switch Chips: Horizontal pills allowing 1-tap switching to secondary plans (e.g., `WAEC SSCE Science`, `Custom Physics Prep`).

### SECTION 2: MILESTONE & STEPPING STONES ROADMAP CARD
- Card Surface: Surface white (`#FFFFFF`) card with soft `1px` border (`#E3DACB`).
- Countdown Banner: "Target Exam Date: April 24, 2027 (64 Days Left)" with overall topic mastery progress bar (`64% Mastery`).
- "Stepping Stones" Visual Roadmap: A horizontal progress track showing completed weeks, current active week, and a final graduation cap icon (`🎓`).
  - Completed Weeks: Leaf Green (`#1B7F45`) badge with checkmark.
  - Active Week: Highlighted in Adire Indigo (`#3A2E9A`) with a pulse dot.
  - Future Weeks: Muted Sand fill (`#F3ECE0`).
- Quick Actions: "🔄 Rebalance Schedule" button (Primary 48px) and daily target pill ("⚡ Daily Target: 45 mins").

### SECTION 3: DYNAMIC WEEKLY SYLLABUS TIMELINE (ACCORDION CARDS)

1. ACTIVE WEEK CARD (EXPANDED BY DEFAULT):
   - Header: "📍 THIS WEEK (WEEK 4: OPTICS & ELECTROMAGNETISM)" with an ACTIVE badge in Marigold (`#F2A91B`).
   - Daily Tasks List (30–45 Minute Blocks):
     - Mon: Refraction & Lenses (30 mins) — [✅ Completed - Score 8/10]
     - Tue: Mirrors & Ray Diagrams (30 mins) — [⚡ Resume Practice Drill]
     - Wed: Electromagnetic Spectrum (45 mins) — [🔒 Upcoming]
   - Dynamic Gap Alert Box (Laterite Soil `#C4532D` accent border):
     - Microcopy: "⚠️ GAP ALERT: Electric Fields flagged from yesterday's practice drill."
     - Action Pill: "[⚡ Add 15-min Gap Review to Thursday]" (1-tap insertion into current week).

2. UPCOMING WEEKS (COLLAPSED ACCORDION CARDS):
   - Collapsible cards for future weeks (e.g., `▶ Week 5: Organic Chemistry (Feb 12 – Feb 18)`).
   - Tapping any week smoothly expands it (`200ms cubic-bezier`) to preview or edit planned topics.

### SECTION 4: SIDEKICK AI COACH INTERACTIVE ASSISTANT
- Floating or bottom card featuring the AI Coach avatar.
- Microcopy: "💬 Life happens! Want me to adjust your study pace for this weekend?"
- Actions:
  - Button 1: "🤖 Auto-Rebalance Schedule" (distributes uncompleted topics evenly across remaining weeks).
  - Button 2: "➕ Add Custom Topic to Plan" (opens quick topic insertion drawer).

---

## 3. MOTION, ACCESSIBILITY & DATA OPTIMIZATION
- Zero Bitmap Images: Uses pure CSS layouts, typography, and lightweight inline SVGs.
- Accordion Motion: Smooth expand/collapse transition (`200ms ease-out`).
- Empathetic Microcopy: Never use harsh red warning screens or "Overdue" labels for missed days. Always offer supportive rebalancing.
```

---

## 8. Module 7: Full Syllabus Diagnostic Heatmap Page

### Overview & Diagnostic Philosophy
The **Full Syllabus Diagnostic Heatmap** is an interactive diagnostic matrix that maps a student's exact knowledge gaps across every unit, topic, and sub-topic in their exam syllabus or uploaded study material. Instead of displaying a single raw percentage score (e.g., "65% in Physics"), it breaks down performance into granular conceptual building blocks to answer: *"Exactly which concepts do I know, and which specific topics are pulling my score down?"*

Following the platform's visual identity, diagnostic states use **Leaf Green** for strong topics, **Marigold** for review items, and **Laterite Soil** red-earth for critical gaps—never punitive red screens.

---

### Master Build Prompt: Full Syllabus Diagnostic Heatmap

```markdown
# UI/UX & FRONT-END BUILD PROMPT: FULL SYLLABUS DIAGNOSTIC HEATMAP

## OVERVIEW & GOAL
Build the Full Syllabus Diagnostic Heatmap page for "African Intelligence". This workspace gives students a visual, drill-down heatmap of their topic mastery across all subjects in their exam syllabus or uploaded custom materials, with 1-tap action routes to launch targeted drills or rebalance study plans.

---

## 1. DESIGN TOKENS & DIAGNOSTIC STATES

### Color Tokens & Feedback Mapping
- Background (`--bg`): `#FBF7F0` (Chalk paper neutral) | Dark: `#14122B` (Night Ink)
- Surface Cards (`--surface`): `#FFFFFF` (Clean white) | Dark: `#1D1A3A` (Deep Indigo Sheet)
- Card Borders (`--border`): `#E3DACB` | Dark: `#38335E`
- 🟢 Strong Mastery (75%–100%): `--success` Leaf Green (`#1B7F45` light / `#5FD08C` dark)
- 🟡 Needs Review (50%–74%): `--highlight` Warm Marigold (`#F2A91B` light / `#F6B93B` dark)
- 🔴 Critical Gap (<50%): `--try-again` Laterite Soil (`#C4532D` light / `#F08A63` dark)
- System Error Only: `--error` (`#C0263F` - reserved strictly for payment or network failure)
- Battery Saver Theme Override: `#0B0A18` (True Dark OLED black)

### Accessibility & Contrast Rules
- Color is never used alone: Every tile or badge MUST combine color background fill with a textual status label (e.g., "Strong", "Needs Review", "Critical Gap") and a visual icon (`🟢`, `🟡`, `🔴 ⚠️`).
- Typography: "Fraunces" for headers, "Nunito Sans" for topic titles, and System Monospace with tabular numerals for percentages and time metrics.
- Touch Targets: Minimum 48px height for filter tabs, expansion headers, and action buttons.

---

## 2. PAGE LAYOUT & COMPONENT SPECIFICATIONS (TOP TO BOTTOM)

### SECTION 1: HEADER & SUBJECT FILTER TABS
- Navigation Header: "← Back to Analytics Dashboard".
- Title (Fraunces 24px): "🗺️ Full Syllabus Topic Heatmap".
- Target Track Tag: "Track: Senior WAEC SSCE | Subject Combination: Physics, Chemistry, Biology, Mathematics".
- Horizontal Subject Filter Tabs (48px Touch Target Height):
  - `[ 🔘 All Subjects ]`  `[ ⚛️ Physics (72%) ]`  `[ 🧪 Chemistry (54%) ]`  `[ 🧬 Biology (80%) ]`
- Readiness Summary Banner:
  - Overall Exam Readiness: "68% Readiness" progress bar.
  - Summary Tags: `4 Strong Units` | `3 Review Units` | `2 Critical Gap Units ⚠️`.

### SECTION 2: DRILL-DOWN SYLLABUS TOPIC MATRIX (EXPANDABLE GRID)

1. UNIT HEADER CARDS (ACCORDION CARDS):
   - Unit Title (Fraunces 18px), Question Count, and Unit Mastery Badge.
   - Example 1: `🟢 Mechanics & Motion [88% Strong]`
   - Example 2: `🟡 Optics & Light Waves [64% Needs Review]`
   - Example 3: `🔴 Electricity & Magnetism [42% Critical Gap] ⚠️`

2. SUB-TOPIC DRILL-DOWN TILES (INSIDE EXPANDED UNIT CARD):
   - Displays granular sub-topic progress bars:
     - Kinematics & Newton's Laws: 92% [🟢 Strong]
     - Work, Energy & Power: 85% [🟢 Strong]
     - Refraction & Lenses: 50% [🟡 Needs Review]
     - Electric Fields & Coulomb's Law: 35% [🔴 Critical Gap] ⚠️
     - Current Electricity & Resistors: 48% [🔴 Critical Gap] ⚠️
   - 1-Tap Action Routing Buttons (Positioned directly under Critical Gap sub-topics):
     - Action Button 1: `[⚡ Launch 10-Min Gap Drill]` (Instantly launches a 10-question practice set focusing strictly on this concept).
     - Action Button 2: `[📅 Add to Study Plan]` (Injects a 15-minute review block into the active Multi-Study Plan).

### SECTION 3: PERFORMANCE MATRIX FILTERS & OVERLAYS
- Display Mode Switcher (Pill Switcher):
  - 🎯 Accuracy Heatmap (Displays % correct across topic questions).
  - ⏱️ Time-per-Question Heatmap (Displays average seconds spent per question using tabular numerals to spot time-management bottlenecks).
- Paper Format Filter:
  - `[ Paper 1 (Objective MCQ) ]` vs `[ Paper 2 (Theory Written) ]` performance split comparison.

---

## 3. MOTION & PERFORMANCE STANDARDS
- Accordion Expand Motion: Smooth 200ms ease-out height expansion when tapping unit header cards.
- Zero Bitmaps: Pure CSS grid and inline SVG badges for instant offline loading via PWA background caching.
- Empathetic Microcopy: Critical gaps feature supportive coaching text ("Let's review this concept together") rather than punitive red warning banners.
```

---

## 9. Module 8: Technical Architecture, Motion Framework & PWA Standards

### Vector & Motion Framework (Zero Bitmap Images)
To ensure fast rendering, low mobile data consumption, and offline execution on budget Android devices, **no raster bitmap images (PNG/JPG)** are used. All graphics are rendered as lightweight inline SVGs and CSS keyframe animations:

```css
/* Lightweight CSS Motion Framework (150ms - 250ms gentle easing) */
@keyframes slidePill {
  from { transform: translateX(-4px); opacity: 0.8; }
  to { transform: translateX(0); opacity: 1; }
}

@keyframes pulseSync {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.08); opacity: 0.8; }
}

@keyframes swayCard {
  0% { transform: translateX(0) rotate(0deg); }
  50% { transform: translateX(12px) rotate(1.5deg); }
  100% { transform: translateX(0) rotate(0deg); }
}

@keyframes drawSuccessCheck {
  0% { stroke-dashoffset: 24; }
  100% { stroke-dashoffset: 0; }
}

/* Reduced Motion Override for Accessibility */
@media (prefers-reduced-motion: reduce) {
  *, ::before, ::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

### Accessibility & PWA Performance Standards
1. **Contrast & Touch Metrics**: All text meets WCAG AA standards (minimum **4.5:1 ratio**). Interactive choices and buttons adhere strictly to a **48px touch target height**.
2. **Offline-First PWA Sync**: Built with Workbox PWA service workers to cache downloadable question packs, allowing full offline practice during network drops or power outages.
3. **Empathetic Coaching Microcopy**: All feedback avoids punitive language ("Failed", "Wrong"). Mistakes trigger supportive guidance in Laterite Soil (`#C4532D` light / `#F08A63` dark).

---

## 10. Module 9: Sidekick AI Coach, Community Workspace & In-Thread Tagging

### Architectural Overview & Dual-Space Concept
The **Sidekick AI Coach** and the **Community Workspace** function as two distinct, fully featured standalone spaces within the platform, connected via **In-Thread AI Tagging (`@SidekickCoach`)**:
* **Standalone AI Tutor Workspace (Page 15)**: A private, 1-on-1 Socratic study lab operating under the "coach, not ghostwriter" policy. It provides step-by-step hints, LaTeX mathematical/chemical equation formatting, and WAEC/NECO/JAMB marking scheme evaluation without giving away unearned answers.
* **Standalone Community Workspace (Page 16)**: A public peer-learning hub structured into departmental channels (*Science*, *Commercial*, *Arts*, *BECE Junior*) featuring daily streak challenges, Q&A discussion feeds, and a shared study vault.
* **The Interconnection Bridge (`@SidekickCoach`)**: Mentions of `@SidekickCoach` in community discussion threads bring the AI Coach directly into public peer conversations to verify answers, explain complex concepts, or audit arguments against official marking schemes.

---

### Master Build Prompt: AI Tutor & Community Hub

```markdown
# UI/UX & FRONT-END BUILD PROMPT: AI TUTOR, COMMUNITY WORKSPACE & IN-THREAD TAGGING

## 1. STANDALONE SIDEKICK AI TUTOR WORKSPACE (PAGE 15)

### Core Sections & Layout
- Header & Context Tag: "📌 Active Context: Senior WAEC Physics (Optics)" | "🤖 Sidekick AI Coach".
- Coach Mode Switcher (Pill Switcher):
  - `[ 🔘 Socratic Hint Mode ]` (Guides student with questions; no raw answers)
  - `[ ⭕ Deep Explanation Mode ]` (LaTeX formulas, step-by-step concept breakdown)
  - `[ ⭕ Exam Evaluator Mode ]` (Grades typed essay answers against WAEC/NECO marking schemes)
- Prompt Accelerator Chips (1-Tap Fast Queries):
  - `[ 💡 "Break down this formula" ]`
  - `[ 🧪 "Give a real-life example" ]`
  - `[ 📝 "Test me on this topic" ]`
  - `[ 🎯 "Show WAEC examiner trick" ]`
- Chat Area: LaTeX math rendering `\[ n_1 \sin(\theta_1) = n_2 \sin(\theta_2) \]`, chemical step rendering, and Sidekick Coach avatar.
- Action Toolbar: Attachment trigger, voice note input, `[ 💾 Save to Notes ]`, and `[ 🎴 Export to Flashcard ]`.

---

## 2. STANDALONE COMMUNITY & PEER WORKSPACE (PAGE 16)

### Core Sections & Layout
- Departmental Channel Directory: Horizontal scroll pills for `🔬 Science Track (12.4k)`, `💼 Commercial (8.1k)`, `🎨 Arts & Humanities (9.2k)`, and `🏫 JSS3 BECE Group (5.3k)`.
- Daily Challenge & Leaderboard Banner: "🏆 Today's JAMB Physics Challenge: 1,420 Completed | Top Streak: 🥇 Chidi O. (14 Days) | Your Rank: #42" + `[⚡ Join 5-Min Group Drill]` CTA button.
- Threaded Discussion Feed: Peer question cards showing post author, subject tags, peer replies, and verified AI badges.
- Shared Study Vault: Downloadable peer summary sheets (`Organic_Chem_Shortcuts.pdf`), mnemonic guides, and community-verified flashcard decks.

---

## 3. CROSSTALK INTERCONNECTION BRIDGE (@SidekickCoach TAGGING)

### Interaction Specification
1. In-Thread Tagging: Typing `@SidekickCoach` inside any community comment thread summons the AI Coach to read the full discussion context and post a verified response directly in the public feed.
2. Verified Response Badge: AI-generated responses in the community feed carry a Leaf Green (`#1B7F45`) "Verified AI Explanation" badge and cite official WAEC, NECO, or JAMB examiner marking criteria.
3. Automated Marking Scheme Audit: Typing `@SidekickCoach verify` evaluates competing peer answers against official marking schemes to settle study group debates.
4. 1-Tap Private Escalation: Every community AI response includes a `[ 💬 Continue 1-on-1 in AI Private Lab ]` button that seamlessly transfers the thread context into the student's private AI workspace for deeper inquiry.
```
