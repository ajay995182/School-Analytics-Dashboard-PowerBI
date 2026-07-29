# Full Build Steps – College / School Analytics Dashboard

This document explains, step by step, how this dashboard was built — useful both as documentation for this repo and as a reference if you want to rebuild it or extend it.

## Step 1 — Import all 5 tables
1. Power BI Desktop → **Get Data → Text/CSV**.
2. Import each file from the `Dataset/` folder separately: `Students.csv`, `Teachers.csv`, `Attendance.csv`, `Marks.csv`, `FeePayments.csv`.
3. **Load** each one (not combined into a single query).

## Step 2 — Clean in Power Query
1. `Attendance`: confirm the `Date` column is typed as **Date**.
2. `Marks`: add a calculated column `Percentage = MarksObtained / MaxMarks * 100`.
3. `FeePayments`: confirm `AmountDue` / `AmountPaid` are **Decimal Number**.
4. `Students`: confirm `Class` is typed as **Text** (not Whole Number) — since it's a category label (6–10), not a value to be summed.
5. Close & Apply.

## Step 3 — Build the data model (relationships)
In **Model view**, connect:
- `Students[StudentID]` → `Attendance[StudentID]` (1-to-many)
- `Students[StudentID]` → `Marks[StudentID]` (1-to-many)
- `Students[StudentID]` → `FeePayments[StudentID]` (1-to-many)
- `Teachers[TeacherID]` → `Marks[TeacherID]` (1-to-many)

This makes `Students` and `Teachers` dimension tables, and `Attendance` / `Marks` / `FeePayments` fact tables — a star schema.

## Step 4 — DAX measures
```dax
Total Students = DISTINCTCOUNT(Students[StudentID])

Attendance % =
DIVIDE(
    CALCULATE(COUNTROWS(Attendance), Attendance[Status] IN {"Present","Late"}),
    COUNTROWS(Attendance)
)

Average Marks % = AVERAGE(Marks[Percentage])

Total Fee Due = SUM(FeePayments[AmountDue])
Total Fee Collected = SUM(FeePayments[AmountPaid])
Fee Collection Rate = DIVIDE([Total Fee Collected], [Total Fee Due])

Overdue Students =
CALCULATE(DISTINCTCOUNT(FeePayments[StudentID]), FeePayments[PaymentStatus] = "Overdue")

Needs Attention Flag =
VAR LowAttendance = [Attendance %] < 0.75
VAR LowMarks = [Average Marks %] < 40
VAR HasOverdueFee =
    CALCULATE(COUNTROWS(FeePayments), FeePayments[PaymentStatus] = "Overdue") > 0
RETURN
    IF(LowAttendance || LowMarks || HasOverdueFee, "At Risk", "OK")
```

## Step 5 — Dashboard pages

**Page 1: Executive Overview**
- KPI cards: Total Students, Attendance %, Average Marks %, Fee Collection Rate
- Bar chart: Attendance % by Class
- Bar chart: Average Marks % by Class
- Donut: Fee Payment Status split

**Page 2: Academic Performance**
- Matrix: Class × Subject average marks
- Bar chart: Average Marks by Teacher
- Table: student-level performance
- Slicers: Class, Section, Exam Type

**Page 3: Attendance Analysis**
- Line chart: Attendance % trend over the sampled dates
- Bar chart: Attendance % by Section
- Scatter: Attendance % vs Average Marks % per student

**Page 4: Fee Collection**
- KPI cards: Total Due, Total Collected, Collection Rate
- Bar chart: Collection Rate by Term
- Table: overdue students
- Donut: Payment Mode split

## Step 6 — Format & polish
- Apply a consistent theme/color scheme across all 4 pages.
- Add a title bar per page.
- Double-check every table/matrix visual — text-like numeric fields (e.g. `Class`) should be set to **Don't summarize**, not Sum/Average, or you'll get meaningless totals.
- Check every page for stray empty text boxes or overlapping visuals before publishing — click around empty-looking areas near your header and slicers to catch any left over from editing.

## Step 7 — Connect to real data (optional, for a live version)
Since a real school management system already stores this exact data in MySQL:
1. Power BI → **Get Data → MySQL Database** (requires the MySQL .NET connector).
2. Point it at the live/local school database instead of the CSVs in `Dataset/`.
3. This turns the project from "sample dashboard" into "BI layer on top of a system I built" — a strong interview talking point.

## Step 8 — Publish & package
1. **File → Publish → Publish to Power BI** (free account).
2. Take screenshots of all 4 pages and drop them into `Images/` using the filenames referenced in `README.md`.
3. Push the whole folder to GitHub.
