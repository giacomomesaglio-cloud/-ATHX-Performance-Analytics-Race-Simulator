<p align="center" style="background-color: #000000; padding: 20px 0; margin-bottom: 20px;">
  <img src="images/0.%20ATHX_logo.png" alt="ATHX Logo" width="100%" style="max-width: 800px; display: block; margin: 0 auto;"/>
</p>

# 🏋️‍♂️ ATHX Performance Analytics & Race Simulator

## 📌 Personal Background & Motivation

After spending 10 years working on major construction sites, I decided to take a sabbatical year to challenge myself both personally and professionally. One of my primary goals was to rebuild my physical fitness, which had taken a back seat during my intense work routine. 

Having always been an active sports enthusiast (beach volleyball, rock climbing, surfing, tennis), I wanted to test my limits with a completely new discipline. In **February 2026**, I began a structured training program targeting the **ATHX Competition in September 2026**—an intense, ~2.5-hour hybrid fitness event combining maximal strength, cardiovascular endurance, and metabolic conditioning.

As a data-driven individual, I couldn't resist applying analytical rigor to this athletic endeavor. What started as a personal quest to benchmark my performance evolved into a comprehensive data analysis and race simulation tool designed to uncover key competitive insights across the ATHX field.

<p align="center">
  <img src="images/Team.jpeg" alt="ATHX Team" width="500"/>
</p>

---

## 📑 About the ATHX Competition

**ATHX** is an elite hybrid fitness event designed for **teams of two athletes** competing together. The pair must strategically manage effort, split work reps, and push each other through three distinct workout zones that test the full spectrum of athletic capability.

### 🏆 Competition Categories
The event features three divisions with escalating standards for workout parameters (weights, distances, and intervals):
1. **ATHX Lite** – Entry-level standards designed for beginners and first-time hybrid athletes.
2. **ATHX** *(Our Division)* – The core competitive standard balancing heavy capacity, high volume, and endurance.
3. **ATHX Pro** – Advanced standards with heavier loads and increased work volumes for elite competitors.

---

### 🔴 Zone 1: Strength
A 20-minute heavy lifting protocol testing maximal raw strength across three fundamental movement patterns:
* **0–6 min:** 1RM Strict Press
* **6–12 min:** 3RM Back Squat
* **12–20 min:** 5RM Deadlift
* **Scoring:** Combined total weight lifted by the pair (Kg).

<p align="center">
  <img src="images/1.ATHX_Workout_Zone1.jpg" alt="ATHX Zone 1 - Strength" width="500"/>
</p>

---

### 🟡 Zone 2: Endurance
A 22-minute aerobic stamina test combining running and rowing in an alternating pair format:
* **Movement A:** Running (750m intervals for **ATHX** category)
* **Movement B:** Rowing
* **Format:** Athlete A starts on the run while Athlete B rows; athletes swap every time the runner completes their prescribed distance.
* **Scoring:** Total combined distance covered by the pair (Km).

<p align="center">
  <img src="images/2.ATHX_Workout_Zone2.jpg" alt="ATHX Zone 2 - Endurance" width="500"/>
</p>

---

### 🟢 Zone 3: MetCon X (Metabolic Conditioning)
A grueling, fast-paced metabolic circuit with a strict **25-minute time cap**:
1. **60 Cal** Ski-Erg
2. **60** Single-Arm Alternating Ground-to-Overhead (M: 20kg / F: 12.5kg)
3. **60m** Sandbag Carry (M: 50kg / F: 30kg — *split 30m/30m*)
4. **60** Box Jump Overs (M: 24" / F: 20")
5. **60m** Dual DB Walking Lunges (M: 20kg / F: 12.5kg)
6. **60m** Burpee Broad Jumps
7. **60 Cal** Ski-Erg
* **Scoring:** Total time to complete the circuit (Minutes/Seconds).

<p align="center">
  <img src="images/3.ATHX_Workout_Zone3.jpg" alt="ATHX Zone 3 - MetCon X" width="500"/>
</p>

---

## 📊 1. Data Collection & Web Scraping

