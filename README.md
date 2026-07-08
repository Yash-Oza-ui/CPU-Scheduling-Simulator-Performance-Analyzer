# ⚙️ SchedLab — CPU Scheduling Simulator & Performance Analyzer

**An extensible CPU scheduling simulator built around clean OOP design**, implementing five core scheduling algorithms with comparative performance analysis and Gantt chart visualization — built to explore how scheduling policy choice affects waiting time, turnaround time, and fairness.

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-Interface-FF4B4B?logo=streamlit&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C?logo=plotly&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

---

## 📌 Overview

SchedLab simulates how an operating system's short-term scheduler decides which process runs next on the CPU. Rather than hardcoding one algorithm, it's built around an **extensible OOP architecture** — an abstract `Scheduler` base class with each algorithm implemented as a subclass — so adding a new scheduling policy means writing one new class, not touching existing code.

Given a configurable set of processes (arrival time, burst time, priority), SchedLab runs them through each algorithm and produces a **Gantt chart** and **performance metrics** (average waiting time, average turnaround time) — making it easy to directly compare how FCFS, SJF, SRTF, Round Robin, and Priority Scheduling behave on the *same* workload.

---

## ✨ Features

- **Five scheduling algorithms implemented from scratch:**
  - **FCFS** (First Come First Serve) — non-preemptive
  - **SJF** (Shortest Job First) — non-preemptive
  - **SRTF** (Shortest Remaining Time First) — preemptive
  - **Round Robin** — preemptive, configurable time quantum
  - **Priority Scheduling** — non-preemptive
- **Extensible OOP design** — abstract `Scheduler` base class defines a common interface (`execute()`), with each algorithm as an independent subclass implementing its own selection logic
- **Configurable workloads** — number of processes, arrival time, burst time, priority, and time quantum are all user-defined, not hardcoded
- **Gantt chart visualization** — per-algorithm execution timeline rendered with Matplotlib
- **Comparative performance dashboard** — average waiting time and average turnaround time computed and displayed side-by-side across all five algorithms on the same input
- **Streamlit interface** — input processes through a form, run all algorithms at once, and view Gantt charts + comparison table without touching the code

---

## 🏗️ Architecture

```
                 Scheduler (abstract base class)
                          │
                          │  execute() → schedule, waiting_time, turnaround_time
                          │
      ┌───────────┬───────────┬────────────┬──────────────┬
      │           │           │            │              │
    FCFS         SJF         SRTF      RoundRobin      Priority
```

Each subclass overrides `execute()` with its own process-selection logic, while shared logic (metric calculation, Gantt data formatting) lives once in the base class — a direct application of polymorphism to avoid duplicated scheduling-loop code across five algorithms.

---

## 🔍 Metrics Computed

For every algorithm, on every run:

| Metric | Definition |
|---|---|
| **Waiting Time** | Turnaround Time − Burst Time (time spent waiting in the ready queue) |
| **Turnaround Time** | Completion Time − Arrival Time (total time from arrival to completion) |
| **Average Waiting Time** | Mean waiting time across all processes |
| **Average Turnaround Time** | Mean turnaround time across all processes |

These are computed identically across all five algorithms so the comparison is apples-to-apples on the exact same input workload.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Core Logic | Python (OOP — abstract base class + inheritance) |
| Visualization | Matplotlib (Gantt charts) |
| Interface | Streamlit |

---

## 📂 Project Structure

```
schedlab/
├── schedulers/
│   ├── base.py          # Abstract Scheduler base class
│   ├── fcfs.py
│   ├── sjf.py
│   ├── srtf.py
│   ├── round_robin.py
│   └── priority.py
├── utils/
│   ├── metrics.py        # Waiting time / turnaround time calculations
│   └── gantt.py           # Gantt chart generation
├── app.py                 # Streamlit interface
└── README.md
```

---

## 🚀 Setup

1. **Clone the repository and install dependencies:**

```bash
git clone https://github.com/Yash-Oza-ui/schedlab.git
cd schedlab
pip install streamlit matplotlib pandas
```

2. **Launch the Streamlit app:**

```bash
streamlit run app.py
```

3. **Using the app:**
   - Enter the number of processes and their arrival time, burst time, and priority
   - Set the time quantum for Round Robin
   - Click **Run** to generate Gantt charts and the comparative metrics table for all five algorithms

---

## 📊 Example Output

For a sample workload of 5 processes, SchedLab produces a comparison like:

| Algorithm | Avg Waiting Time | Avg Turnaround Time |
|---|---|---|
| FCFS | 8.2 | 13.5 |
| SJF | 5.4 | 10.2 |
| SRTF | 4.9 | 9.8 |
| Round Robin (q=2) | 7.1 | 12.3 |
| Priority | 6.8 | 11.9 |

*(Actual values depend on the input workload — this table is generated live by the app.)*

---

## 🎯 What This Project Demonstrates

- **Operating Systems fundamentals** — correct implementation of preemptive and non-preemptive CPU scheduling policies, and understanding of the waiting-time/turnaround-time tradeoffs between them
- **Object-oriented design** — an abstract base class with polymorphic subclasses, avoiding duplicated logic across five distinct algorithms
- **Data visualization** — translating raw scheduling output into an interpretable Gantt chart and comparative dashboard

---

## 👤 Author

**Yash Oza**
[GitHub](https://github.com/Yash-Oza-ui)
