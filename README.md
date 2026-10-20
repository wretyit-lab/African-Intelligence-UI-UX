[design.md](https://github.com/user-attachments/files/33730029/design.md)
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
  }
}
```

### Accessibility & PWA Constraints
1. **Contrast & Touch Metrics**: All text meets WCAG AA standards (minimum **4.5:1 ratio**). Interactive elements adhere strictly to **48px touch target height**.
2. **Offline-First PWA Sync**: Built with Workbox PWA service workers to cache downloadable question packs, allowing full offline practice during network drops or power outages [2, 3].
3. **Empathetic Coaching Microcopy**: All feedback avoids punitive language ("Failed", "Wrong"). Mistakes trigger supportive guidance in Laterite Soil (`#C4532D`) [3].
