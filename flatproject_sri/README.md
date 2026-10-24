# AutomataLab — Interactive Automata & DFA Simulator Suite

[![GitHub Pages](https://img.shields.io/badge/Deployment-GitHub%20Pages-22c55e?logo=github)](https://sriharish71.github.io/flat_miniproject/)
[![FLAT Theory](https://img.shields.io/badge/Formal%20Languages-Automata%20Theory-38bdf8)](https://sriharish71.github.io/flat_miniproject/)
[![Tests](https://img.shields.io/badge/Verification%20Tests-67%2F67%20Passed%20(100%25)-10b981)]()
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero%20(Pure%20Vanilla)-a855f7)]()

> A modern, interactive web application and virtual laboratory for **Formal Languages and Automata Theory (FLAT)**. Features multiple classic **Deterministic Finite Automata (DFAs)** with dynamic vector SVG state transition diagrams, real-time input tape animation, step-by-step trace execution, interactive $\delta$-matrix highlights, and automated batch test suites.

🔗 **Live Deployment:** [https://sriharish71.github.io/flat_miniproject/](https://sriharish71.github.io/flat_miniproject/)

---

## 🚀 Supported Automata Machines

The simulator features a multi-machine selector with 5 foundational automata models:

### 1. Pattern Matching: Ends with `"01"`
- **Language:** $L = \{ w \in \{0, 1\}^* \mid w \text{ ends with } 01 \}$
- **Regular Expression:** `(0|1)*01`
- **5-Tuple:** $M = (Q, \Sigma, \delta, q_0, F)$
  - $Q = \{q_0, q_1, q_2\}$
  - $\Sigma = \{0, 1\}$
  - $q_0 = \text{Initial state}$
  - $F = \{q_2\}$
- **Transition Table ($\delta$):**

  | Current State ($q$) | Input `'0'` | Input `'1'` | Nature |
  |:---:|:---:|:---:|:---|
  | $\to q_0$ | $q_1$ | $q_0$ | Initial |
  | $q_1$ | $q_1$ | $q_2$ | Saw `'0'` |
  | $*q_2$ | $q_1$ | $q_0$ | **Final / Accept** |

---

### 2. Substring Detection: Contains Substring `"101"`
- **Language:** $L = \{ w \in \{0, 1\}^* \mid w \text{ contains substring } 101 \}$
- **Regular Expression:** `(0|1)*101(0|1)*`
- **5-Tuple:** $M = (Q, \Sigma, \delta, q_0, F)$
  - $Q = \{q_0, q_1, q_2, q_3\}$
  - $\Sigma = \{0, 1\}$
  - $q_0 = \text{Initial state}$
  - $F = \{q_3\}$ (Dead/Trap accepting loop)
- **Transition Table ($\delta$):**

  | Current State ($q$) | Input `'0'` | Input `'1'` | Nature |
  |:---:|:---:|:---:|:---|
  | $\to q_0$ | $q_0$ | $q_1$ | Initial |
  | $q_1$ | $q_2$ | $q_1$ | Saw `'1'` |
  | $q_2$ | $q_0$ | $q_3$ | Saw `'10'` |
  | $*q_3$ | $q_3$ | $q_3$ | **Final / Accept (Trap)** |

---

### 3. Modulo Arithmetic: Binary Divisible by 3 ($n \pmod 3 == 0$)
- **Language:** $L = \{ w \in \{0, 1\}^* \mid \text{bin2dec}(w) \equiv 0 \pmod 3 \}$
- **Mathematical Formula:** $\text{Remainder}_{\text{new}} = (2 \times \text{Remainder}_{\text{old}} + \text{bit}) \pmod 3$
- **Canonical Regular Expression:** `(0|1(01*0)*1)*`
- **5-Tuple:** $M = (Q, \Sigma, \delta, r_0, F)$
  - $Q = \{r_0, r_1, r_2\}$
  - $\Sigma = \{0, 1\}$
  - $q_0 = r_0$
  - $F = \{r_0\}$
- **Transition Table ($\delta$):**

  | Current State ($q$) | Input `'0'` | Input `'1'` | Value Example |
  |:---:|:---:|:---:|:---|
  | $\to *r_0$ | $r_0$ | $r_1$ | $\epsilon, 0, 3 (\text{"11"}), 6 (\text{"110"}), 9 (\text{"1001"}), 21 (\text{"10101"})$ |
  | $r_1$ | $r_2$ | $r_0$ | $1 (\text{"1"}), 4 (\text{"100"}), 7 (\text{"111"})$ |
  | $r_2$ | $r_1$ | $r_2$ | $2 (\text{"10"}), 5 (\text{"101"}), 8 (\text{"1000"})$ |

---

### 4. Parity Automaton: Even 0s and Even 1s
- **Language:** $L = \{ w \in \{0, 1\}^* \mid \text{count}(0) \pmod 2 = 0 \land \text{count}(1) \pmod 2 = 0 \}$
- **Regular Expression:** `((00|11)|(01|10)(00|11)*(01|10))*`
- **5-Tuple:** $M = (Q, \Sigma, \delta, q_{EE}, F)$
  - $Q = \{q_{EE}, q_{OE}, q_{EO}, q_{OO}\}$
  - $\Sigma = \{0, 1\}$
  - $q_0 = q_{EE}$
  - $F = \{q_{EE}\}$
- **Transition Table ($\delta$):**

  | Current State ($q$) | Input `'0'` | Input `'1'` | Nature |
  |:---:|:---:|:---:|:---|
  | $\to *q_{EE}$ | $q_{OE}$ | $q_{EO}$ | **Start & Final (Even 0s, Even 1s)** |
  | $q_{OE}$ | $q_{EE}$ | $q_{OO}$ | Odd 0s, Even 1s |
  | $q_{EO}$ | $q_{OO}$ | $q_{EE}$ | Even 0s, Odd 1s |
  | $q_{OO}$ | $q_{EO}$ | $q_{OE}$ | Odd 0s, Odd 1s |

---

### 5. Constraint & Trap State: No Consecutive `"11"`
- **Language:** $L = \{ w \in \{0, 1\}^* \mid w \text{ does not contain substring } 11 \}$ (Fibonacci binary strings)
- **Regular Expression:** `(0|10)*(1|ε)`
- **5-Tuple:** $M = (Q, \Sigma, \delta, q_0, F)$
  - $Q = \{q_0, q_1, q_{\text{Trap}}\}$
  - $\Sigma = \{0, 1\}$
  - $q_0 = q_0$
  - $F = \{q_0, q_1\}$
- **Transition Table ($\delta$):**

  | Current State ($q$) | Input `'0'` | Input `'1'` | Nature |
  |:---:|:---:|:---:|:---|
  | $\to *q_0$ | $q_0$ | $q_1$ | **Start & Accept (Ends in 0 or $\epsilon$)** |
  | $*q_1$ | $q_0$ | $q_{\text{Trap}}$ | **Accept (Ends in 1)** |
  | $q_{\text{Trap}}$ | $q_{\text{Trap}}$ | $q_{\text{Trap}}$ | Dead Trap State (Illegal `"11"`) |

---

## ✨ Application Features

- 🔄 **Multi-Machine Pill Switcher**: Seamlessly switch between automata models with a single click or keyboard navigation.
- 🎨 **Dynamic SVG State Machine Graph**: Real-time vector rendering of state nodes, double-ring accepting states, curved transition paths, and active glowing pulses.
- 🎞️ **Input Tape Visualizer**: Visual representation of the input string with dynamic `▲ HEAD` scanner and automatic centering.
- ⏯️ **Playback Controls**: Step forward, Auto Play/Pause, speed slider ($0.2\text{s}$ to $1.6\text{s}$), and full reset.
- ⌨️ **Keyboard Accessibility**:
  - <kbd>Space</kbd>: Auto Play / Pause
  - <kbd>→</kbd>: Step Forward
  - <kbd>R</kbd> or <kbd>Esc</kbd>: Reset Simulation
  - <kbd>Enter</kbd>: Execute
- 📋 **Trace Table & Formal 5-Tuple**: Step-by-step history log along with mathematical definitions $M = (Q, \Sigma, \delta, q_0, F)$ and active cell highlighting in the $\delta$ matrix.
- 🧪 **Presets & Batch Test Suites**: Pre-configured test cases for quick acceptance and rejection verification, plus a **"Run All Tests"** button that executes the full test suite in real time.
- 🛡️ **Input Validation**: Clean sanitization for $\Sigma = \{0, 1\}$ with user-friendly warning feedback on invalid characters. Empty string $\epsilon$ is fully supported across all models.

---

## 🚀 Running Locally

### Option 1: Direct Browser Launch
Double-click `index.html` in any modern web browser, or launch from PowerShell:
```powershell
Start-Process index.html
```

### Option 2: Local HTTP Server
Using Python:
```bash
python -m http.server 8080
```
Then visit: [http://localhost:8080](http://localhost:8080)

Using Node.js:
```bash
npx serve .
```

---

## 🧪 Testing and Verification

The project includes built-in verification across all 5 machines and 67 test cases (including boundary tests for $\epsilon$, prefix matching, modulo divisibility, and trap state loops).

To run verification in the browser:
1. Open the simulator.
2. Select the **Batch Tests** tab on the right panel.
3. Click **"Run All Tests"** to verify all cases with real-time pass/fail badges.

---

## 🌐 Deployment to GitHub Pages

This project is configured with a automated GitHub Actions workflow (`.github/workflows/deploy.yml`).

1. Push your code to the `main` branch:
   ```bash
   git push origin main
   ```
2. In your GitHub repository settings:
   - Navigate to **Settings** &rarr; **Pages**.
   - Under **Build and deployment** &rarr; **Source**, select **GitHub Actions**.
3. The live website is available at:
   `https://<username>.github.io/<repository-name>/`
