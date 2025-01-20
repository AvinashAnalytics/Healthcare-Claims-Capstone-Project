# 🌟 **Healthcare Claims Capstone Project** 🌟

## 🔍 **Overview**

This capstone project focuses on analyzing **healthcare claims data** to extract actionable insights. The project simulates real-world scenarios in the healthcare domain and involves various phases such as **data extraction**, **SQL analysis**, and **data visualization** using **Power BI/Tableau**. The ultimate goal is to provide deeper insights into healthcare claims, **beneficiary demographics**, and **provider performance** to enable better decision-making.

**Project Objectives**:
- 🎯 **Data Extraction**: Extract key insights using **SQL**.
- 📊 **Data Visualization**: Create interactive dashboards using **Power BI** or **Tableau**.
- 🏥 **Healthcare Insights**: Understand trends, demographics, and provider performance in healthcare claims.

---

## 🛠️ **Phase 1: SQL Analysis – Healthcare Claims Data**

### **Objective:**
In this phase, we perform SQL queries on healthcare claims data to generate reports and valuable insights that will aid decision-making processes.

### **SQL Queries:**

1. **💸 Claims Analysis**  
   Analyze the total reimbursement amounts for inpatient claims grouped by the provider.
   ```sql
   SELECT 
       Provider,
       SUM(InscClaimAmtReimbursed) AS TotalAmountReimbursed
   FROM
       in_patient_data
   GROUP BY Provider
   ORDER BY TotalAmountReimbursed DESC;
   ```

2. **👨‍⚕️ Provider Insights**  
   Identify the top 5 providers with the highest number of outpatient claims.
   ```sql
   SELECT 
       Provider, COUNT(*) AS TotalClaims
   FROM
       out_patient_data
   GROUP BY Provider
   ORDER BY TotalClaims DESC
   LIMIT 5;
   ```

3. **🩺 Chronic Conditions**  
   Count the beneficiaries with claims related to chronic conditions like diabetes.
   ```sql
   SELECT 
       COUNT(*) AS TotalCount
   FROM
       beneficiary_data
   WHERE
       ChronicCond_Diabetes = 1;
   ```

4. **⚖️ Gender-Based Analysis**  
   Calculate the average inpatient claim amount reimbursed for each gender.
   ```sql
   SELECT 
       b.gender,
       AVG(i.InscClaimAmtReimbursed) AS AverageReimbursed
   FROM
       beneficiary_data b
       LEFT JOIN in_patient_data i ON b.BeneID = i.BeneID
   GROUP BY b.gender;
   ```

5. **📝 Beneficiary History**  
   Retrieve all claims for a specific BeneID to analyze their history.
   ```sql
   SELECT 
       BeneID, ClaimID, ClaimStartDt, ClaimEndDt, Provider, InscClaimAmtReimbursed 
   FROM
       in_patient_data
   WHERE
       BeneID = 'BENE21203' 
   UNION 
   SELECT 
       BeneID, ClaimID, ClaimStartDt, ClaimEndDt, Provider, InscClaimAmtReimbursed
   FROM
       out_patient_data
   WHERE
       BeneID = 'BENE21203';
   ```

6. **💰 High-Value Claims**  
   Identify providers where claims' admission dates are in 2009 and the reimbursed amount exceeds $10,000.
   ```sql
   SELECT 
       Provider, AdmissionDt, InscClaimAmtReimbursed
   FROM
       in_patient_data
   WHERE
       YEAR(AdmissionDt) = 2009
           AND InscClaimAmtReimbursed > 10000;
   ```

7. **👵 Demographic Analysis**  
   Calculate the average deductible amount for beneficiaries aged 65 and older.
   ```sql
   SELECT 
       AVG(IPAnnualDeductibleAmt) AS Avg_Deductible
   FROM
       in_patient_data i
       JOIN beneficiary_data b ON i.BeneID = b.BeneID
   WHERE
       TIMESTAMPDIFF(YEAR, b.DOB, CURDATE()) >= 65;
   ```

8. **👩‍⚕️ Physician Involvement**  
   List all claims involving more than one physician.
   ```sql
   SELECT 
       BeneID, ClaimID, ClaimStartDt, ClaimEndDt, Provider, InscClaimAmtReimbursed,
       AttendingPhysician, OperatingPhysician, OtherPhysician
   FROM
       in_patient_data
   WHERE
       (AttendingPhysician IS NOT NULL AND OperatingPhysician IS NOT NULL)
       OR (AttendingPhysician IS NOT NULL AND OtherPhysician IS NOT NULL)
       OR (OperatingPhysician IS NOT NULL AND OtherPhysician IS NOT NULL);
   ```

