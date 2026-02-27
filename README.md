# 🎲 Monte Carlo Simulation: Strategic Decision-Making with Spreadsheets

### *Predicting Outcomes via Discrete and Normal Probability Distributions*

![Inferential Statistics](https://img.shields.io/badge/Analysis-Stochastic%20Modeling-0078D4?style=for-the-badge&logo=statistics&logoColor=white)
![Method](https://img.shields.io/badge/Method-Monte%20Carlo%20Simulation-6F42C1?style=for-the-badge&logo=diagram&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=for-the-badge&logo=google-sheets&logoColor=white)

---

## 📌 Project Overview

Static data tells you what *happened*; simulations tell you what *could happen*. This project demonstrates the use of **Monte Carlo Simulations**—a mathematical technique used to model risk and uncertainty. By using random sampling from known distributions, I developed three simulation models to forecast quality control triggers, subscription retention, and inventory requirements.

---

## 📂 Business Scenarios Modeled

1. **Manufacturing Quality Control**: Simulating DNA test kit validity to avoid expensive process destruction.

2. **Subscription Retention**: Predicting user behavior (Basic vs. Premium vs. Cancel) after a free trial.

3. **Inventory Optimization**: Modeling population physical characteristics (height) to stock appropriate equipment sizes.

---

### 📊 Project Resources

* **Interactive Spreadsheet:** [View Simulation Model on Google Sheets](https://docs.google.com/spreadsheets/d/13NfHngBBRXGd5Un8-dWl9IounXtN7qPnluQaFWaXHZQ/edit?usp=sharing)

---

## ⚙️ Analytical Methodology & Theory

### 1. Discrete Simulation: Manufacturing Quality Control (DNA Test Kits)

* **Objective:** 

    To understand the likelihood of a test kit being destroyed during validity testing. Since testing is expensive and destructive, the lab needs to simulate many batches to see how often they might hit a "quality control trigger."

* **The Theory:**

    **Bernoulli Distribution.** This models a single "trial" with only two possible outcomes: Success (Valid) or Failure (Invalid).

* **Logic & Intuition:**

    If a random sample from a Uniform Distribution ($0,1$) is $\le 0.7$ (the probability of validity), the test is "Valid." By establishing a 70% success rate as our constant, we can simulate the outcome of any number of boxes. We use a uniform random number generator to determine if a box "passes" or "fails" based on that probability threshold.

* **Steps & Formula:**

    1. Generate a random seed using `=RAND()`.
    2. Apply logic: `=IF(A2 <= 0.7, "VALID", "INVALID")`.
    3. Visualized the "Quality Control Trigger" across 10-track batches.

* *Why:* Because the RAND function is uniform, 70% of generated values will fall at or below 0.7.

<p align="center">
<img src="Count of Test Validity.png" width="60%" />
</p>

* **The Result:**

    The simulation mirrored the 70% probability but revealed that failures often occur in "clusters" due to randomness rather than technical faults.

* **Strategic Insight:**

    The lab should use this to define a "Normal Failure Range." If actual lab results fall significantly outside this simulated range, it indicates a systemic issue rather than simple statistical variance.

---

### 2. Multi-Outcome Simulation: Subscription Retention (Subscription Outcomes)

* **Objective:** 

    To forecast revenue and churn by simulating user decisions after a free trial without needing to interview every individual user.

* **The Theory:**
  
    **Discrete Categorical Distribution.** Modeling three or more distinct outcomes. This expands on binary logic to accommodate multiple fixed outcomes (Basic, Premium, or Canceled).

* **Logic & Intuition:**
  
    We divide the total probability (1.0) into three specific "buckets" based on market research:
    * 0.0 - 0.3: Basic Subscription
    * 0.3 - 0.5: Premium Subscription
    * 0.5 - 1.0: Cancellation

* **Steps & Formula:**
  
1. Generate 100 samples using `=RANDARRAY(100)`: to scale the simulation to 100 users for statistical stability.
2. Apply nested logic: `=IFS(A2<=0.3, "Basic", A2<=0.5, "Premium", A2>0.5, "Canceled")`.

* *Why:* This maps the seeds to the specific market shares: 30% for Basic, 20% for Premium, and 50% for Canceled.

<p align="center">
<img src="Count of Subscriber Outcome.png" width="60%" />
</p>

* **The Result:**

    The 100-user simulation produced a breakdown of approximately **50% Cancellations, 20% Premium, and 30% Basic.**

* **Strategic Insight:**

    Small samples (n=10) showed high volatility, while n=100 provided stable results.

* **Recommendation:**

    Operations should focus on the "Basic" tier (30%) as the primary target for retention campaigns to offset the 50% churn.

---

### 3. Continuous Simulation: Inventory Optimization (Male Heights)

* **Objective:** To optimize diving suit inventory by simulating the physical height distribution of 100 customers.

* **The Theory:**
  
    **Normal Distribution (The Bell Curve).** Modeling data that clusters around a mean.

* **Logic & Intuition:**
  
    Height is continuous. Using the Inverse Transform Method (NORM.INV) to turn a uniform random number into a height based on a population Mean ($\mu$) and Standard Deviation ($\sigma$).

* **Steps & Formula:**
  
1. Identify **Population Parameters**: Mean ($\mu$) = 172cm, Std Dev ($\sigma$) = 7.1cm.
2. Calculated height: `=NORM.INV(RAND(), 172, 7.1)`.
3. Summarized results using a Histogram to observe the "Bell Curve."

* *Why:* `NORM.INV` calculates the exact value on a bell curve that corresponds to a specific probability.

<p align="center">
<img src="Histogram of height.png" width="60%" />
</p>

* **The Result:**

  Comparison of **Population Parameters** vs. **Sample Statistics**:

  | Metric | Population Parameters | Sample Statistics (Simulated) |
  | --- | --- | --- |
  | **Mean** | 172 | **172.048** |
  | **Standard Deviation** | 7.1 | **7.275** |

* **Strategic Insight:**

    Despite a sample mean near 172cm, the simulation identified outliers at 192cm+. To maintain 100% service levels, the business should stock a "safety buffer" of extreme sizes (Outliers), even if they only appear in 1% of simulations.

* **Recommendation:** 
    
    **Outlier Identification (Inventory Management)**: The Normal Distribution simulation identified "Extreme Outliers" (e.g., individuals over $191\text{cm}$ or under $155\text{cm}$). Inventory curation must include a 5% buffer for "extreme" sizes to accommodate the "tails" of the distribution.

---

## 🛠️ Summary of Statistical Logic

  | Function | Statistical Concept | Business Application |
  | --- | --- | --- |
  | **RAND** | Uniform Randomness | The "Uncertainty Factor" in any system. |
  | **IF / IFS** | Discrete Mapping | Mapping uncertainty to specific choices (Yes/No, Type A/B/C). |
  | **NORM.INV** | Continuous Modeling | Simulating real-world measurements (Time, Weight, Height). |
  | **ARRAYFORMULA** | Scaling | Moving from one "Guess" to 1,000 "Simulations." |

---

## 🔬 Analytical Deep Dive: Why Simulate?

While we know the **Population Parameters** (e.g., 50% will cancel), businesses operate in the "Actual," not the "Ideal." Simulation bridges this gap:

* **Modeling Volatility:** Simulation shows the "spread" of possible outcomes. It helps answer: *"If I have an unlucky month, what is the worst-case churn I need to be prepared for?"*

* **The Outlier Effect:** Parameters only tell us the average; simulations reveal the extremes. Seeing a 192cm individual in a sample run forces an inventory manager to plan for physical outliers that a mean value ignores.

* **Stress Testing:** Because the **Sample Statistics** generated (Mean 172.04) are so close to our target **Population Parameters** (172), it proves the logic of our predictive model is sound.

* **Defining Thresholds:** By simulating 1,000 batches, we find the "Probability of the Exceptional." This allows us to set **Operational Thresholds**—knowing exactly when a batch of results is a statistical fluke versus a systemic failure.
---

## 🎓 Project Credits

Developed as part of the **Applied Statistics for Data Analytics** course by **DeepLearning.AI** on Coursera.

## 👤 About the Author

**Ayushi Gajendra** *Product & Operations Analyst*
I specialize in using **Inferential Statistics** and **Sample Statistics** to validate **Population Parameters** and drive data-backed strategy.

