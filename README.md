# 🎲 Monte Carlo Simulation: Strategic Decision-Making with Spreadsheets

### *Predicting Outcomes via Discrete and Normal Probability Distributions*

---

## 📌 Project Overview

Static data tells you what *happened*; simulations tell you what *could happen*. This project demonstrates the use of **Monte Carlo Simulations**—a mathematical technique used to model risk and uncertainty. By using random sampling from known distributions, I developed three simulation models to forecast quality control triggers, subscription retention, and inventory requirements.

---

## 📂 Business Scenarios Modeled

### 1. Manufacturing Quality Control (DNA Test Kits)

**Objective:** To understand the likelihood of a test kit being destroyed during validity testing. Since testing is expensive and destructive, the lab needs to simulate many batches to see how often they might hit a "quality control trigger."

* **The Theory:** **Bernoulli Distribution.** This models a single "trial" with only two possible outcomes: Success (Valid) or Failure (Invalid).
* **Logic & Intuition:** By establishing a 70% success rate as our constant, we can simulate the outcome of any number of boxes. We use a uniform random number generator to determine if a box "passes" or "fails" based on that probability threshold.
* **Steps & Formula:**
1. Generate a random seed using `=RAND()`.
2. Apply logic: `=IF(A2 <= 0.7, "✅VALID", "❌INVALID")`.


* *Why:* Because the RAND function is uniform, 70% of generated values will fall at or below 0.7.


* **The Result:** The simulation mirrored the 70% probability but revealed that failures often occur in "clusters" due to randomness rather than technical faults.
* **Strategic Insight:** The lab should use this to define a "Normal Failure Range." If actual lab results fall significantly outside this simulated range, it indicates a systemic issue rather than simple statistical variance.

---

### 2. User Conversion Pipeline (Subscription Outcomes)

**Objective:** To forecast revenue and churn by simulating user decisions after a free trial without needing to interview every individual user.

* **The Theory:** **Discrete Categorical Distribution.** This expands on binary logic to accommodate multiple fixed outcomes (Basic, Premium, or Cancel).
* **Logic & Intuition:** We divide the total probability (1.0) into three specific "buckets" based on market research. The random seed's landing spot determines the user's path.
* **Steps & Formula:**
1. Generate 100 samples using `=RANDARRAY(100)`.
2. Apply nested logic: `=IFS(A2<=0.3, "Basic", A2<=0.5, "Premium", TRUE, "Cancel")`.


* *Why:* This maps the seeds to the specific market shares: 30% for Basic, 20% for Premium, and 50% for Cancel.


* **The Result:** The 100-user simulation produced a breakdown of approximately **50% Cancellations, 20% Premium, and 30% Basic.**
* **Strategic Insight:** Small samples (n=10) showed high volatility, while n=100 provided stable results. **Recommendation:** Operations should focus on the "Basic" tier (30%) as the primary target for retention campaigns to offset the 50% churn.

<p align="center">
<img src="subscription-outcomes.png" width="60%" />
</p>

---

### 3. Inventory Optimization (Male Heights)

**Objective:** To optimize diving suit inventory by simulating the physical height distribution of 100 customers.

* **The Theory:** **Normal Distribution (The Bell Curve).**
* **Logic & Intuition:** Height is continuous. We use the "Inverse Transform" method to turn a flat random number into a height value that follows the natural "clustering" seen in human populations.
* **Steps & Formula:**
1. Identify **Population Parameters**: Mean ($\mu$) = 172cm, Std Dev ($\sigma$) = 7.1cm.
2. Apply Transform: `=NORM.INV(RAND(), 172, 7.1)`.


* *Why:* `NORM.INV` calculates the exact value on a bell curve that corresponds to a specific probability.


* **The Result:** Comparison of **Population Parameters** vs. **Sample Statistics**:

| Metric | Population Parameters | Sample Statistics (Simulated) |
| --- | --- | --- |
| **Mean** | 172 | **172.048** |
| **Standard Deviation** | 7.1 | **7.275** |

* **Strategic Insight:** Despite a sample mean near 172cm, the simulation identified outliers at 192cm+. **Recommendation:** Inventory curation must include a 5% buffer for "extreme" sizes to accommodate the "tails" of the distribution.

---

## 🛠️ Summary of Statistical Logic

| Function | Statistical Concept | Business Application |
| --- | --- | --- |
| **RAND** | Uniform Randomness | The "Uncertainty Factor" in any system. |
| **IF / IFS** | Discrete Mapping | Mapping uncertainty to specific choices (Yes/No, Type A/B/C). |
| **NORM.INV** | Continuous Modeling | Simulating real-world measurements (Time, Weight, Height). |
| **ARRAYFORMULA** | Scaling | Moving from one "Guess" to 1,000 "Simulations." |

---

## 🎓 Project Credits

Developed as part of the **Applied Statistics for Data Analytics** course by **DeepLearning.AI** on Coursera.

## 👤 About the Author

**Ayushi Gajendra** *Product & Operations Analyst*
I specialize in using **Inferential Statistics** and **Sample Statistics** to validate **Population Parameters** and drive data-backed strategy.
