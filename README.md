# Go Green Woods — Stock Update

This project contains two python scripts that work together to automate inventory updates for **Go Green Woods**.  
The workflow is:  
**Scrape live stock data → Clean + merge into Wayfair export → Updated inventory sheet**

---

## 📂 Files

### 1. `Amp_Web_Scrape.ipynb`
- Automates login to the vendor CMS using **Selenium**.  
- Navigates to the Living Room category and switches to list view.  
- Paginates through all products, collecting **SKU** and **Stock**.  
- Saves results to:
  - `raw_inventory.csv` → stable filename, always overwritten with the latest scrape  

**Inputs:**  
- credentials (`CMS_EMAIL`, `CMS_PASSWORD`)  

**Outputs:**  
- `raw_inventory.csv`  

---

### 2. `AMP_DataCleaning.ipynb`
- Reads the scraped data from `raw_inventory.csv`.  
- Finds the latest Wayfair export file (`Inventory_*.csv`).  
- Prefixes SKUs with `GGWal` for alignment.  
- Updates the **In Stock** column in the Wayfair export.  
- Fills blank values in key numeric columns (`In Stock`, `Quantity Backordered`, `Quantity on Order`) with 0.  
- Reorders columns for consistency.  
- Saves results to:
  - `merged_wayfair_inventory.csv` → stable filename, always overwritten with the latest merge  
  - *(optional)* timestamped backup: `merged_wayfair_inventory_YYYYMMDD_HHMMSS.csv`

**Inputs:**  
- `raw_inventory.csv` (from the scraper)  
- Latest Wayfair export file (`Inventory_*.csv`)  

**Outputs:**  
- `merged_wayfair_inventory.csv`  

---

## ⚙️ Setup

1. **Clone this repo locally**  
   ```bash
   git clone https://github.com/<your-username>/go-green-woods.git
   cd go-green-woods
