# 🧮 Handling Numerical Missing Values — Mean, Median, and Arbitrary Imputation

**📘 AI-Generated README (Custom prompt used for clarity and learning ease)**  

---

## 📌 Overview  
This experiment focuses on **handling missing numerical values** using three main techniques — **Mean Imputation**, **Median Imputation**, and **Arbitrary Value Imputation**.  
The dataset used is located in the repository (Titanic dataset).

---

## 🧰 Libraries Used  
- **NumPy** — numerical operations  
- **Pandas** — data cleaning and manipulation  
- **Matplotlib / Seaborn** — visualization  
- **Scikit-learn** — imputation utilities  

---

## 📂 Dataset Details  
- The dataset contains two key numerical columns with missing values:  
  - `Age` → **19% missing values**  
  - `Fare` → **0.05% missing values**  
- The data was split into **training** and **testing** sets before applying imputations.

---

## 🧠 Step-by-Step Process

### 1. Mean and Median Imputation  
- Calculated **mean** and **median** for both `Age` and `Fare`.  
- Created two new columns each — one filled using **mean** and one using **median**.  
- Variance comparison showed:
  - Variance **decreased** after imputation in both columns.  
  - Indicates that extreme values were smoothed out.

#### 🟢 KDE Visualization  
- *<img width="576" height="413" alt="num1" src="https://github.com/user-attachments/assets/3c93c12e-6fbf-4df1-8e36-60a5accb8376" />
:* KDE plot of `Age`, `Age_Median`, and `Age_Mean`.  
  - Slight change for median (less distortion).  
  - Mean imputation caused a **larger shift** due to higher percentage of missing values.  
- *<img width="598" height="413" alt="num2" src="https://github.com/user-attachments/assets/e29e27b4-c92c-4b0b-9cc3-94089bded4b9" />
:* KDE plot for `Fare` shows **almost identical curves** — fewer missing values led to minimal change.  

#### 🟢 Covariance Analysis  
- Covariance values slightly changed after imputation — as expected when replacing missing entries.  

#### 🟢 Box Plot Visualization  
- *<img width="543" height="413" alt="num3" src="https://github.com/user-attachments/assets/29fb65be-cbf8-4ccf-b991-94e8e00d5952" />
:* `Age` boxplot shows **increased outliers** after mean/median imputation.  
- *<img width="552" height="413" alt="num4" src="https://github.com/user-attachments/assets/d894359c-b965-4f08-9f18-c11243bbba5c" />
:* `Fare` boxplot remained almost unchanged due to negligible missingness.  

---

### 2. Using `SimpleImputer` from scikit-learn  
- Created two imputers using `strategy='mean'` and `strategy='median'`.  
- Applied via `ColumnTransformer` for automation.  
- Verified that imputer statistics matched manually calculated values.  
- Output remained consistent with manual imputation results.

---

### 3. Arbitrary Value Imputation  
- Since no one can realistically have **99 years** or **-1 fare**, arbitrary imputation was tested using 99 and -1.  
- Filled missing values with **99** and **-1** for both columns.  
- Observed that:
  - Variance **increased significantly**.  
  - Distribution became distorted.  
  - Covariance changed drastically.  

#### 🔴 KDE and Box Plot Visuals  
- *<img width="584" height="413" alt="num5" src="https://github.com/user-attachments/assets/4d572e67-a139-40f6-9971-fc83080d0b65" />
* KDE plot of `Age`, `Age_99`, and `Age_-1` — messy, distorted distribution.  
- *<img width="593" height="413" alt="num6" src="https://github.com/user-attachments/assets/095c631e-9d3f-411c-959a-16b29f2eb773" />
* KDE plot of `Fare` after arbitrary fill — similarly distorted and unrealistic.

#### ⚙️ Automated Arbitrary Imputation  
- Used `SimpleImputer(strategy='constant', fill_value=9)` within `ColumnTransformer`.  
- Produced identical results as manual arbitrary fill.

---

## 🧩 Comparison Summary

| Method | Variance Change | Distribution Effect | Best Used When |
|---------|----------------|---------------------|----------------|
| Mean Imputation | Decreases variance | Distorts if many missing values | Small % of missing data |
| Median Imputation | Slightly decreases variance | Maintains shape | Data has outliers |
| Arbitrary Imputation | Increases variance | Distorts heavily | For **flagging** missing data only |

---

## 🧠 Key Insights  
- **Median Imputation** performed best, preserving distribution even with missing values.  
- **Mean Imputation** works but can distort data if many values are missing.  
- **Arbitrary Imputation** should not be used for analysis — only to mark missing entries.  
- Automated tools like **`SimpleImputer`** simplify this process while ensuring consistency.

---

📎 *Note: This README was AI-generated using a custom prompt for educational and clarity purposes.*
