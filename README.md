# ✈️ Airline Delay Analysis — Flight Intelligence Dashboard
 
<div align="center">
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-Measures-6366F1?style=for-the-badge)
![Schema](https://img.shields.io/badge/Schema-Star%20Schema-0EA5E9?style=for-the-badge)
![Pages](https://img.shields.io/badge/Dashboard%20Pages-3-22C55E?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-16a34a?style=for-the-badge)
 
<br/>
> **An end-to-end flight delay analytics solution — from raw data cleaning in Python to an interactive 3-page Power BI dashboard — uncovering delay patterns across 2M+ flights, 20+ airlines, and thousands of US routes.**
 
</div>
---
 
## 🗂️ Table of Contents
 
- [Project Overview](#-project-overview)
- [Project Workflow](#-project-workflow)
- [Dashboard Pages](#-dashboard-pages)
- [Data Model](#-data-model)
- [DAX Measures](#-dax-measures)
- [Key KPIs at a Glance](#-key-kpis-at-a-glance)
- [Tools & Technologies](#-tools--technologies)
- [Project Structure](#-project-structure)
- [How to Use](#-how-to-use)
---
 
## 🎯 Project Overview
 
This project analyzes **US domestic flight delays** to help airlines and operations teams understand:
 
- 📅 **When** delays are highest (by month, day of week)
- 🏢 **Which carriers** cause the most delays
- 📍 **Which cities and routes** are the worst performers
- 🌦️ **What causes** delays (carrier, weather, NAS, late aircraft)
| Feature | Details |
|---|---|
| 📁 Power BI File | `النسخة.pbix` |
| 🐍 Python Notebook | `Data_Cleaning_Airline.ipynb` |
| 📄 Dashboard Pages | 3 Interactive Pages |
| 🗃️ Schema | Star Schema |
| ✈️ Total Flights | 2,000,000+ |
| 🛫 Unique Routes | 7,498 |
| 🏢 Airlines Covered | 20+ US Carriers |
 
---
 
## 🔄 Project Workflow
 
```
Raw CSV Data
     │
     ▼
┌─────────────────────────────┐
│  🐍 Python — Jupyter        │
│  Data_Cleaning_Airline.ipynb│
│  • Remove nulls & duplicates│
│  • Fix data types           │
│  • Feature engineering      │
│  • Export clean CSV         │
└────────────┬────────────────┘
             │
             ▼
┌─────────────────────────────┐
│  📊 Power BI Desktop        │
│  • Load cleaned data        │
│  • Build Star Schema        │
│  • Write DAX measures       │
│  • Design 3-page dashboard  │
└─────────────────────────────┘
```
 
---
 
## 📑 Dashboard Pages
 
---
 
### 1️⃣ OverView
> *High-level summary of all flight operations*
 
| KPI | Value |
|---|---|
| ✈️ Total Flights | **2M** |
| ⏰ Delayed Flights % | **65.86%** |
| 🛫 AVG Departure Delay | **43.09 min** |
| 🛬 AVG Arrival Delay | **42.20 min** |
| 🗺️ Unique Flight Routes | **7,498** |
 
**Visuals:**
- 📈 **Line Chart** — Avg Departure & Arrival Delay by Month (seasonality trend)
- 📉 **Area Chart** — Delayed Flights % by Day of Week
- 📊 **Bar Chart** — Total Flights by Carrier Name (Southwest leads with 0.38M)
**Slicers:** Month · Day · Carrier
 
---
 
### 2️⃣ Delay Analysis
> *Root cause breakdown of delay types across carriers and cities*
 
| KPI | Value |
|---|---|
| 🏢 AVG Carrier Delay | **12.41 min** |
| 🌦️ AVG Weather Delay | **2.40 min** |
| 🏛️ AVG NAS Delay | **9.72 min** |
| ✈️ AVG Late Aircraft Delay | **16.36 min** |
| 🔁 Recovered Flights % | **2.04%** |
 
**Visuals:**
- 📊 **Stacked Bar Chart** — All 4 delay types by Month
- 📊 **Bar Chart** — Avg Carrier Delay by Airline (Mesa Air tops at 29 min)
- 🗺️ **Treemap** — Top 10 Cities by Total Delay Minutes (Chicago leads at 7M)
- 🎯 **Gauge Chart** — Delayed Flights % vs Min/Max/Target thresholds
**Key Insight:** Late Aircraft is the #1 delay cause (16.36 min avg), followed by Carrier delays (12.41 min).
 
---
 
### 3️⃣ Route & Airport
> *Geographic and route-level performance analysis*
 
| KPI | Value |
|---|---|
| ✈️ Flights to Airport | **2M** |
| 📏 Min Distance | **11 miles** |
| 📏 Max Distance | **4,962 miles** |
| 💨 AVG Speed | **7.06** |
| 🛬 AVG Arrival Delay by Dest | **42.20 min** |
 
**Visuals:**
- 🔵 **Scatter Plot** — Departure vs Arrival Delay by Carrier (bubble size = total flights)
- 📊 **Bar Chart** — Avg Departure Delay by Origin City (Hancock tops at 116 min)
- 📊 **Bar Chart** — Avg Arrival Delay by Destination City (Hancock leads at 123 min)
- 📋 **Detail Table** — Route-level: Origin → Destination · Flights · Avg Departure Delay · Avg Arrival Delay
---
 
## 🗃️ Data Model
 
The project uses a clean **Star Schema** with one central fact table surrounded by 4 dimension tables.
 
```
                    ┌───────────────┐
                    │   Dim_Date    │
                    │  Date         │
                    │  DateKey      │
                    │  Day, Month   │
                    │  DayName      │
                    │  MonthName    │
                    │  Year         │
                    └──────┬────────┘
                           │ 1
                           │
┌──────────────────┐       │        ┌─────────────────────┐
│ Dim_Origin_      │  *    ▼  *     │ Dim_Destination_    │
│ Airport          ├───►Fact_Flights◄┤ Airport             │
│                  │               │                     │
│ AirportCode      │               │ AirportCode         │
│ AirportKey       │               │ AirportKey          │
│ AirportName      │               │ AirportName         │
│ Origin_City      │               │ Destination_City    │
└──────────────────┘               └─────────────────────┘
                           │ *
                           │
                    ┌──────┴────────┐
                    │  Dim_Carrier  │
                    │  CarrierKey   │
                    │  CarrierName  │
                    │  UniqueCarrier│
                    └───────────────┘
```
 
### Fact Table — `Fact_Flights`
 
| Column | Description |
|---|---|
| `DateKey` | FK → Dim_Date |
| `OriginKey` | FK → Dim_Origin_Airport |
| `DestKey` | FK → Dim_Destination_Airport |
| `CarrierKey` | FK → Dim_Carrier |
| `Departure_Delay` | Minutes of departure delay |
| `Arrival_Delay` | Minutes of arrival delay |
| `CarrierDelay` | Delay caused by the carrier |
| `WeatherDelay` | Delay caused by weather |
| `NASDelay` | National Air System delay |
| `LateAircraftDelay` | Previous flight late arrival |
| `SecurityDelay` | Security-related delay |
| `Distance` | Route distance in miles |
| `AirTime` | Actual time in air |
| `TaxiIn / TaxiOut` | Ground taxi times |
| `FlightNum` | Flight number |
| `TailNum` | Aircraft identifier |
 
---
 
## 📐 DAX Measures
 
All measures are stored in the dedicated **`#KPIs`** table:
 
```
📁 #KPIs
├── ✈️  Total Flights
├── 🗺️  Unique Flight Routes
├── 🛫  Avg Departure Delay
├── 🛬  Avg Arrival Delay
├── 🛬  Avg Arrival Delay By Dest
├── ⏰  Delayed Flights %
├── 🏢  Avg Carrier Delay
├── 🌦️  Avg Weather Delay
├── 🏛️  Avg NAS Delay
├── ✈️  Avg LateAircraft Delay
├── 🔒  Avg Security Delay
├── 💨  Avg Speed
├── 🔁  Recovered Flights %
├── 🏙️  Top Delay Cause
├── ⏱️  Total Delay Minutes
├── 🛩️  Unique Aircraft
├── 📏  Min Distance
├── 📏  Max Distance
├── 🎯  Target Value
├── ⬆️  Max Value
└── ⬇️  Min Value
```
 
---
 
## 📊 Key KPIs at a Glance
 
```
┌──────────────────────────────────────────────────────────┐
│                  FLIGHT SUMMARY                          │
├──────────────────────┬───────────────────────────────────┤
│  ✈️ Total Flights    │  2,000,000+                       │
│  ⏰ Delayed Flights  │  65.86% of all flights            │
│  🛫 Avg Dep. Delay   │  43.09 minutes                    │
│  🛬 Avg Arr. Delay   │  42.20 minutes                    │
│  🗺️ Unique Routes    │  7,498 routes                     │
├──────────────────────┼───────────────────────────────────┤
│  🏢 Carrier Delay    │  12.41 min  (2nd cause)           │
│  🌦️ Weather Delay    │  2.40 min   (smallest cause)      │
│  🏛️ NAS Delay        │  9.72 min                         │
│  ✈️ Late Aircraft    │  16.36 min  (top cause ⚠️)        │
│  🔁 Recovered Flights│  2.04%                            │
├──────────────────────┼───────────────────────────────────┤
│  📏 Min Route        │  11 miles                         │
│  📏 Max Route        │  4,962 miles                      │
└──────────────────────┴───────────────────────────────────┘
```
 
**🏆 Top Delayed Carrier:** Mesa Air (29 min avg carrier delay)  
**🏆 Most Flights:** Southwest Airlines (0.38M flights)  
**🏆 Most Delayed City:** Chicago (7M total delay minutes)  
**🏆 Most Delayed Origin:** Hancock Airport (116 min avg departure delay)  
**📅 Worst Delay Month:** Summer months (June–August peak)  
**📅 Worst Delay Day:** Thursday & Friday
 
---
 
## 🛠️ Tools & Technologies
 
| Tool | Usage |
|---|---|
| ![Python](https://img.shields.io/badge/-Python-3776AB?logo=python&logoColor=white&style=flat-square) | Data cleaning & preprocessing |
| ![Pandas](https://img.shields.io/badge/-Pandas-150458?logo=pandas&logoColor=white&style=flat-square) | Data wrangling in Jupyter Notebook |
| ![Power BI](https://img.shields.io/badge/-Power%20BI-F2C811?logo=powerbi&logoColor=black&style=flat-square) | Dashboard design & publishing |
| ![DAX](https://img.shields.io/badge/-DAX-6366F1?style=flat-square) | KPI measures & calculations |
| ![Power Query](https://img.shields.io/badge/-Power%20Query-0EA5E9?style=flat-square) | Data loading & transformation |
| ![Star Schema](https://img.shields.io/badge/-Star%20Schema-64748b?style=flat-square) | Relational data modeling |
 
---
 
## 📁 Project Structure
 
```
📦 Airline-Delay-Analysis/
├── 📊 النسخة.pbix                     ← Power BI dashboard file
├── 🐍 Data_Cleaning_Airline.ipynb     ← Python data cleaning notebook
├── 📸 screenshots/
│   ├── 01_Overview.png
│   ├── 02_Delay_Analysis.png
│   ├── 03_Route_Airport.png
│   └── 04_Data_Model.png
└── 📄 README.md
```
 
---
 
## 🚀 How to Use
 
### Power BI Dashboard
1. Download `النسخة.pbix`
2. Open in **Power BI Desktop** (2023 or later)
3. Use the **left sidebar** to switch between the 3 pages
4. Use the **slicers** (Month · Day · Carrier) to filter the data interactively
### Python Notebook
1. Make sure you have Python installed with: `pandas`, `numpy`, `matplotlib`
2. Open `Data_Cleaning_Airline.ipynb` in **Jupyter Notebook** or **VS Code**
3. Run all cells to reproduce the data cleaning pipeline
```bash
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook Data_Cleaning_Airline.ipynb
```
 
---
 
## 👤 About the Author
 
**Abd Elfatah Gaber Ebrahim**
Data Analysis Student · ITI (Information Technology Institute) · Egypt 🇪🇬
 
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Abd%20Elfatah%20Gaber-0A66C2?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/abd-elfatah-gaber-ebrahim/)
[![GitHub](https://img.shields.io/badge/GitHub-abd--elfatah--gaber-181717?style=for-the-badge&logo=github)](https://github.com/abd-elfatah-gaber)
[![Mostaql](https://img.shields.io/badge/Mostaql-Abdelfatah26-1abc9c?style=for-the-badge)](https://mostaql.com/u/Abdelfatah26)
[![Khamsat](https://img.shields.io/badge/Khamsat-abd__elfatah__gaber26-e67e22?style=for-the-badge)](https://khamsat.com/user/abd_elfatah_gaber26)
 
---
 
<div align="center">
⭐ **If you found this project useful, please consider giving it a star!** ⭐
 
*Built with ❤️ using Python & Power BI*
 
</div>
 
