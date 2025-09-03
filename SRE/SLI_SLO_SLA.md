# 🌐 SLI, SLO, SLA — Explained Simply

Think of a **pizza delivery service** 🍕 (instead of servers).

---

## 🔑 The Three Terms

### 1. SLA (Service Level Agreement)  
👉 A *promise* you make to customers.  
- **Business-facing**.  
- If you break it → customer gets compensation.  

**Example:**  
- “We promise your pizza will arrive within **30 minutes**, 95% of the time.”  
- If it’s late, you get a refund.  

---

### 2. SLO (Service Level Objective)  
👉 A *goal* the engineering team sets to stay within the SLA.  
- **Internally focused**.  
- Usually stricter than SLA (to give buffer).  

**Example:**  
- Internal goal: deliver 97% of pizzas within **25 minutes**.  
- This way, you’re safely above the SLA target.  

---

### 3. SLI (Service Level Indicator)  
👉 The actual **measurement/metric**.  
- **The number you track**.  
- Defines success/failure quantitatively.  

**Example:**  
- % of pizzas delivered within 25 minutes in the last 30 days.  
- If it drops below 97% → you’re missing the SLO.  

---

## 💻 In Tech Terms
- **SLI** = The metric (e.g., 99.9% of HTTP requests return < 500ms).  
- **SLO** = The goal (e.g., 99.9% over 30 days).  
- **SLA** = The legal/business promise (e.g., 99.5% uptime, or customer gets credits).  

---

## ✅ One-Liner Summary
- **SLI = What you measure.**  
- **SLO = What you aim for.**  
- **SLA = What you promise (with consequences).**  


## 🔹 SLO is about *success*
- An **SLO (Service Level Objective)** defines the target success level.  
- Example:  
  - **SLO = 99.9% availability** → means you want **99.9% of time (or requests)** to be good.

---

## 🔹 Error budget is about *failure allowance*
- By definition, the **error budget** is the **allowable fraction of failure**.  


---

## 🔹 Example in Time
Total time in a 30-day month:
- `30 × 24 × 60 = 43,200 minutes`  
- **SLO = 99.9% = 0.999 success**  
- **Error budget = 1 – 0.999 = 0.001 (0.1%)**
- 43,200 × 0.001 = 43.2 minutes downtime allowed



---

## 🔹 Example in Requests
Say you handle **10M requests/day**:  
- **SLO = 99.95% success rate**  
- Error budget = `1 – 0.9995 = 0.0005 (0.05%)`
- 10,000,000 × 0.0005 = 5,000 requests may fail per day

