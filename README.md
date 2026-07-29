# College / School Analytics Dashboard – Power BI

An interactive Power BI dashboard analyzing student performance, attendance trends, and fee collection status across a school — built with a proper relational data model (5 connected tables) rather than a single flat file, mirroring how a real school management system stores its data.

This is my **second Power BI project**, built as a natural extension of the school management systems ([SchoolHub](#) and Sri Bhavani Vidyaniketan) I've already developed in PHP/MySQL — I built the system that generates this kind of data, then built the BI layer on top of it.

---

## 📊 Dashboard Preview

### 🏠 Page 1 – Executive Overview
Total students, attendance %, average marks %, fee collection rate, attrition-style KPIs, attendance and marks by class, fee status split.

![Executive Overview](Images/ExecutiveOverview.png)

### 📚 Page 2 – Academic Performance
Class/section/exam-type filters, a class-vs-subject performance matrix, average marks by teacher, and a top-student detail table.

![Academic Performance](Images/AcademicPerformance.png)

### 📅 Page 3 – Attendance Analysis
Attendance trend over time, attendance by section, and a scatter plot correlating attendance with academic performance.

![Attendance Analysis](Images/AttendanceAnalysis.png)

### 💰 Page 4 – Fee Collection
Fee due/collected KPIs, collection rate by term, an overdue-students table, and payment mode split.

![Fee Collection](Images/FeeCollection.png)

---

## ✨ Features

**Executive Overview**
- KPI cards: Total Students, Attendance %, Average Marks %, Fee Collection Rate
- Attendance % and Average Marks % by Class (bar charts)
- Fee Payment Status split (donut chart)

**Academic Performance**
- Class / Section / Exam Type slicers
- Class × Subject performance matrix
- Average Marks by Teacher (bar chart)
- Student-level performance table

**Attendance Analysis**
- Attendance % trend over the school term (line chart)
- Attendance % by Section (bar chart)
- Attendance vs Marks correlation (scatter plot)

**Fee Collection**
- Total Due / Collected / Collection Rate (KPI cards)
- Collection Rate by Term (bar chart)
- Overdue students table
- Payment Mode split (donut chart)

---

## 🛠 Technologies Used
- Microsoft Power BI
- Power Query
- DAX (Data Analysis Expressions)
- Relational Data Modeling (star schema, 5 connected tables)
- Interactive Dashboard Design

---

## 📁 Dataset
A relational, multi-table synthetic dataset designed to mirror a real school ERP:

| Table | Rows | Description |
|---|---|---|
| `Students.csv` | 900 | Student demographics, class, section, admission year, bus usage |
| `Teachers.csv` | 90 | Teacher name, subject, class/section assignment, experience |
| `Attendance.csv` | 63,000 | Daily attendance records (Present/Absent/Late) |
| `Marks.csv` | 21,600 | Exam marks across 4 exam types and 6 subjects |
| `FeePayments.csv` | 2,700 | Term-wise fee due/paid, payment status, payment mode |

Full build steps, including the DAX measures and data model relationships, are documented in [`STEPS.md`](STEPS.md).

---

## 📈 Key Insights
- Attendance and academic performance are correlated — students with lower attendance tend to score lower on average.
- Certain sections consistently show lower attendance than others.
- A meaningful share of fee accounts fall into "Pending" or "Overdue" each term.
- Teacher-wise average marks vary, useful for identifying where extra academic support may help.

---

## 🎯 Learning Outcomes
Through this project I practiced:
- Designing a relational (star schema) data model with multiple fact and dimension tables
- Writing DAX measures across related tables
- Power Query data cleaning and transformation
- Multi-page interactive dashboard design
- Business intelligence reporting for a real-world domain (education / HR-adjacent)

---

## 📁 Repository Structure
```
School-Analytics-Dashboard-PowerBI/
│
├── Dashboard.pbix
├── README.md
├── STEPS.md
├── Dataset/
│   ├── Students.csv
│   ├── Teachers.csv
│   ├── Attendance.csv
│   ├── Marks.csv
│   └── FeePayments.csv
├── Images/
│   ├── ExecutiveOverview.png
│   ├── AcademicPerformance.png
│   ├── AttendanceAnalysis.png
│   └── FeeCollection.png
└── LICENSE
```

---

## 🚀 How to Use
1. Download `Dashboard.pbix`.
2. Open it in [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free).
3. Explore all 4 report pages using the slicers, or connect it to your own MySQL school database as described in `STEPS.md`.

---

## 📬 Contact
If you have suggestions or feedback, feel free to connect with me on LinkedIn.

⭐ If you like this project, don't forget to star this repository.
