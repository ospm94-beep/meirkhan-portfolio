# 🛒 Walmart Sales Analysis — Power BI Project

This Power BI project analyzes **Walmart weekly sales** across multiple stores (2010–2012).  
It uncovers valuable insights including:

✅ Store performance ranking  
✅ Weekly & yearly sales trends  
✅ Holiday vs Non-Holiday sales lift  
✅ Seasonality & week-level patterns  
✅ Interactive drill-down analysis with slicers  
✅ Dynamic KPIs and DAX measures

---

# 📂 Project Files Included

- **Walmart_Sales_Analysis.pbix** — Full Power BI report  
- **Walmart_Sales.csv** — Original dataset  
- **Executive_Summary.png** — Screenshot of Page 1  
- **Store_Performance.png** — Screenshot of Page 2  
- **Holiday_Analysis.png** — Screenshot of Page 3  

---

# 📊 Dashboard Pages

### ✅ **1. Executive Summary**
- Total Sales  
- Avg Weekly Sales  
- YoY Growth %  
- Holiday Sales  
- Sales trend  
- Store ranking  
- Holiday vs Non-Holiday comparison  

### ✅ **2. Store Performance**
- Store-level KPIs  
- Store sales trend over time  
- Weekly seasonality  
- Store ranking table  

### ✅ **3. Holiday Analysis**
- Holiday Lift %  
- Holiday week performance  
- Holiday vs Non-Holiday trend  
- Seasonal heatmap  
- Holiday sales by store  

---

# 🧠 Insights

- Holiday weeks deliver **substantially higher sales** compared to non-holiday weeks.  
- Sales consistently spike in **weeks 47–52** every year (strong seasonality).  
- Certain stores generate a disproportionate share of total revenue.  
- Year-over-year growth from 2010 → 2011 is visible, followed by stabilization.  

---

# 🛠️ Tools Used

- Power BI Desktop  
- Power Query  
- DAX  
- CSV data  
- GitHub for documentation & version control  

---

# 🔧 Key DAX Measures (Sample)

```DAX
Total Sales = SUM(Walmart_Sales[Weekly_Sales])

Holiday Sales =
CALCULATE([Total Sales], Walmart_Sales[Holiday_Flag] = 1)

YoY Growth % =
DIVIDE([Total Sales] - [Previous Year Sales], [Previous Year Sales])
