# Financial Health Dashboard

An interactive Power BI dashboard designed for SMEs to analyze financial performance, track profitability trends, and provide forecasting for budgeting and financial planning.

## Features

### 📊 Core Visualizations
- **Income Statement Analysis**: Revenue, expenses, and net profit tracking
- **Balance Sheet Overview**: Assets, liabilities, and equity monitoring
- **Cash Flow Analysis**: Operating, investing, and financing activities
- **Profitability Trends**: Monthly/quarterly performance analysis
- **Financial Ratios**: Key performance indicators (KPIs)

### 🔄 Interactive Elements
- Date range filtering
- Category and account drill-down
- Comparative analysis (month-over-month, year-over-year)
- Dynamic forecasting scenarios

### 📈 Forecasting & Planning
- Revenue projection models
- Expense trend analysis
- Cash flow forecasting
- Budget vs. Actual comparisons

## Data Structure

The dashboard uses the following data structure:

| Column | Type | Description |
|--------|------|-------------|
| Date | DateTime | Transaction date |
| Category | String | Financial category (Revenue, COGS, Operating Expenses, etc.) |
| Account | String | Specific account name |
| Amount | Decimal | Transaction amount |
| Type | String | Income, Expense, Asset, Liability, or Equity |

## Key DAX Measures

### Financial Metrics
- **Total Revenue**: `CALCULATE(SUM(Amount), Type = "Income")`
- **Total Expenses**: `CALCULATE(SUM(Amount), Type = "Expense")`
- **Net Profit**: `[Total Revenue] - [Total Expenses]`
- **Profit Margin**: `DIVIDE([Net Profit], [Total Revenue], 0)`

### Balance Sheet Metrics
- **Total Assets**: `CALCULATE(SUM(Amount), Type = "Asset")`
- **Total Liabilities**: `CALCULATE(SUM(Amount), Type = "Liability")`
- **Total Equity**: `CALCULATE(SUM(Amount), Type = "Equity")`

### Financial Ratios
- **Current Ratio**: `DIVIDE([Total Assets], [Total Liabilities], 0)`
- **Debt to Equity**: `DIVIDE([Total Liabilities], [Total Equity], 0)`
- **Return on Equity**: `DIVIDE([Net Profit], [Total Equity], 0)`

## Setup Instructions

### 1. Data Preparation
- Export your financial data to CSV format matching the structure above
- Ensure dates are in YYYY-MM-DD format
- Categorize transactions appropriately

### 2. Power BI Setup
1. Open `Financial_Health_Dashboard.pbix` in Power BI Desktop
2. Replace the sample data with your actual financial data:
   - Click "Transform Data" → "Data source settings"
   - Change the data source to your CSV file
   - Refresh the data model

### 3. Customization
- Adjust date ranges in the filters pane
- Modify color schemes in the formatting options
- Add additional measures as needed for your business

## Dashboard Pages

### 1. Financial Overview
- Key performance indicators (KPIs)
- Profit and loss summary
- Quick ratio analysis

### 2. Income Statement
- Revenue trends by category
- Expense breakdown
- Profit margin analysis

### 3. Balance Sheet
- Asset composition
- Liability structure
- Equity changes over time

### 4. Cash Flow
- Operating cash flow
- Investing activities
- Financing activities

### 5. Forecasting
- Revenue projections
- Expense forecasts
- Cash flow predictions

## Best Practices

### Data Management
- Update data regularly (weekly/monthly)
- Maintain consistent categorization
- Reconcile with accounting software

### Analysis Tips
- Compare against industry benchmarks
- Set up budget vs. actual tracking
- Monitor key ratios regularly

## Troubleshooting

### Common Issues
1. **Data not loading**: Check CSV format and file path
2. **Measures not calculating**: Verify data types and relationships
3. **Visuals not updating**: Refresh data and check filters

### Performance Optimization
- Use summarized data for large datasets
- Implement incremental refresh for historical data
- Optimize DAX measures for better performance

## Support

For questions or issues:
1. Check the data structure matches requirements
2. Verify Power BI version compatibility
3. Review DAX measure formulas

## Version History

- v1.0 (2024-01-01): Initial release with core financial metrics
- v1.1 (2024-01-15): Added forecasting capabilities
- v1.2 (2024-02-01): Enhanced visualizations and interactivity

## License

This dashboard template is provided as-is for educational and business use. Modify and adapt as needed for your organization's requirements.
