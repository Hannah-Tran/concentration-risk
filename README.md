# Concentration Risk Analysis by Loan Purpose Using SQL

## 📊 Project Overview
This project analyses over 2 million peer-to-peer loans from the Lending Club dataset (2007–2018) to assess concentration risk by loan purpose. It examines where exposure is concentrated, whether risky segments carry hidden risk beyond their credit grade, how concentration has changed over time, and how much loss the portfolio would absorb under stress. The analysis applies CFA-level portfolio and credit risk frameworks, implemented entirely in SQL.

## 🎯 Objective
To simulate how a credit risk analyst monitors portfolio concentration: measuring exposure by purpose, separating purpose risk from grade risk, quantifying diversification with the Herfindahl-Hirschman Index (HHI), and stress testing losses — presented as a portfolio-ready case study.

## 🧰 Tools Used
- SQL (SQLite via DB Browser for SQLite)
- GitHub (project documentation)
- Dataset: [Lending Club Loan Data 2007–2018](https://www.kaggle.com/datasets/wordsforthewise/lending-club) via Kaggle

## 📂 Folder Structure
```
credit-portfolio-risk-sql/
├── queries/
│   └── 03_concentration_risk.sql
└── README.md
```

## 📌 Key Business Questions
1. How much money sits in each loan purpose, and what does each purpose actually lose after recoveries?
2. Is a purpose risky in itself, or only because of the grades of its borrowers?
3. Where inside the largest purposes do the losses come from?
4. Has concentration increased over time?
5. How diversified is the portfolio really?
6. How much loss would the portfolio absorb if the worst historical vintage repeated?

## 🔍 Analysis Structure


| Query | Business Question | Technique |
|-------|-------------------|-----------|
| 1 | Exposure and net loss by purpose | Dollar-weighted default rate, net loss after recoveries |
| 2 | Purpose risk versus grade risk | Mix-adjusted default (actual vs expected), CTE and JOIN |
| 3 | Losses by purpose and grade | Cross-segment drill-down with minimum sample size |
| 4 | Concentration trend over time | Exposure share by vintage |
| 5 | True level of diversification | HHI and Effective N (1 / HHI) |
| 6 | Worst-vintage stress test | Data-driven stress multiplier applied to each purpose |

## 🧠 Methodology Notes
- **Resolved loans only:** default metrics use Fully Paid and Charged Off loans. Loans still Current or Late have no final outcome and would understate default rates, especially for recent vintages and 60-month terms
- **Net loss, not assumed loss:** loss is calculated as funded amount minus principal repaid minus recoveries, replacing the common assumption of 100% loss given default
- **Mix adjustment:** Query 2 compares each purpose's actual default rate with the rate expected from its grade mix. A positive gap indicates risk the grade does not capture
- **Evidence-based stress test:** the multiplier is taken from the worst observed vintage (vintages above 5,000 loans only) instead of an arbitrary shock



## ✅ How to Reproduce
1. Download the Lending Club dataset from [Kaggle](https://www.kaggle.com/datasets/wordsforthewise/lending-club)
2. Open **DB Browser for SQLite** → New Database → name it `credit_portfolio.db`
3. Import the CSV: **File → Import → Table from CSV file** (tick "Column names in first line"). The table is named `accepted_2007_to_2018Q4` automatically
4. Open the **Execute SQL** tab and paste the contents of `queries/03_concentration_risk.sql`
5. Highlight one query at a time and press **F5**


**Hannah (Huong) Tran** |
Financial Analysis |
MSc Banking & Finance with Distinction |
CFA Levels I & II cleared

[LinkedIn](https://www.linkedin.com/in/huong-hannah/) | [GitHub](https://github.com/Hannah-Tran)
