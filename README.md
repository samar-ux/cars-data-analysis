# Used Vehicle Listings: Exploratory Data Analysis
![Project cover](<img width="1200" height="627" alt="cars-data-analysis-cover" src="https://github.com/user-attachments/assets/e45bedca-690f-49eb-83ef-3ed29d28bc38" />

Exploratory data analysis of 15,049 used-vehicle listings (Craigslist) using Python. The notebook cleans the data and answers 12 business-style questions about manufacturers, prices, vehicle types, conditions, fuel types and mileage.

## Objective

Understand what the listings look like and which factors are associated with vehicle price.

## Dataset

`vehicles.xlsx`: 15,049 listings, 26 columns.

| Group | Columns |
|---|---|
| Vehicle | `manufacturer`, `model`, `year`, `type`, `condition`, `cylinders`, `fuel`, `transmission`, `drive`, `size`, `paint_color`, `odometer`, `title_status`, `VIN` |
| Listing | `price`, `posting_date`, `description`, `url`, `image_url` |
| Location | `region`, `state`, `lat`, `long` |

Data quality issues found during assessment:
- `county` is 100% missing, and `size` (about 73%), `condition` (about 42%), `cylinders`, `VIN` and `drive` have large gaps.
- Extreme values exist (for example prices of 0 and above 900 million, and odometer readings up to 10 million).

## Approach

1. **Extract:** load the Excel file with pandas.
2. **Assess:** `info()`, missing values, summary statistics, duplicates and unique values of categorical columns.
3. **Clean:**
   - removed duplicates (none were found)
   - filled missing `condition` with `unknown`
   - dropped rows missing `price`, `year` or `manufacturer`
   - converted `price` to float and `year` to integer
   - removed prices above the 99th percentile
4. **Explore:** 12 questions answered with grouping, aggregation and plots.

## Key findings

- **Most common manufacturers:** Ford (2,458 listings), Chevrolet (2,135) and Toyota (1,224).
- **Most common types:** sedans (2,905), SUVs (2,701) and pickups (1,843).
- **Most listed models:** F-150 (308) and Silverado 1500 (213).
- **Average price by manufacturer:** Tesla (about $38.4k), Jaguar (about $31.1k) and Alfa Romeo (about $29.7k) are the highest; Saturn (about $3.9k) and Mercury (about $5.8k) are the lowest. Brands with few listings can skew these averages.
- **Price by vehicle type:** pickups have the highest average price (about $27.8k), while mini-vans (about $14.7k) and sedans (about $16.2k) are among the lowest.
- **Price by fuel type:** diesel vehicles average about $27.2k versus about $18.8k for gas and $18.2k for hybrid.
- **Price by condition:** `fair` (about $4.3k) and `salvage` (about $3.4k) are far cheaper than other conditions. About 42% of listings have an unknown condition.

## Limitations

- **Zero-price listings remain:** 581 listings (about 4% of the cleaned data) still have a price of 0, which pulls down every average price reported above. Only the top 1% of prices was removed.
- **Outliers in mileage:** 76 listings above 500k miles remain (the maximum is 10 million), so average mileage by type (for example, off-road and trucks above 270k miles) should be read with caution. Medians would be more robust.
- **Small groups:** some categories have very few listings. For example, Tesla's average is based on 38 listings, Saturn and Mercury on 24 each, and the `new` and `salvage` conditions on 38 and 16, so these averages are not reliable.
- **Geography:** after cleaning, the listings cover only three states (AK, AL and AZ), so state-level comparisons are not representative.
- **Model names are not standardized** (for example `silverado`, `silverado 1500` and `1500` appear separately).
- The analysis is descriptive; it shows associations, not causes.

## Next steps

- Remove zero-price listings and unrealistic mileage values, then re-run the analysis.
- Standardize model names.
- Use medians alongside means.
- Add a price-prediction model (for example, regression with scikit-learn).
- Build an interactive Power BI dashboard from the cleaned data.

## How to run

```bash
git clone https://github.com/samar-ux/cars-data-analysis.git
cd cars-data-analysis
pip install pandas numpy matplotlib seaborn openpyxl jupyter
```

Open `cars_data_analysis.ipynb` and run all cells. The dataset `vehicles.xlsx` is included in the repository.

## Tech stack

Python, pandas, NumPy, matplotlib, seaborn, Jupyter.

## Author

**Samar Mohamed**: Full-Stack Developer | AI & Automation | Power BI
[LinkedIn](https://www.linkedin.com/in/samar-mohamed-71a4b7178/) | samar7ux@gmail.com
