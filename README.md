# E-commerce Analysis: Seasonal Trends & Cart Abandonment
import pandas as pd
import matplotlib.pyplot as plt

# Load dataset
df = pd.read_csv("ecommerce_data_sample.csv")

# Convert Order Date to datetime
df["Order Date"] = pd.to_datetime(df["Order Date"])

# Monthly Sales Trend
df["Month"] = df["Order Date"].dt.to_period("M")
monthly_sales = df.groupby("Month")["Sales"].sum()

plt.figure(figsize=(10, 5))
monthly_sales.plot(marker='o')
plt.title("Monthly Sales Trend")
plt.ylabel("Total Sales")
plt.xlabel("Month")
plt.grid(True)
plt.tight_layout()
plt.show()

# Cart Abandonment Rate
abandon_rate = df["Cart Abandoned"].mean() * 100
print(f"Cart Abandonment Rate: {abandon_rate:.2f}%")

# Category Sales Breakdown
category_sales = df.groupby("Category")["Sales"].sum().sort_values(ascending=False)
category_sales.plot(kind="bar", title="Sales by Category", ylabel="Sales", xlabel="Category", figsize=(8,4))
plt.tight_layout()
plt.show()
