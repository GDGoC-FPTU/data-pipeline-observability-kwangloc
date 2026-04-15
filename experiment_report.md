# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600333
**Name:** Truong Quang Loc
**Date:** 15/4/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200. | 10 | Correct and useful recommendation |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Technically executed, but the answer is absurd and misleading |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

(Hay phan tich cac van de nhu Duplicate IDs, wrong data types, outliers, null values
va giai thich tai sao chung anh huong den ket qua cua Agent.)

Agent didn't give the wrong answer, agent was given wrong knowledge.

> - **Outlier** (`price=999999`): no range check
> - **Wrong type** (`price="ten dollars"`): silently poisons numeric operations
> - **Duplicate ID** (`id=1` x2): corrupts any downstream count or join
> - **Null fields** (empty `id`/`category`): ghost rows that surface anywhere.

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

Yes. Garbage in, garbage out
