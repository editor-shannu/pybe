# PyBe TraceLab — Cognitive Notional Machine & Step-by-Step Python Simulator

> **"Transforming abstract code into visible, interactive mental models."**  
> *A production-grade pedagogical extension for PyBe built by Shanmukha Medisetty.*

---

## 🌟 The Core Feature: PyBe TraceLab

In computing education, beginners frequently suffer from the **"Hidden State Illusion"** (*Sorva, 2013*). While reading Python code, the text on screen is static, but the computer's internal memory state is dynamically changing. Beginners cannot visualize what variables exist at line 2 versus line 4, how conditions evaluate dynamically, or how accumulators evolve across loop cycles.

**PyBe TraceLab** introduces a complete **Cognitive Notional Machine & Execution Laboratory** to the PyBe platform:

1. 🔬 **Interactive Execution Stepper & AST Inspector**: Step forward and backward through Python code line-by-line with active glowing indicators, execution pointer badges, and adjustable playback speeds (`0.5x`, `1x`, `2x`).
2. 🧠 **Notional Machine Memory Watch**: Real-time variable register board displaying variable identifiers, data type pills (`int`, `float`, `str`, `list`, `dict`, `bool`), and mutation flash animations (`@keyframes pulseMutation`) showing previous versus updated values.
3. 🎯 **Socratic "Predict-the-State" Micro-Checkpoints**: At key decision points and arithmetic calculations, the simulator pauses and challenges the learner to predict the memory state or boolean branch outcome (*Chi's ICAP Framework — Interactive vs Passive Learning*).
4. 🧭 **Physical-to-Abstract Real-World Anchor**: Maps abstract code transitions back to physical scenario invariants (e.g. school bag on scale, canteen tray receipt, temperature threshold alert).
5. 🛡️ **Automated Misconception Diagnostician**: Detects classic novice cognitive traps (range boundary exclusion, accumulator reset inside loop, assignment `=` in condition, type coercion issues) with 1-click remediation advice.
6. ⚡ **Custom Python Code Sandbox**: Write or edit arbitrary Python code and generate an instant, interactive Notional Machine execution trace.
7. 📊 **Cognitive Analytics & Roadmap**: Tracks prediction accuracy, session counts, and concept mastery distributions.

---

## 📚 Learning Science & Pedagogical Grounding

- **Juha Sorva — Notional Machine Theory (2013)**: Software state is invisible. Making variable registers, stack frames, and mutation events visible eliminates the novice "black box" illusion.
- **Michelene Chi — ICAP Framework (2009)**: Active and interactive cognitive engagement (predicting the next state before seeing it) yields significantly higher conceptual retention than passive code reading.
- **K. Anders Ericsson — Deliberate Practice (1993)**: Immediate, targeted explanations on why a predicted state was correct or incorrect builds strong mental models.
- **David Kolb — Experiential Learning Cycle (1984)**: Completes the 4th quadrant (Active Experimentation) by allowing students to step through, predict, and mutate code states directly.

---

## 🛠️ Tech Stack & Architecture

- **Frontend**: React 18 + Vite, Lucide Icons, Modern Glassmorphism CSS design system.
- **Backend**: Node.js + Express (RESTful API).
- **Tracer Engine**: Deterministic AST-level state simulator in Node.js (offline-first, zero external sandbox risks).
- **Data Store**: Local JSON storage (`server/src/data/db.json`).

---

## 🚀 Quick Start Guide

### 1. Prerequisites
- **Node.js**: v18.0.0 or higher
- **npm**: v9.0.0 or higher

### 2. Installation & Setup
From the `Shanmukha Medisetty` directory:

```bash
# Install root, server, and client dependencies
npm run installAll

# Configure environment (defaults work offline out-of-the-box)
cp server/.env.example server/.env

# Seed the 30 scenario curriculum
npm run seed

# Launch both server (Port 5000) and client (Port 5173)
npm run dev
```

### 3. Accessing the Application
- **Frontend UI**: http://localhost:5173
- **Backend API**: http://localhost:5000/api
- **Health Check**: http://localhost:5000/api/health

---

## 📡 API Endpoints Specification

### `POST /api/tracer/trace`
Generates step-by-step Notional Machine execution traces from scenario or user code.
- **Request Body**: `{ "scenarioId": "...", "code": "optional custom code" }`
- **Response**:
```json
{
  "code": "samosa = 20\njuice = 15\ntotal = samosa + juice\nprint(f'Total: {total}')",
  "totalSteps": 4,
  "steps": [
    {
      "stepNumber": 1,
      "line": 1,
      "code": "samosa = 20",
      "actionType": "assignment",
      "variables": [
        { "name": "samosa", "value": "20", "type": "int", "isNew": true, "isUpdated": false }
      ],
      "physicalAnchor": "🍽️ Canteen Counter: Ordering snack items.",
      "checkpoint": null
    }
  ],
  "stdout": ["Total: 35"],
  "misconceptions": []
}
```

### `POST /api/tracer/predict`
Validates Socratic state prediction answers.
- **Request Body**: `{ "checkpoint": { ... }, "selectedIndex": 0 }`
- **Response**: `{ "isCorrect": true, "pedagogicalFeedback": "...", "explanation": "..." }`

---

## 📁 Repository Structure

```
summership-26-prs/Shanmukha Medisetty/
├── client/
│   ├── index.html                   # HTML entry point with Google Fonts
│   ├── package.json                 # Client dependencies
│   ├── vite.config.js               # Vite bundler config
│   └── src/
│       ├── main.jsx                 # Top-level React UI & Notional Machine Stepper
│       └── styles.css               # Modern glassmorphism design system
├── server/
│   ├── package.json                 # Server dependencies
│   ├── src/
│   │   ├── index.js                 # Server entry & route mounting
│   │   ├── seed.js                  # 30 scenario curriculum seed script
│   │   ├── data/
│   │   │   ├── store.js             # JSON database store
│   │   │   └── roadmap.js           # PyBe V0–V3 roadmap items
│   │   ├── routes/
│   │   │   ├── tracer.js            # Notional Machine & Prediction endpoints
│   │   │   ├── scenarios.js         # Scenario CRUD
│   │   │   ├── sessions.js          # Session persistence with tracerMetrics
│   │   │   ├── analytics.js         # Cognitive analytics with prediction metrics
│   │   │   ├── codeReview.js        # Static practice check
│   │   │   └── roadmap.js           # Roadmap route
│   │   └── services/
│   │       ├── tracerEngine.js      # Core Notional Machine emulator & Misconception analyzer
│   │       ├── codeEvaluator.js     # Static practice evaluator
│   │       └── learningEngine.js    # Abstraction mapping & code generator
└── readme.md                        # Project documentation
```

---

## 👤 Author Information

- **Contributor:** Shanmukha Medisetty
- **Project:** PyBe TraceLab — Cognitive Notional Machine & Step-by-Step Python Simulator