The primary goal of the data collection phase was to build a comprehensive, structured dataset containing all official competition results directly from the official source: [ATHX Games Team Leaderboards](https://athxgames.com/team-leaderboards).

<p align="center">
  <img src="images/0.%20Results_scraping.png" alt="ATHX Team Leaderboard Interface" width="800"/>
</p>

### 🔍 Source Structure & Challenges
The official leaderboard interface relies on several dynamic filter variables:
* **Year:** Event edition (e.g., 2026)
* **Country & Event:** Location-specific event (e.g., *ATHX MARSEILLE 2026*)
* **Division:** Gender split (*Male*, *Female*, *Mixed*)
* **Age Group:** Age bracket selections
* **Category:** Competition level (*ATHX Lite*, *ATHX*, *ATHX Pro*)
* **Workout:** Overall ranking vs. specific zone metrics

The platform displays **10 results per page** across multiple pages (e.g., up to 20 pages / 197+ team entries for a single event configuration). Manually collecting or copying this data across different categories, events, and pages would be inefficient and error-prone.

### 🤖 Automated Web Scraping Pipeline
To overcome these limitations, an automated Python web scraping workflow was developed to:
1. **Iterate through dynamic filters:** Programmatically select and fetch data for all target divisions and events.
2. **Handle Pagination:** Automatically traverse through all paginated results (1 to N pages) per leaderboard view.
3. **Extract Raw Metrics:** Scrape key metrics for each pair, including overall rank, team names, individual zone performances (*Strength*, *Endurance*, *MetCon X*), and total points.
4. **Export Clean Dataset:** Standardize raw metric strings (e.g., parsing `808KG`, `10.487KM`, and `11:16` time formats) into clean tabular data for downstream statistical analysis.

📌 **Scraping Notebook:**  
You can explore the complete web scraping notebook and implementation here:  
👉 [`notebook/ATHX_Web_Scraping.ipynb`](notebook/ATHX_Web_Scraping.ipynb)

---

---
---
---

## 📊 2. Performance Evaluation & Simulation (ATHX Performance Evaluator)

The analytical framework begins with the integration of the **`ATHX PERFORMANCE EVALUATOR`** notebook, a dedicated tool designed to break down athlete performance and project potential outcomes:

* **Input Actual Data:** Logs and archives exact completion times, station split times, and transition intervals achieved across all official race zones.
* **Run Simulations:** Enables scenario modeling by dynamically adjusting individual zone times. This allows us to simulate "what-if" performance scenarios and evaluate their direct impact on overall ranking within the official field.

---

## 📈 3. Performance Distribution Curves

To comprehensively evaluate our team's relative standing against the complete field of competitors, two core statistical distribution visualisations were implemented across the different zones:

### A. Cumulative Percentile & Distribution Charts

![Zone 1 Performance](1.Zone_1_Tom&Giaco.jpg)
![Zone 2 Performance](2.Zone_2_Tom&Giaco.jpg)
![Zone 3 Performance](3.Zone_3_Tom&Giaco.jpg)

* **What it shows:** Displays the performance trajectory, split distributions, and completion times across individual race zones for Tom and Giaco compared to the competition field.
* **Interpretation:** Serves as a direct indicator of percentile rank per zone. Higher placement along the curve correlates to outperforming a larger portion of the field in specific disciplines.
* **Analysis of Our Performance:** Highlights our exact positions along the completion trajectory for each zone. This provides a clear, quantitative baseline showing where we outpaced competitors and where time deltas remain.

---

## 🎯 4. Athletic Profile (Radar Chart)

![Radar Chart Athletic Profile](4.Radar_chart.png)

The **Radar Chart** provides a multi-axial breakdown of our athletic performance across individual race stations and physical domains, evaluated against key benchmarks:

1. **Top 10% Benchmark:** The empirical average performance metrics calculated from the top 10% overall finishers in the competition.
2. **ATHX Progression Milestones Benchmark:** Standardized performance targets established by the ATHX methodology to guide structured athletic development.

### Profile Insights & Strategic Takeaways
* **Identified Strengths:** Clearly pinpoints stations and skill domains where our current splits closely align with or match top-tier competitor output.
* **Target Areas for Improvement:** Graphically exposes area deficits—represented by the visual gap between our profile area and the Top 10% boundary line—providing an immediate guide on which stations will deliver the highest yield from targeted training blocks.

---

## 🔍 5. Gap Analysis & Rank Improvement Analysis

### A. Gap Analysis (Top 10% Target Benchmark)

![Gap Analysis Table](6.Gap_Analysis_table.png)
![Gap Analysis Bars](7.Gap_Analysis_bars.png)

The gap analysis provides a granular breakdown of the time reductions needed across each segment to systematically reach the 90th percentile threshold:

* **Target Objective:** Match or exceed the split benchmarks established by the Top 10% finishing field.
* **Variance by Zone:** Measures exact time differences (in seconds and minutes) for every individual station. This identifies efficiency leaks and allows us to prioritize high-ROI interventions in upcoming training blocks.

### B. Rank Improvement Analysis

![Improvement Analysis](8.Improvement analysis.png)

Utilizing the interactive simulation capabilities of the **`ATHX PERFORMANCE EVALUATOR`**, a sensitivity analysis was conducted to measure leaderboard movement relative to performance gains:

* **Simulating Improvements:** Solves key strategic questions such as: *"How many leaderboard positions do we gain by shaving off 5% or 10% in our weakest stations?"*
* **Race Strategy Optimization:** Demonstrates that strategic focus on high-leverage stations yields significant jumps in overall classification, often far more effectively than marginal gains in already strong disciplines.

---

## 📓 Analytical Notebook

The complete data processing pipeline, statistical models, chart generation scripts, and simulation tools are available in the Jupyter Notebook:

* [`notebook_analitico.ipynb`](./notebook_analitico.ipynb) *(Note: Code refactoring, documentation updates, and visual polish are ongoing prior to the final release).*