---

### **SQL Resources**:
- 📝 [SQL Queries File](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/sql/SQL-Project-File.sql)
- 📄 [SQL Insights Report](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/reports/SQL-Analysis-Insights-Report.docx)

---

## 📊 **Phase 2: Dashboard Creation – Power BI**

### **Objective:**
In Phase 2, we create **interactive dashboards** to visualize the healthcare claims data, making it easier for stakeholders to understand and make data-driven decisions.

---

### **Dashboard Pages:**

1. **🏠 Home Page**  
   - **Visuals**: Overview of total reimbursement and claims distribution.
   - **KPIs**: Total Claims, Average Claim Amount.  
   ![Home Page](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/dashboards/Dashboard-Images/Home%20Page.png)

2. **💼 Claims Overview**  
   - **Visuals**: Breakdown of claims by provider and reimbursement.
   - **KPIs**: Total Claims, Average Claim Amount.  
   ![Claims Overview](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/dashboards/Dashboard-Images/Page%201%20-%20Claims%20Overview.png)

3. **🩺 Provider Analysis**  
   - **Visuals**: Insights on top 5 providers and claims related to them.
   - **KPIs**: Number of Providers, Total Reimbursement.  
   ![Provider Analysis](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/dashboards/Dashboard-Images/Page%202%20-%20%20Provider%20Analysis.png)

4. **👩‍👩‍👧 Demographic Insights**  
   - **Visuals**: Demographic breakdown (gender, age, and race) and chronic conditions.
   - **KPIs**: Number of Beneficiaries, Average Deductible.  
   ![Demographic Insights](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/dashboards/Dashboard-Images/Page%203%20-%20Demographic%20Insights.png)

5. **📈 Trends Over Time**  
   - **Visuals**: Claims and reimbursement trends over time (monthly/quarterly).
   - **KPIs**: Average Claim Amount.  
   ![Trends Over Time](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/dashboards/Dashboard-Images/Page%204%20-%20%20Trends%20Over%20Time.png)

---

### **Power BI Resources**:
- 📊 [Power BI Project File](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/dashboards/HealthCare-Claims-Project-PowerBI.pbix)
- 📄 [Dashboard Insights Report](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/reports/Dashboard-Insights-Report.docx)
- 🧹 [Data Cleaning Process](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/reports/Data-Cleaning-Process.docx)

---

## 🏁 **Final Deliverables**

- 🎤 **Presentation PDF**: [Healthcare Claims Project PDF](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/reports/Healthcare-Claims-Project-PDF.pdf)

---

## 🚀 **Conclusion**

This project offers an in-depth analysis of **healthcare claims data**, providing insights into **provider performance**, **demographics**, and **health trends**. By using **SQL analysis** and **interactive dashboards**, this capstone project empowers stakeholders to make more informed decisions in the healthcare industry. 

**Key Takeaways**:
- ✨ Actionable insights through SQL.
- 🎨 Powerful visualizations for easy decision-making.
- 💡 Data-driven conclusions that contribute to more efficient healthcare systems.

---

### 🔗 **Useful Links**:
- [Project Repository](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project)
- [SQL Queries File](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/sql/SQL-Project-File.sql)
- [Power BI Project File](https://github.com/AvinashAnalytics/Healthcare-Claims-Capstone-Project/blob/main/dashboards/HealthCare-Claims-Project-PowerBI.pbix)

---

## 📊 **About Me**

I’m a passionate **Data Analyst** with a background in **Mathematics**, focusing on turning complex data into actionable insights. I specialize in using tools like **Python**, **SQL**, and **Tableau** to solve real-world business problems, uncover trends, and create data-driven strategies. My goal is to help businesses leverage the power of data for smarter decision-making.

---

## 📫 **Contact Me**

I’m always open to discussing data projects and collaboration opportunities. Feel free to reach out:

- **Email:** [masteravinashrai@gmail.com](mailto:masteravinashrai@gmail.com)
- **LinkedIn:** [Avinash Analytics](https://www.linkedin.com/in/avinashanalytics/)
- **HackerRank:** [AvinashAnalytics](https://www.hackerrank.com/AvinashAnalytics)
- **Twitter (X):** [@AvinashAnalytiX](https://x.com/AvinashAnalytiX)

---
