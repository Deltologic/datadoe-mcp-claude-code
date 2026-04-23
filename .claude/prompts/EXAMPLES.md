# Example Prompts Library

The following are example prompts you can use with DataDoe MCP for Amazon.com seller operations.  
You can copy-paste or adapt these as needed in your workflows.

> [!NOTE]  
> Some example prompts contain parameters in curly braces (e.g., `{{seller_name}}`).  
> When using these prompts, always replace parameters with your actual account name, ASIN, SKU, or other relevant value.  
> For example, if your seller account is "Acme Brands", update `{{seller_name}}` to "Acme Brands".

---

## 1) Show registered sellers

Use when: you want a quick list of seller accounts connected to Amazon.com.

```text
Show my sellers registered on Amazon.com
```

## 2) List active listings

Use when: you need a current snapshot of products live on Amazon.

```text
List all my active Amazon product listings
```

## 3) Get inventory by SKU

Use when: you want stock visibility for replenishment planning.

```text
Show current inventory levels for all my SKUs
```

## 4) Download last month's sales report

Use when: you need historical sales data for monthly review.

```text
Download last month's Amazon sales report
```

## 5) Summarize weekly PPC ad spend

Use when: you want a weekly performance view of paid campaigns.

```text
Prepare me report which includes Top 5 PPC Child ASINs by spend for the last month for {{seller_name}} seller.
```

## 6) Show last 7 days sales by seller

Use when: you want a quick weekly sales snapshot for a specific seller account.

```text
Show my sales for last 7 days for {{seller_name}} seller
```

## 7) List last month's cancelled orders by seller

Use when: you need a cancellation-focused order export for operational review.

```text
Prepare list of orders for {{seller_name}} seller for last month which order status is 'Cancelled'. Provide Amazon Order ID, Order Status, Date, Fulfillment Channel and City Destination.
```

## 8) Generate Modern Seller Dashboard Visualization

Use when: You want to create or visualize a clean and modern dashboard for a specific Amazon seller (e.g., for reporting, analysis, executive review, or performance monitoring) with mock or real data.

```text
Make a modern, responsive Dashboard for a {{seller_name}} seller.

**Tech Stack & Context:**
- Use ReactJS and Tailwind CSS for styling.
- Use Recharts for the data visualization.
- Generate realistic mock data for the current period (March 2026, 31 days) and the comparison period (February 2026).

**Layout & Styling Requirements:**
- The overall aesthetic should be clean, modern, and minimalist (think Stripe or Vercel UI). Use a subtle light gray background for the page and white backgrounds for the components, with soft borders and shadows (`shadow-sm`, `rounded-xl`).

**Feature 1: KPIs Grid**
- Create a CSS Grid layout (1 column on mobile, 2 on tablet, 4 on desktop) for four KPI cards.
- Metrics to include: Total Sales (£), Total Units Sold, Total Orders, Total ACOS (%).
- **Card UI:** Each tile must include:
  - A subtle relevant icon in the top right.
  - The Metric Name (muted text, small, uppercase).
  - The Metric Value (large, bold, dark text).
  - The percentage change compared to February 2026.
  - **Logic:** Color-code the percentage change. Green for positive trends (e.g., Sales went up) and Red for negative trends. *Note: For ACOS, a lower number is better, so a decrease should be Green and an increase should be Red.*

**Feature 2: Day-by-Day Line Chart**
- Create a large, responsive card placed below the KPI grid.
- Include a title: "Financial Overview: March 2026".
- **Chart Details:**
  - X-axis: Dates from March 1 to March 31.
  - Y-axis: Currency amount (£).
  - Line 1: 'Total Profit' (Use a smooth curve, primary brand color like bold blue or emerald green).
  - Line 2: 'Ads Costs' (Use a smooth curve, secondary muted color like orange or red).
  - Include an interactive tooltip on hover that shows the exact values for both lines on that specific day, and a legend at the top or bottom.
```

## 9) Generate Weekly PDF Business Report

Use when: you want to automatically generate a weekly PDF Business Report for a specific seller account, including finances, risk/exceptions, and recommendations, in a presentation-ready document.

// Fill all curly brace parameters with concrete values before running:

- `{{seller_name}}` – Seller name (e.g., "Delto UK")
- `{{date_start}}` – Start date of reporting period (e.g., 09.04.2026)
- `{{date_end}}` – End date of reporting period (e.g., 16.04.2026)
- `{{output_pdf_name}}` – PDF filename to save (e.g., DeltoUK_WeeklyReport.pdf)

```text
Generate a script to automatically create a weekly PDF Business Report for a `{{seller_name}}` seller.

**Tech Stack & Requirements:**

- Use the `react-pdf` library for PDF creation.
- Data must include: daily revenue, ad spend, refunds, and flagged system events.
- Date range is from `{{date_start}}` to `{{date_end}}`.

**Document Layout & Styling:**

1. **Header & Meta Information**

   - Title: "`{{seller_name}}`: Weekly Performance & Security Report"
   - Date Range: `{{date_start}}` – `{{date_end}}`
   - Insert a subtle dividing line below the header.

2. **Financial Summary (Profits & Losses)**

   - Display a summary block showing: **Total Revenue**, **Total Costs** (Ads + Fees), and **Net Profit** for the week.
   - Add a concise, generated summary (1–2 sentences) explaining the week's financial trend versus a typical week.

3. **Suspicious Activity & Exceptions**

   - Define "suspicious activity" as: either an unusually high return rate on a specific day or a spike in declined transactions (mock the data accordingly).
   - List incidents as bullet points. If none, output: “All systems normal. No anomalous activity detected.”

4. **Strategic Recommendations**
   - Based on the above mock data, provide **exactly three actionable recommendations** (to increase sales or reduce costs).
   - Each should be a numbered list: start with a bold title for the action, plus a brief supporting explanation.
     Example: `1. **Optimize Ad Spend on Weekends:** Data shows...`

**Execution:**

- The script must compile without errors and save the output PDF to the `./pdfReport` directory within the agent workspace, using the file name `{{output_pdf_name}}`.
```
