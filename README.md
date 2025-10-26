# Currency-Converter-Project
A simple real-time currency converter built using Python and Tkinter
# currency_converter.py
# ----------------------------------------------------------
# Currency Converter and Market Indices (Mini Project)
# Developed by: Aishwarya SD, Aishwarya KU, Shubhashree NG, Sinchana HK
# Guide: Mr. Rohith P
# Department of Electronics and Communication Engineering
# Bahubali College of Engineering, Shravanabelagola
# ----------------------------------------------------------

import tkinter as tk
from tkinter import messagebox

# Example exchange rates (you can modify or replace with live API)
exchange_rates = {
    'USD': {'EUR': 0.95, 'INR': 84.46, 'GBP': 0.79},
    'EUR': {'USD': 1.05, 'INR': 89.29, 'GBP': 0.83},
    'INR': {'USD': 0.012, 'EUR': 0.011, 'GBP': 0.0093},
    'GBP': {'USD': 1.27, 'EUR': 1.20, 'INR': 107.07},
}

# Static market indices data
static_market_indices = {
    "Dow Jones": "35,200.50",
    "S&P 500": "4,550.22",
    "NASDAQ": "14,400.80",
    "FTSE 100": "7,900.25",
    "DAX": "15,700.65",
    "Nikkei 225": "33,000.75",
}


# Function to convert the currency
def convert_currency():
    try:
        amount = float(entry_amount.get())
        from_currency = from_currency_var.get()
        to_currency = to_currency_var.get()

        if not from_currency or not to_currency:
            messagebox.showerror("Error", "Please select both currencies.")
            return

        if from_currency == to_currency:
            messagebox.showinfo("Result", "Both currencies are the same. No conversion needed.")
            return

        if from_currency in exchange_rates and to_currency in exchange_rates[from_currency]:
            rate = exchange_rates[from_currency][to_currency]
            converted_amount = amount * rate
            result_label.config(
                text=f"{amount} {from_currency} = {converted_amount:.2f} {to_currency}"
            )
        else:
            messagebox.showerror("Error", "Exchange rate for this conversion is not available.")
    except ValueError:
        messagebox.showerror("Error", "Please enter a valid numeric amount.")


# Function to display static market indices
def show_static_indices():
    indices_text = "\n".join(
        [f"{index}: {value}" for index, value in static_market_indices.items()]
    )
    market_indices_label.config(text=indices_text)


# -------------------- GUI Setup --------------------
root = tk.Tk()
root.title("Currency Converter and Market Indices")
root.geometry("600x700")
root.configure(bg="lightblue")

# Title Label
tk.Label(root, text="Currency Converter", bg="lightblue", font=("Arial", 20, "bold")).place(x=150, y=10)

# Amount input
tk.Label(root, text="Enter Amount:", bg="lightblue", font=("Arial", 12)).place(x=50, y=80)
entry_amount = tk.Entry(root)
entry_amount.place(x=200, y=80, width=150)

# From Currency
tk.Label(root, text="From Currency:", bg="lightblue", font=("Arial", 12)).place(x=50, y=130)
from_currency_var = tk.StringVar(value="USD")
from_currency_menu = tk.OptionMenu(root, from_currency_var, "USD", "EUR", "INR", "GBP")
from_currency_menu.place(x=200, y=125)

# To Currency
tk.Label(root, text="To Currency:", bg="lightblue", font=("Arial", 12)).place(x=50, y=180)
to_currency_var = tk.StringVar(value="INR")
to_currency_menu = tk.OptionMenu(root, to_currency_var, "USD", "EUR", "INR", "GBP")
to_currency_menu.place(x=200, y=175)

# Convert Button
convert_button = tk.Button(root, text="Convert", command=convert_currency, bg="lightgreen", font=("Arial", 12))
convert_button.place(x=200, y=230)

# Result Label
result_label = tk.Label(root, text="", font=("Arial", 14), bg="lightblue")
result_label.place(x=50, y=280)

# Static Market Indices Section
tk.Label(root, text="Global Market Indices", bg="lightblue", font=("Arial", 16, "bold")).place(x=50, y=350)
market_indices_label = tk.Label(root, text="", font=("Arial", 12), bg="lightblue", justify="left")
market_indices_label.place(x=50, y=390)

# Refresh Button
refresh_button = tk.Button(root, text="Show Indices", command=show_static_indices, bg="lightgreen", font=("Arial", 12))
refresh_button.place(x=200, y=620)

# Display static indices initially
show_static_indices()

# Run the GUI
root.mainloop()
