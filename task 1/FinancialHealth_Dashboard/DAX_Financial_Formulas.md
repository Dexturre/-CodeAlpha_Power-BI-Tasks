# DAX Financial Formulas Reference Guide

## Core Financial Metrics

### Revenue Analysis
```dax
Total Revenue = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Type] = "Income"
)

Revenue MTD = 
CALCULATE(
    [Total Revenue],
    DATESMTD('DateTable'[Date])
)

Revenue YTD = 
CALCULATE(
    [Total Revenue],
    DATESYTD('DateTable'[Date])
)

Revenue QTD = 
CALCULATE(
    [Total Revenue],
    DATESQTD('DateTable'[Date])
)

Revenue Previous Period = 
CALCULATE(
    [Total Revenue],
    DATEADD('DateTable'[Date], -1, MONTH)
)

Revenue Growth % = 
DIVIDE(
    [Total Revenue] - [Revenue Previous Period],
    [Revenue Previous Period],
    0
)
```

### Expense Analysis
```dax
Total Expenses = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Type] = "Expense"
)

COGS = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Category] = "COGS"
)

Operating Expenses = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Category] = "Operating Expenses"
)

Expense by Category = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Type] = "Expense",
    VALUES(FinancialData[Category])
)
```

### Profitability Measures
```dax
Gross Profit = [Total Revenue] - [COGS]

Operating Profit = [Gross Profit] - [Operating Expenses]

Net Profit = [Total Revenue] - [Total Expenses]

Gross Profit Margin = 
DIVIDE(
    [Gross Profit],
    [Total Revenue],
    0
)

Operating Profit Margin = 
DIVIDE(
    [Operating Profit],
    [Total Revenue],
    0
)

Net Profit Margin = 
DIVIDE(
    [Net Profit],
    [Total Revenue],
    0
)
```

## Balance Sheet Metrics

### Asset Analysis
```dax
Total Assets = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Type] = "Asset"
)

Current Assets = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Type] = "Asset",
    FinancialData[Category] IN {"Cash", "Accounts Receivable", "Inventory"}
)

Fixed Assets = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Type] = "Asset",
    FinancialData[Category] = "Fixed Assets"
)
```

### Liability Analysis
```dax
Total Liabilities = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Type] = "Liability"
)

Current Liabilities = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Type] = "Liability",
    FinancialData[Category] = "Accounts Payable"
)

Long-term Liabilities = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Type] = "Liability",
    FinancialData[Category] = "Loans"
)
```

### Equity Analysis
```dax
Total Equity = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Type] = "Equity"
)

Retained Earnings = 
CALCULATE(
    SUM(FinancialData[Amount]),
    FinancialData[Type] = "Equity",
    FinancialData[Account] = "Retained Earnings"
)
```

## Financial Ratios

### Liquidity Ratios
```dax
Current Ratio = 
DIVIDE(
    [Current Assets],
    [Current Liabilities],
    0
)

Quick Ratio = 
DIVIDE(
    [Current Assets] - CALCULATE(SUM(FinancialData[Amount]), FinancialData[Account] = "Inventory"),
    [Current Liabilities],
    0
)

Cash Ratio = 
DIVIDE(
    CALCULATE(SUM(FinancialData[Amount]), FinancialData[Account] = "Cash"),
    [Current Liabilities],
    0
)
```

### Solvency Ratios
```dax
Debt to Equity Ratio = 
DIVIDE(
    [Total Liabilities],
    [Total Equity],
    0
)

Debt to Assets Ratio = 
DIVIDE(
    [Total Liabilities],
    [Total Assets],
    0
)

Equity Ratio = 
DIVIDE(
    [Total Equity],
    [Total Assets],
    0
)
```

### Profitability Ratios
```dax
Return on Assets (ROA) = 
DIVIDE(
    [Net Profit],
    [Total Assets],
    0
)

Return on Equity (ROE) = 
DIVIDE(
    [Net Profit],
    [Total Equity],
    0
)

Return on Investment (ROI) = 
DIVIDE(
    [Net Profit],
    [Total Assets] - [Current Liabilities],
    0
)
```

### Efficiency Ratios
```dax
Asset Turnover = 
DIVIDE(
    [Total Revenue],
    [Total Assets],
    0
)

Inventory Turnover = 
DIVIDE(
    [COGS],
    CALCULATE(SUM(FinancialData[Amount]), FinancialData[Account] = "Inventory"),
    0
)

Receivables Turnover = 
DIVIDE(
    [Total Revenue],
    CALCULATE(SUM(FinancialData[Amount]), FinancialData[Account] = "Accounts Receivable"),
    0
)
```

## Budget vs Actual Analysis

```dax
Budget Revenue = 
CALCULATE(
    SUM(BudgetData[Budget]),
    BudgetData[Type] = "Income"
)

Actual Revenue = 
CALCULATE(
    SUM(BudgetData[Actual]),
    BudgetData[Type] = "Income"
)

Revenue Variance = [Actual Revenue] - [Budget Revenue]

Revenue Variance % = 
DIVIDE(
    [Revenue Variance],
    [Budget Revenue],
    0
)

Budget Expenses = 
CALCULATE(
    SUM(BudgetData[Budget]),
    BudgetData[Type] = "Expense"
)

Actual Expenses = 
CALCULATE(
    SUM(BudgetData[Actual]),
    BudgetData[Type] = "Expense"
)

Expense Variance = [Actual Expenses] - [Budget Expenses]

Expense Variance % = 
DIVIDE(
    [Expense Variance],
    [Budget Expenses],
    0
)
```

