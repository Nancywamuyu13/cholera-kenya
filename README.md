# Cholera in Kenya, 1981-2024: How Uneven Is the Burden?

A descriptive analysis of reported cholera cases in Kenya, built in Excel from publicly available data. The project looks at how the disease burden is distributed across years, which years were epidemic years, how the burden changed by period, and whether annual rainfall explains the year-to-year pattern.

**Author:** [Your name]
**Date:** [Month Year]
**Tools:** Excel/WPS Spreadsheet (formulas and charts)

---

## 1. Questions

1. How large is the reported cholera burden in Kenya, and how is it spread across years?
2. Which years were epidemic years?
3. How did the burden change across periods (1980s to 2020s)?
4. Is annual national rainfall associated with reported cases? (secondary check)

## 2. Data

| Data | Source | Coverage | Notes |
|---|---|---|---|
| Reported cholera cases, by country and year | Our World in Data (based on WHO data) | Kenya, 1971-2024 | File: `number-reported-cases-of-cholera.csv`. Accessed [date]. |
| Mean annual rainfall for Kenya (mm) | [FILL IN: dataset name and how it was produced, e.g. Earth Engine export of a gridded rainfall product] | 1981-2024 | File: `ee-chart.csv`. |

**Analysis period:** 1981-2024, the years covered by both datasets. That is 44 years, of which 37 have a case report.

**Missing years:** Seven years in the period have no report (1988, 1990, 1991, 1993, 2003, 2012, 2013). They are treated as *not reported*, never as zero.

## 3. Methods

1. **Cleaning.** Kenya was selected using the country code `KEN`. A complete list of years was built and cases were joined by year, so unreported years appear as gaps.
2. **Descriptive statistics.** Total, mean, median, maximum and minimum of reported cases.
3. **Epidemic years.** An epidemic year is defined as a year with reported cases above the 75th percentile of reported years (4,288 cases). This is a simple rule chosen for this analysis. It is not a medical or WHO definition.
4. **Concentration.** The share of all reported cases that fell in the five largest years.
5. **Period comparison.** Totals, number of reported years, mean cases per reported year and number of epidemic years for 1981-89, 1990-99, 2000-09, 2010-19 and 2020-24.
6. **Rainfall check.** Pearson correlation between annual mean rainfall and reported cases for the 37 years with both values, plus a one-year lag (rainfall in year *t*, cases in year *t+1*).

## 4. Results

### 4.1 The burden is highly uneven

| Measure | Value |
|---|---|
| Years with a report | 37 of 44 |
| Total reported cases | 138,834 |
| Mean per reported year | about 3,752 |
| Median per reported year | 1,206 |
| Peak year | 1998 (22,432 cases) |
| Lowest reported year | 14 cases |
| Share of cases in the five largest years | about 54% |

The mean is roughly three times the median, so a small number of large epidemic years drive the total. The five largest years (1998, 1997, 2015, 2009 and 1999) account for about 54% of all reported cases.

### 4.2 Epidemic years

Nine years exceeded the 4,288-case threshold: **1997, 1998, 1999, 2009, 2015, 2016, 2018, 2019 and 2023.** They cluster, with runs in 1997-1999, 2015-2016 and 2018-2019, which suggests outbreaks often continue for more than one year.

![Reported cholera cases in Kenya](Cholera%20cases%20Chart.png)

*Gaps are years with no report. Orange/blue coloring in the chart follows the epidemic-year rule above.*

### 4.3 Change by period

| Period | Total cases | Years reported | Mean per reported year | Epidemic years |
|---|---|---|---|---|
| 1981-89 | 10,349 | 8 | 1,294 | 0 |
| 1990-99 | 56,968 | 7 | 8,138 | 3 |
| 2000-09 | 20,727 | 9 | 2,303 | 1 |
| 2010-19 | 37,669 | 8 | 4,709 | 4 |
| 2020-24 | 13,121 | 5 | 2,624 | 1 |

![Mean cases per reported year by period](Kenya%20cholera%20cases%20by%20period.png)

The 1990s had the highest mean per reported year, and the 2010s had the most epidemic years (four of eight reported years). Because the periods have different numbers of reported years, the table compares means per reported year, not totals.

### 4.4 Rainfall check (secondary result)

Annual mean rainfall was weakly correlated with reported cases (r = 0.27, n = 37, p about 0.11, not significant at the 5% level). A one-year lag was weaker (r = 0.14). Annual national rainfall therefore does not explain the year-to-year pattern in this dataset.

## 5. Limitations

- **Reported cases only.** The data are cases reported to WHO, not true incidence. Surveillance quality, case definitions and reporting practice changed over time.
- **Missing years.** Seven years have no report, so period totals are not directly comparable, and the real burden in some periods may be higher than shown.
- **Very low recent counts.** The low numbers in 2020 (447), 2021 (38) and 2024 (302) may reflect reporting problems rather than a real fall in cholera. This analysis cannot tell which.
- **National and annual scale.** Annual national totals and averages hide seasonal and regional patterns. A weak national rainfall correlation does not rule out local links between flooding or rainfall and outbreaks.
- **Epidemic threshold.** The 75th-percentile rule is a descriptive choice, and a different cutoff would change the list of epidemic years.
- **Not included.** 2025 data, deaths and case fatality, and county-level data are not part of this analysis.

## 6. Possible next steps

- Add 2025 from the WHO Global Cholera and AWD Dashboard.
- Add reported deaths and calculate case fatality rates.
- Use county-level case data and seasonal (October-December and March-May) rainfall to test local links.
- Map outbreak counties against rainfall or flood extent in GIS.

## 7. Repository structure

```
cholera-kenya/
├── README.md
├── number-reported-cases-of-cholera.csv   (cases data)
├── ee-chart.csv                           (rainfall data)
├── cholera-kenya-analysis.xlsx            (the analysis workbook)
├── Cholera cases Chart.png                (trend chart)
└── Kenya cholera cases by period.png      (period chart)
```

## 8. How to reproduce

1. Open `cholera-kenya-analysis.xlsx`.
2. The `Rain` sheet holds the joined data: year, rainfall, cases, a cleaned cases column, the epidemic-year flag, the summary table and the period table.
3. Key formulas: `QUARTILE(cases,3)` for the threshold, `SUMIFS` and `COUNTIFS` for the period table, `CORREL` for the rainfall check, and `SUM(LARGE(cases,{1,2,3,4,5}))/total` for the concentration share.

## 9. Sources

- Our World in Data, reported cholera cases (based on WHO data): [add the page link and date accessed]
- Rainfall data: [add the dataset name, link and date accessed]
