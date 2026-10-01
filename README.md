# 🧺 QuickBasket Checkout App

**Automating small business sales with Python.**

QuickBasket is a lightweight, offline-friendly checkout system built in a Jupyter Notebook. It lets a cashier enter items, then calculates the subtotal, applies a discount, adds VAT, and produces a clean, readable text receipt — no external services or third-party libraries required.

---

## ✨ Features

- **Shopping cart** stored as a simple Python dictionary (`item → price & quantity`)
- **Add items** – repeated items automatically have their quantities combined
- **Remove items** – with a friendly message if the item isn't in the cart
- **Interactive entry** – a cashier-style loop; type `done` to finish
- **Input validation** – safely converts input with `float()` / `int()` and rejects non-numeric values, negative prices and zero/negative quantities
- **Pricing pipeline** – subtotal → discount → tax (VAT, default 7.5%) → final amount
- **Formatted receipt** – store name, date/time, cashier, itemised lines and totals

---

## 🗂️ Project Structure

```
QuickBasket_Checkout_App/
├── QuickBasket_Checkout_App.ipynb   # The full app, with step-by-step explanations
└── README.md                        # You are here
```

---

## 🚀 Getting Started

### Requirements

- Python 3.8 or newer
- [Jupyter Notebook](https://jupyter.org/) or JupyterLab

The app only uses the Python standard library (`datetime`), so there is nothing else to install.

### Run it

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# 2. (Optional) install Jupyter if you don't have it
pip install notebook

# 3. Launch the notebook
jupyter notebook QuickBasket_Checkout_App.ipynb
```

Then run the cells from top to bottom (**Run → Run All Cells**).

---

## 🧠 How It Works

The notebook follows a simple **input → process → output** flow, built up in stages:

| Step | What happens |
|------|--------------|
| 1. Cart setup | A dictionary holds each item's `price` and `quantity`. |
| 2. Core functions | `add_item()` and `remove_item()` keep the code clean and reusable (DRY). |
| 3. Interactive input | `collect_items_interactively()` prompts the cashier for items until `done` is typed, validating every entry. |
| 4. Pricing | `calculate_subtotal()`, `apply_discount()`, `apply_tax()` and `calculate_totals()` produce the final amount (money values rounded to 2 decimals). |
| 5. Receipt | `generate_receipt()` builds a fixed-width, human-readable receipt. |

### Key functions

| Function | Purpose |
|----------|---------|
| `add_item(cart, name, price, quantity)` | Adds an item, or increases its quantity if it already exists |
| `remove_item(cart, name)` | Removes an item from the cart |
| `collect_items_interactively(cart)` | Interactive loop to enter items one at a time |
| `calculate_subtotal(cart)` | Sums `price × quantity` across the cart |
| `apply_discount(amount, discount_percent)` | Returns the discounted amount and the discount value |
| `apply_tax(amount, tax_percent)` | Returns the amount with tax and the tax value |
| `calculate_totals(cart, discount_percent, tax_percent)` | Runs the whole pricing pipeline and returns a summary dictionary |
| `generate_receipt(cart, total, store_name, cashier)` | Returns the receipt as a list of text lines |

---

## 💡 Example Usage

```python
cart = {}

add_item(cart, "Bread", 900, 4)
add_item(cart, "Rice", 1500, 3)

totals = calculate_totals(cart, discount_percent=3, tax_percent=4.5)
receipt = generate_receipt(cart, totals, store_name="QuickBasket Store", cashier="John")

print("\n".join(receipt))
```

Or let the cashier enter items interactively:

```python
cart = {}
collect_items_interactively(cart)
```

---

## 🧾 Sample Receipt

```
            QuickBasket Store
             Berlin, Germany
Date: 01-10-2026 12:48
Cashier Name: John
==========================================
Item               Qty  Price($)  Total($)
==========================================
Bread                4    900.00  3,600.00
Rice                 3  1,500.00  4,500.00
==========================================
Subtotal:                         8,100.00
Discount (3%):                     -243.00
VAT (4.5%):                         353.56
==========================================
TOTAL AMOUNT ($):                 8,210.56
==========================================
     Thank you for shopping with us!
             Come back soon!
```

---

## 🛣️ Roadmap

Ideas for future improvements:

- [ ] Save the receipt as an image (e.g. with Pillow) so it can be shared or printed
- [ ] Configurable store name, location and currency
- [ ] Export sales to CSV for record keeping
- [ ] Support multiple discounts or per-item tax rates

---

## 🤝 Contributing

Suggestions and pull requests are welcome. Fork the repo, create a feature branch, and open a PR.

## 📄 License

Add a license of your choice (for example, [MIT](https://choosealicense.com/licenses/mit/)) before sharing publicly.
