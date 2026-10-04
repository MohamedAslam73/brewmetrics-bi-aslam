# BrewMetrics — Copilot DAX Development Notes

## 1. Month-over-Month Growth

**Measure:** `MoM Growth %`

**Copilot suggestion:**
Copilot suggested calculating the current month's sales and comparing it with the previous month's sales using `DATEADD()`.

**My correction:**
I verified that the calculation needed to use the `Dim_Date[Date]` column and handled the division using `DIVIDE()` to avoid division-by-zero errors.

**Final approach:**
The measure calculates the percentage change between current-month sales and previous-month sales.

---

## 2. Running Total Sales

**Measure:** `Running Total Sales`

**Copilot suggestion:**
Copilot suggested using `CALCULATE()` with a date filter to accumulate sales over time.

**My correction:**
I verified the filter context and used `ALL(Dim_Date[Date])` so that the calculation considers all dates up to the current date.

**Final approach:**
The measure calculates cumulative sales from the beginning of the available period through the current date.

---

## 3. City Sales Rank

**Measure:** `City Sales Rank`

**Copilot suggestion:**
Copilot suggested using `RANKX()` to rank cities according to total sales.

**My correction:**
I used `ALL(Dim_City[city])` so that every city is considered when calculating the ranking.

**Final approach:**
The measure ranks cities from highest to lowest based on total sales.

---

## 4. Average Order Value

**Measure:** `Average Order Value`

**Copilot suggestion:**
Copilot suggested calculating total sales divided by the number of transactions.

**My correction:**
I verified the transaction identifier column in the Fact_Sales table and used `DISTINCTCOUNT()` to count unique transactions.

**Final approach:**
The measure calculates the average sales value per transaction.

---

## Copilot Correction Example

During development, I did not use Copilot output blindly. I checked the suggested DAX against the star-schema relationships and the actual column names in the model. I corrected the date column and filter context where necessary, and verified the measures in Power BI before committing them.
