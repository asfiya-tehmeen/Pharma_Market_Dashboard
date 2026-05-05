# FDA Drug Approval & Pipeline Intelligence Dashboard
### Pharma Market Analytics | Python · Power BI · FDA Drugs@FDA · Orange Book

---

## What This Project Is

This project replicates the market intelligence workflow used by pharma business development and strategy teams — analyzing 24 years of FDA drug approval data to surface competitive pipeline trends, approval velocity shifts, dosage form innovation patterns, and upcoming patent cliff opportunities.

Built entirely on public FDA datasets. Designed to answer the kinds of questions a pharma analyst or consultant gets asked on day one:

- Which therapeutic areas are attracting the most NDA filings?
- Which companies are accelerating or slowing their approval velocity?
- How is the biologics (BLA) share growing relative to small molecules?
- Which drugs lose patent protection between 2024 and 2030 — and what does that mean for generic market entry?

---

## Dashboard Preview

> *4-page interactive Power BI dashboard — screenshots below*

| Page | Focus |
|---|---|
| Market Overview | FDA approval volume by year, application type, and top sponsors |
| Approval Trends | NDA vs BLA vs ANDA shifts, dosage form evolution, company velocity |
| Company Intelligence | Sponsor benchmarking — breadth vs depth, approval acceleration |
| Patent Cliff Analysis | Drugs losing exclusivity 2024–2030, generic entry opportunity sizing |

*(Add your Power BI screenshots here — export each page as PNG from Power BI: File → Export → Export to PDF or use Snipping Tool)*

---

## Data Sources

| Dataset | Source | Contents |
|---|---|---|
| FDA Drugs@FDA — Products.txt | [FDA Drugs@FDA](https://www.fda.gov/drugs/drug-approvals-and-databases/drugsfda-data-files) | Every approved drug, action date, dosage form, active ingredient |
| FDA Drugs@FDA — Applications.txt | Same | Application type (NDA/BLA/ANDA), sponsor company, approval status |
| FDA Orange Book — products.txt | [FDA Orange Book](https://www.fda.gov/drugs/drug-approvals-and-databases/orange-book-data-files) | Patent expiry dates, exclusivity periods, generic competition data |

All data is publicly available from the U.S. Food and Drug Administration. No proprietary data used.

---

## Project Structure

```
fda-pipeline-intelligence/
├── data/
│   ├── FDA/
│   │   ├── Products.txt
│   │   └── Applications.txt
│   └── FDA Orange/
│       └── products.txt
├── outputs/
│   ├── yearly_approvals.csv
│   ├── company_performance.csv
│   ├── form_trends.csv
│   ├── approval_velocity.csv
│   └── patent_cliff.csv
├── dashboard/
│   └── pharma_pipeline_dashboard.pbix
├── screenshots/
│   ├── page1_market_overview.png
│   ├── page2_approval_trends.png
│   ├── page3_company_intelligence.png
│   └── page4_patent_cliff.png
├── pharma_pipeline_analysis.ipynb
└── README.md
```

---

## Methodology

### 1. Data Pipeline (Python / Pandas)

- Loaded and joined `Products.txt` and `Applications.txt` on `ApplNo`
- Filtered to actual approvals only (`ActionType == 'AP'`), excluding tentative approvals
- Parsed approval dates, extracted year and month for time-series analysis
- Standardized sponsor names to consolidate subsidiary variations (e.g., Janssen → J&J, Pfizer Inc → Pfizer)
- Extracted dosage form categories via regex from free-text `Form` field
- Applied 3-year rolling average to approval velocity to smooth year-to-year noise

### 2. Patent Cliff Analysis (Orange Book)

- Loaded Orange Book patent expiry data
- Filtered to drugs with patent expiry between 2024 and 2030
- Counted unique molecules losing exclusivity per year to size the generic entry opportunity
- Cross-referenced with active ingredient names from the main approvals dataset

### 3. Power BI Dashboard

- Imported 5 output CSVs as separate tables
- Built relationships on `ApprovalYear` (yearly + trends tables) and `SponsorName` (company + velocity tables)
- Created DAX measures for YoY growth, generic share %, and rolling approval averages
- Designed 4-page report with cross-page slicers for application type and year range

---

## Key Findings

> *Update these with your actual numbers after running the analysis*

- **[X] total FDA drug approvals** processed from 2000 to 2024 after deduplication and quality filtering
- **Biologics (BLA) approvals grew [X]%** between 2010 and 2024, reflecting the industry's structural shift from small molecules to large molecule therapies
- **[Top Company]** led all sponsors by approval volume with [X] approvals, while **[Company 2]** showed the highest 3-year velocity acceleration
- **[X] drugs** are projected to lose patent protection between 2024 and 2030, representing a significant generic market entry window — with [Year] being the peak cliff year
- Tablet and capsule forms still dominate (~[X]% of approvals), but injectable and biological formulations have grown from [X]% to [X]% of annual approvals since 2010

---

## How to Run

### Requirements

```
python >= 3.8
pandas
numpy
jupyter
```

Install dependencies:
```bash
pip install pandas numpy jupyter
```

### Steps

1. Download the FDA datasets from the links above and place them in the `data/` folders as shown in the project structure
2. Launch Jupyter from inside the project folder:
```bash
cd path/to/fda-pipeline-intelligence
jupyter notebook
```
3. Open `pharma_pipeline_analysis.ipynb` and run all cells in order
4. Output CSVs will be saved to the `outputs/` folder
5. Open `dashboard/pharma_pipeline_dashboard.pbix` in Power BI Desktop and refresh data sources to point to your local `outputs/` folder

---

## Why This Matters

Patent cliff analysis, pipeline benchmarking, and approval velocity tracking are standard outputs of pharma business intelligence and strategy functions. Tools like IQVIA, Citeline, and Evaluate Pharma charge thousands of dollars per license for this kind of data. This project replicates the core analytical layer using publicly available FDA data — demonstrating that the methodology, not the data subscription, is the value.

This type of analysis is directly relevant to:
- **Pharma BD & Strategy teams** evaluating competitive pipeline positioning
- **Market access analysts** assessing generic entry timing and pricing pressure
- **Healthcare consultants** building market sizing models for pharma clients
- **Regulatory affairs teams** benchmarking approval timelines by application type

---

## Author

**Asfiya Tehmeen**

[LinkedIn](https://linkedin.com/in/your-profile) · [Portfolio](https://github.com/your-username)
