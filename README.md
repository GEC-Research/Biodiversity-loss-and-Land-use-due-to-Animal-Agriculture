
# Biodiversity Intactness vs Agricultural Land (NHM BTE / PREDICTS, 1970–2014)

This repository reproduces the analysis and figures relating **Biodiversity Intactness Index (BII)** to **agricultural land use** (pasture + cropland) using data from the **Natural History Museum (NHM) Biodiversity Trends Explorer (BTE)**.

Agricultural land is defined strictly as:

agricultural land = pasture + cropland

exactly as provided in the NHM dataset. No external assumptions about livestock feed shares or cropland allocation are used in any calculations.

All processing and figure generation are implemented in:

`BII_vs_ag_land.ipynb`

---

## 1. Repository Structure

```
.
├── data/
│   └── resource.csv
├── output/
│   ├── BII_vs_ag_land_hist_proj_LASTMARK_noYEAR.png
│   └── BII_vs_ag_land_hist_proj_LASTMARK_noYEAR.pdf
├── BII_vs_ag_land.ipynb
└── README.md
```

---

## 2. Input Data (Manual Download Required)

### 2.1 Natural History Museum Biodiversity Trends Explorer (BTE)

**Official dataset page:**  
https://data.nhm.ac.uk/dataset/bii-bte

**Primary resource used:**  
`resource.csv` (extracted from the downloaded ZIP file)

### Download Instructions

1. Visit the dataset page above.
2. Download the dataset ZIP file.
3. **Unzip the downloaded file locally.**
4. From the unzipped contents, locate the file:
   ```
   resource.csv
   ```
5. Move this file into the repository directory:

```
data/resource.csv
```

(Optional) The auxiliary file `area_code.json` may be downloaded for UN M49 region lookups but is not required for the main analysis.

---

## 3. Temporal Coverage

The BTE dataset provides BII and land-use summaries for 1970–2050 (historical and scenario projections).  
In this analysis, we use **only the historical period up to 2014** and restrict the data to:

1970–2014

Years beyond 2014 (scenario-based projections) are excluded from all figures and calculations.

---

## 4. Data Columns Used

The notebook expects the following columns from `resource.csv`:

- `area_code`
- `year`
- `scenario`
- `variable` (e.g., `bii`, `pasture`, `cropland`)
- `value`

Variables are harmonized and aggregated as follows:

```
ag_total = pasture + cropland
```

Both **BII** and **ag_total** are computed as **annual medians across countries** and plotted over 1970–2014.

---

## 5. Method Summary

1. Load BII and land-use data from the NHM BTE summary dataset (`resource.csv`).

2. Restrict the dataset to:
   - Historical scenario only
   - Years 1970–2014

3. Retain only the following variables:
   - Biodiversity Intactness Index (BII)
   - Pasture land
   - Cropland

4. Harmonize land-use variables and construct total agricultural land:
   ```
   ag_total = pasture + cropland
   ```

5. Compute annual country-level values for BII and agricultural land.

6. Aggregate country values to **annual global medians** for BII and agricultural land.

7. Generate time-series figures showing:
   - BII vs agricultural land over 1970–2014
   - Historical trajectory of biodiversity loss relative to agricultural expansion

8. Export final figures to the `output/` directory.

---

## 6. How to Run

### Requirements
- Python ≥ 3.9  
- pandas  
- numpy  
- matplotlib  

### Install

```bash
pip install pandas numpy matplotlib
```

### Run

```bash
jupyter notebook BII_vs_ag_land.ipynb
```

Then run all cells.

---

## 7. Data Sources

Phillips, H., De Palma, A., Gonzalez, R. E., Contu, S., et al. (2021).  
*The Biodiversity Intactness Index – country, region and global-level summaries for 1970–2050*.  
Natural History Museum.  
https://doi.org/10.5519/he1eqmg1


---

## License

- **Code:**  
  MIT License.

- **Data:**  
  This repository uses third-party datasets that are subject to their own licenses and terms of use, including the Biodiversity Intactness Index provided by the Natural History Museum.  
  Users should consult the original data providers for full licensing details.

