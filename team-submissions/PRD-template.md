# Product Requirements Document (PRD)

**Project Name:** [e.g., LABS-Solv-V1]
**Team Name:** Mehrafrouz
**GitHub Repository:** [https://github.com/AdeleMehrafrouz/2026-NVIDIA/tree/main/team-submissions]

---

> **Note to Students:** > The questions and examples provided in the specific sections below are **prompts to guide your thinking**, not a rigid checklist. 
> * **Adaptability:** If a specific question doesn't fit your strategy, you may skip or adapt it.
> * **Depth:** You are encouraged to go beyond these examples. If there are other critical technical details relevant to your specific approach, please include them.
> * **Goal:** The objective is to convince the reader that you have a solid plan, not just to fill in boxes.

---

## 1. Team Roles & Responsibilities [You can DM the judges this information instead of including it in the repository]

| Role | Name | GitHub Handle | Discord Handle
| :--- | :--- | :--- | :--- |
| **Project Lead** (Architect) | Adele Mehrafrouz | https://github.com/AdeleMehrafrouz | adele_58262_45899 |
| **GPU Acceleration PIC** (Builder) | [Name] | [@handle] | [@handle] |
| **Quality Assurance PIC** (Verifier) | [Name] | [@handle] | [@handle] |
| **Technical Marketing PIC** (Storyteller) | [Name] | [@handle] | [@handle] |

---

## 2. The Architecture
**Owner:** Project Lead

### Choice of Quantum Algorithm
* **Algorithm:** Digitized counterdiabatic-inspired circuit (tutorial baseline), with plans to explore QAOA-style ansätze in Phase 2.


* **Motivation:**  
For Phase 1, I focused on fully understanding and validating the tutorial’s counterdiabatic construction and the hybrid quantum–classical workflow. For Phase 2, I plan to explore QAOA-style parameterized circuits as an alternative quantum seed, since their layered structure may align well with the correlation structure of LABS sequences.

### Literature Review
* **Reference:** Scaling advantage with quantum-enhanced memetic tabu search,Alejandro Gomez Cadavid, https://arxiv.org/html/2511.04553v1
* **Relevance:** This paper motivates the hybrid approach used in this project, where quantum-generated samples seed a classical Memetic Tabu Search rather than replace it, and shows that such seeding can improve scaling behavior.
---

## 3. The Acceleration Strategy
**Owner:** GPU Acceleration PIC

### Quantum Acceleration (CUDA-Q)
* **Strategy:** For Phase 1, all quantum circuits are validated on CPU using CUDA-Q in qBraid. 
 

### Classical Acceleration (MTS)
* **Strategy:** The classical MTS is currently CPU-based. In Phase 2, I plan to explore GPU acceleration of the energy evaluation step using vectorized or batched computation to reduce the cost of neighborhood exploration.

### Hardware Targets
* **Dev Environment:** qBraid (CPU) for algorithm development and validation
* **Production Environment:** [e.g., Brev A100-80GB for final N=50 benchmarks]

---

## 4. The Verification Plan
**Owner:** Quality Assurance PIC

### Unit Testing Strategy
* **Framework:** [e.g., `pytest`, `unittest`]
* **AI Hallucination Guardrails:** [How do you know the AI code is right?]
    * *Example:* "We will require AI-generated kernels to pass a 'property test' (Hypothesis library) ensuring outputs are always within theoretical energy bounds before they are integrated."

### Core Correctness Checks
* **Check 1 (Symmetry):** [Describe a specific physics check]
    * *Example:* "LABS sequence $S$ and its negation $-S$ must have identical energies. We will assert `energy(S) == energy(-S)`."
* **Check 2 (Ground Truth):**
    * *Example:* "For $N=3$, the known optimal energy is 1.0. Our test suite will assert that our GPU kernel returns exactly 1.0 for the sequence `[1, 1, -1]`."

---

## 5. Execution Strategy & Success Metrics
**Owner:** Technical Marketing PIC

### Agentic Workflow
* **Plan:** [How will you orchestrate your tools?]
    * *Example:* "We are using Cursor as the IDE. We have created a `skills.md` file containing the CUDA-Q documentation so the agent doesn't hallucinate API calls. The QA Lead runs the tests, and if they fail, pastes the error log back into the Agent to refactor."

### Success Metrics
* **Metric 1 (Approximation):** [e.g., Target Ratio > 0.9 for N=30]
* **Metric 2 (Speedup):** [e.g., 10x speedup over the CPU-only Tutorial baseline]
* **Metric 3 (Scale):** [e.g., Successfully run a simulation for N=40]

### Visualization Plan
* **Plot 1:** [e.g., "Time-to-Solution vs. Problem Size (N)" comparing CPU vs. GPU]
* **Plot 2:** [e.g., "Convergence Rate" (Energy vs. Iteration count) for the Quantum Seed vs. Random Seed]

---

## 6. Resource Management Plan
**Owner:** GPU Acceleration PIC 

* **Plan:** [How will you avoid burning all your credits?]
    * *Example:* "We will develop entirely on Qbraid (CPU) until the unit tests pass. We will then spin up a cheap L4 instance on Brev for porting. We will only spin up the expensive A100 instance for the final 2 hours of benchmarking."
    * *Example:* "The GPU Acceleration PIC is responsible for manually shutting down the Brev instance whenever the team takes a meal break."