## Forecasting Measures

### Time Series Forecasting
```dax
3 Month Moving Average = 
AVERAGEX(
    DATESINPERIOD(
        'DateTable'[Date],
        LASTDATE('DateTable'[Date]),
        -3,
        MONTH
    ),
    [Total Revenue]
)

6 Month Moving Average = 
AVERAGEX(
    DATESINPERIOD(
        'DateTable'[Date],
        LASTDATE('DateTable'[Date]),
        -6,
        MONTH
    ),
    [Total Revenue]
)

12 Month Moving Average = 
AVERAGEX(
    DATESINPERIOD(
        'DateTable'[Date],
        LASTDATE('DateTable'[Date]),
        -12,
        MONTH
    ),
    [Total Revenue]
)
```

### Growth Rate Calculations
```dax
Monthly Growth Rate = 
VAR CurrentRevenue = [Total Revenue]
VAR PreviousRevenue = 
    CALCULATE(
        [Total Revenue],
        DATEADD('DateTable'[Date], -1, MONTH)
    )
RETURN
DIVIDE(
    CurrentRevenue - PreviousRevenue,
    PreviousRevenue,
    0
)

Compound Monthly Growth Rate (CMGR) = 
POWER(
    (1 + [Monthly Growth Rate]),
    12
) - 1
```

### Trend Analysis
```dax
Linear Trend Forecast = 
VAR LastDate = MAX('DateTable'[Date])
VAR DaysInFuture = DATEDIFF(LastDate, MAX('DateTable'[Date]), DAY)
VAR AvgDailyRevenue = 
    AVERAGEX(
        SUMMARIZE(
            FinancialData,
            FinancialData[Date],
            "DailyRevenue", [Total Revenue]
        ),
        [DailyRevenue]
    )
RETURN
[Total Revenue] + (DaysInFuture * AvgDailyRevenue * 1.05)  -- 5% growth assumption

Seasonal Adjusted Forecast = 
[Linear Trend Forecast] * 
CALCULATE(
    AVERAGE([Total Revenue]),
    ALLEXCEPT('DateTable', 'DateTable'[MonthNumber])
) / 
CALCULATE(
    AVERAGE([Total Revenue]),
    ALL('DateTable')
)
```

## Advanced Financial Analysis

### Break-even Analysis
```dax
Break-even Revenue = 
DIVIDE(
    [Fixed Costs],
    (1 - ([Variable Costs] / [Total Revenue])),
    0
)

Contribution Margin = [Total Revenue] - [Variable Costs]

Contribution Margin Ratio = 
DIVIDE(
    [Contribution Margin],
    [Total Revenue],
    0
)
```

### Cash Flow Analysis
```dax
Operating Cash Flow = 
[Net Profit] + 
CALCULATE(SUM(FinancialData[Amount]), FinancialData[Category] = "Depreciation") -
CALCULATE(SUM(FinancialData[Amount]), FinancialData[Account] = "Accounts Receivable", FinancialData[Type] = "Asset") +
CALCULATE(SUM(FinancialData[Amount]), FinancialData[Account] = "Accounts Payable", FinancialData[Type] = "Liability")

Free Cash Flow = 
[Operating Cash Flow] -
CALCULATE(SUM(FinancialData[Amount]), FinancialData[Category] = "Capital Expenditures")
```

### Working Capital Management
```dax
Net Working Capital = [Current Assets] - [Current Liabilities]

Working Capital Ratio = 
DIVIDE(
    [Current Assets],
    [Current Liabilities],
    0
)

Days Sales Outstanding (DSO) = 
DIVIDE(
    CALCULATE(SUM(FinancialData[Amount]), FinancialData[Account] = "Accounts Receivable"),
    [Total Revenue] / 365,
    0
)

Days Payable Outstanding (DPO) = 
DIVIDE(
    CALCULATE(SUM(FinancialData[Amount]), FinancialData[Account] = "Accounts Payable"),
    [COGS] / 365,
    0
)

Days Inventory Outstanding (DIO) = 
DIVIDE(
    CALCULATE(SUM(FinancialData[Amount]), FinancialData[Account] = "Inventory"),
    [COGS] / 365,
    0
)

Cash Conversion Cycle = [DSO] + [DIO] - [DPO]
```

## Best Practices for Financial DAX

### Performance Optimization
```dax
-- Use variables for complex calculations
Revenue Analysis = 
VAR TotalRev = [Total Revenue]
VAR TotalExp = [Total Expenses]
VAR NetProf = TotalRev - TotalExp
RETURN
NetProf

-- Use SUMMARIZE for aggregated calculations
Monthly Revenue = 
SUMMARIZE(
    FinancialData,
    'DateTable'[Year],
    'DateTable'[Month],
    "Revenue", [Total Revenue]
)

-- Use CALCULATE with FILTER for complex conditions
High Value Transactions = 
CALCULATE(
    COUNTROWS(FinancialData),
    FILTER(
        FinancialData,
        FinancialData[Amount] > 10000
    )
)
```

### Error Handling
```dax
Safe Division = 
DIVIDE(
    [Numerator],
    [Denominator],
    0  -- Return 0 instead of error
)

Revenue with BLANK handling = 
IF(
    ISBLANK([Total Revenue]),
    0,
    [Total Revenue]
)

Conditional Calculation = 
IF(
    [Total Revenue] > 0,
    [Net Profit] / [Total Revenue],
    BLANK()
)
```

This comprehensive DAX reference guide provides the essential formulas needed for financial analysis and dashboard creation in Power BI.
