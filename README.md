# Hospital-Dashboard
Interactive 6-page Power BI dashboard analyzing hospital operations — patient trends, doctor performance, and financial KPIs — built with DAX, Power Query, and dynamic slicers/navigation.
# 🏥 Hospital Analysis Dashboard

An interactive **6-page Power BI dashboard** that analyzes hospital operations end-to-end — patient trends, doctor performance, hospital utilization, and financial KPIs. Built entirely with **Power Query**, **DAX**, and dynamic slicers/navigation.

The dashboard is driven by a star-schema data model sourced from 15 Excel tables, and it presents actionable insights through a clean, modern UI with custom navigation, drill-through cards, and dynamic filters.


---

## 📸 Dashboard Pages

The report features a **custom navigation bar** (top center) that switches between five analytical pages plus a home/cover page.

### 1. Home
A cover page with an overview illustration and a set of clickable navigation cards (Overview, Patient, Doctor, Hospital, Finance) that describe what each page covers.

![Home](Hospital%20dashboard/Screenshots/Screenshot%202026-08-31%20162333.png)

### 2. Overview
High-level hospital KPIs at a glance:

- **Stock Status** — gauge of stock left vs. stock sold
- **Bed Status** — gauge of beds available vs. occupied
- **Recent** — latest patient rating & feedback
- **KPI cards** — Patients, Amount, Doctors, Staff count
- **Medicines** — tracking patient medicine purchases by month and weekday
- **Charges** — breakdown of room, test, other, medicine & doctor-fee charges
- **Upcoming Appointments** — next scheduled patient visits

![Overview](Hospital%20dashboard/Screenshots/Screenshot%202026-08-31%20162346.png)

### 3. Patient
Patient-centric drill-down with a selected patient profile:

- **Patient details** — doctor, patient ID, diagnosis, ratings & feedback
- **Personal & Patient information** — gender, phone, state, email, address, age, weight, department, room type, blood group
- **Admit / Discharge dates** and **Med Qty / Paid Amount** cards
- **Medicines heat-map** — purchases tracked by month and weekday
- **Charges** — categorized charge breakdown per patient
- **Medicines Bought** — quantity of each medicine the patient took

![Patient](Hospital%20dashboard/Screenshots/Screenshot%202026-08-31%20162416.png)

### 4. Doctor
Doctor performance and earnings:

- **Doctor profile** — salary, qualifications, experience
- **KPI cards** — Estimated, Patient Paid, Commission %
- **Commission Calculator** — interactive gauge and slider-driven calculator for commission % and patient amount
- **Appointments** — upcoming appointments for the doctor
- **Patients table** — patient list with suggest, status, ratings, bills, and fees

![Doctor](Hospital%20dashboard/Screenshots/Screenshot%202026-08-31%20162432.png)

### 5. Hospital
Hospital information and operational status:

- **Patient by Age Category** — age distribution bar chart
- **Patient Tests Status** — test name, notes, and status for each patient
- **Surgeries** — scheduled surgeries with dates and doctors
- **Beds Status**
- **Doctor's Appointments** — doctor, patient, reason, and appointment status

![Hospital](Hospital%20dashboard/Screenshots/Screenshot%202026-08-31%20162445.png)

### 6. Finance
Financial insights across hospital, doctor, and patient dimensions:

- **KPI cards** — Patients, Paid Amount, Avg Age, Avg Spend
- **Doctors** — Doctors Salary, Avg Doctors Salary, Doctor Commission
- **Staff** — Doctor Commission, Staff count, Salaries, Avg Staff
- **Purchase/Profit** — Purchase Price, Sell Price, Total Profit, ARMC
- **Payment method selector** — Cash / Credit Card / Insurance with a monthly trend chart
- **Charges** — surgery, room, test, other, doctor-fee, and medicine charges
- **Medicine Status** — in-stock vs. quantity sold per medicine
- **Suppliers** — quantity supplied by supplier

![Finance](Hospital%20dashboard/Screenshots/Screenshot%202026-08-31%20162501.png)

---

## 🗂️ Data Model

The report uses a **star-schema** model built from 15 Excel tables located in `Hospital dashboard/Excel Files - Direct Import/`.

