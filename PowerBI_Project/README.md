# 📊 Power BI Sales Insights Dashboard — AdventureWorks (Full Dataset)

This project uses the full **AdventureWorks sales dataset** (2017–2020) contained in the Excel file you provided.  
The report delivers insights into revenue, product performance, territory profitability, and ordering patterns.

---

## ✅ Dataset Summary
The dataset includes:

- SalesOrderNumber  
- OrderDate  
- ProductKey  
- SalesTerritoryKey  
- EmployeeKey  
- ResellerKey  
- Quantity  
- Unit Price  
- Cost  

---

## ✅ Data Model (Star Schema)

           DimDate
                │
                │ (OrderDate)
                ▼
           ┌───────────┐
           │ FactSales │
           └───────────┘
   ▲           ▲           ▲
   │           │           │


   ProductKey   TerritoryKey   ResellerKey
│           │           │
▼           ▼           ▼
DimProduct   DimTerritory   DimReseller

## ✅ Power Query (M-code)

```m
let
    Source = Excel.Workbook(File.Contents("AdventureWorksData.xlsx"), null, true),
    Sales_Raw = Source{[Item="Sales", Kind="Sheet"]}[Data],
    Promoted = Table.PromoteHeaders(Sales_Raw, [PromoteAllScalars=true]),
    ChangedTypes = Table.TransformColumnTypes(Promoted,
        {
            {"SalesOrderNumber", type text},
            {"OrderDate", type date},
            {"ProductKey", Int64.Type},
            {"ResellerKey", Int64.Type},
            {"EmployeeKey", Int64.Type},
            {"SalesTerritoryKey", Int64.Type},
            {"Quantity", Int64.Type},
            {"Unit Price", type number},
            {"Cost", type number}
        }),
    AddedRevenue = Table.AddColumn(ChangedTypes, "Revenue", each [Quantity] * [Unit Price]),
    AddedProfit = Table.AddColumn(AddedRevenue, "Profit", each [Revenue] - ([Quantity] * [Cost])),
    Cleaned = Table.SelectRows(AddedProfit, each [Quantity] > 0 and [Unit Price] > 0)
in
    Cleaned

✅ DAX Measures

Total Revenue = SUM(FactSales[Revenue])

Total Profit = SUM(FactSales[Profit])

Total Quantity = SUM(FactSales[Quantity])

Avg Price = DIVIDE([Total Revenue], [Total Quantity])

YoY Revenue Growth =
VAR PrevYear = CALCULATE([Total Revenue], DATEADD(DimDate[Date], -1, YEAR))
RETURN DIVIDE([Total Revenue] - PrevYear, PrevYear)

Revenue by Territory = SUMX(FactSales, FactSales[Revenue])

✅ Project Files

PowerBI_Project/
│
├── AdventureWorksData.xlsx
├── README.md
├── DAX_Measures.txt
├── Data_Model.png
├── Dashboard_Page1.png
└── Dashboard_Page2.png