### Fact / Transaction tables
| File | Table | Key columns |
|------|-------|-------------|
| `Appointment.xlsx` | Appointments | appointment_id, patient_id, doctor_id, appointment_date, status, reason, fees |
| `Hospital Bills.xlsx` | Bills | bill_id, patient_id, room_charges, surgery_charges, medicine_charges, test_charges, doctor_fees, paid_amount |
| `Patient_Tests.xlsx` | Patient Tests | patient_test_id, patient_id, test_id, doctor_id, test_date, result |
| `Surgery.xlsx` | Surgeries | appointment_id, patient_id, doctor_id, reason, fees |
| `medicine_patient.xlsx` | Medicine (Bridging) | patient_id, medicine_id, qty, date |
| `Satisfaction Score.xlsx` | Satisfaction | satisfaction_id, patient_id, doctor_id, rating, feedback |

### Dimension tables
| File | Table | Key columns |
|------|-------|-------------|
| `patient.xlsx` | Patient | patient_id, name, age, gender, blood_group, admission_date, status |
| `Doctor.xlsx` | Doctor | doctor_id, name, specialization, department, salary, qualification |
| `Department.xlsx` | Department | department_id, name, floor, head_doctor_id, total_staff |
| `Rooms.xlsx` | Rooms | room_id, department_id, room_type, daily_charge |
| `Beds.xlsx` | Beds | bed_id, room_id, status, patient_id |
| `Medical Stock.xlsx` | Medical Stock | medicine_id, name, category, cost_price, unit_price, stock_qty |
| `Medical Tests.xlsx` | Medical Tests | test_id, test_name, category, cost |
| `Staff.xlsx` | Staff | staff_id, name, department_id, role, salary, shift |
| `Supplier.xlsx` | Supplier | supplier_id, name, contact_person, city, state |

> Relationships are established on the primary/foreign keys above (e.g., `patient_id`, `doctor_id`, `medicine_id`), supporting many-to-one joins from facts to dimensions.

---

## 🛠️ Tools & Techniques

- **Power BI Desktop** — report authoring, visuals, and layout
- **Power Query (M)** — data extraction, cleaning, and transformation of the Excel source files
- **DAX** — calculated measures and columns:
  - Aggregates (Paid Amount, Total Charges, Avg Age, Avg Spend, Counts)
  - Custom measures for **Commission %**, **Total Profit**, **Stock Left / Sold**, **Bed Availability**
  - Time-intelligence over `appointment_date` / `admission_date`
- **Custom navigation & slicers** — page navigation bar, drill-through cards, and dropdown slicers (All / Cash / Credit Card / Insurance)
- **Interactive Controls** — the **Commission Calculator** on the Doctor page uses a slider + gauge driven by DAX

---

## 🚀 Getting Started

1. **Clone / download** the repository.
2. Open **`Hospital dashboard/Hospital_Dashboard-v1.pbix`** in **Power BI Desktop**.
3. Data is imported via **Direct Import** from the Excel files in `Hospital dashboard/Excel Files - Direct Import/`. If the data connection breaks, re-point the sources to your local copy of those files (Home → Transform Data → Data Source Settings).
4. Refresh the data and explore the pages via the top navigation bar.

---

## 📁 Repository Structure

```text
Hospital-Dashboard/
├── README.md                              # This file
└── Hospital dashboard/
    ├── Hospital_Dashboard-v1.pbix         # Power BI report
    ├── Excel Files - Direct Import/       # Source Excel data (15 tables)
    │   ├── Appointment.xlsx
    │   ├── Beds.xlsx
    │   ├── Department.xlsx
    │   ├── Doctor.xlsx
    │   ├── Hospital Bills.xlsx
    │   ├── Medical Stock.xlsx
    │   ├── Medical Tests.xlsx
    │   ├── Patient_Tests.xlsx
    │   ├── Rooms.xlsx
    │   ├── Satisfaction Score.xlsx
    │   ├── Staff.xlsx
    │   ├── Supplier.xlsx
    │   ├── Surgery.xlsx
    │   ├── medicine_patient.xlsx
    │   └── patient.xlsx
    ├── Images/                            # Backgrounds, doctor images, icons
    │   ├── Background Images/
    │   ├── Doctor Images/
    │   └── Icons/
    └── Screenshots/                       # Dashboard page screenshots
```

---

## 🤝 Contributing

Pull requests are welcome. If you find a bug or want to improve a visual or DAX measure, feel free to open an issue or submit a PR.

---

## 📄 License

This project is shared for learning and demonstration purposes. Please attribute the repository if you reuse or extend the dashboard.
