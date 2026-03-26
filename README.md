
#  Expense Tracker System (Python)

#  Project Description

The **Expense Tracker System** is a simple yet effective Python-based application designed to help users manage and monitor their daily expenses. In today’s fast-paced world, tracking expenses is essential for maintaining financial stability and avoiding unnecessary spending.

This project allows users to **record their expenses under different categories**, view previously saved data, and calculate the total expenditure over a period of time. It also provides basic feedback on spending habits, helping users understand whether their expenses are within a reasonable range.

The application uses **file handling (CSV format)** to store data permanently, ensuring that the information is not lost after the program is closed. The system is menu-driven, making it easy to use even for beginners.

---

#  Objectives

* To develop a simple and user-friendly expense management system
* To understand and implement **file handling in Python**
* To perform **basic calculations and data processing**
* To encourage users to track and manage their spending habits
* To demonstrate real-world application of Python programming concepts

---

#  Files in the Project

* `expense.py` – Main Python program containing all functions and logic
* `expenses.csv` – Data file used to store expense records (expense name and amount)

---

#  Features

*  Add new expenses with name and amount
*  View all recorded expenses
*  Calculate total expenses
*  Store and retrieve data using CSV file
*  Continuous operation using menu-driven system
*  Error handling for missing files
*  Optional feedback based on spending level (Low / Moderate / High)
*  Simple and modular code structure for easy understanding

---

#  Requirements

* Python 3.x installed on the system
* Basic understanding of Python (loops, functions, file handling)
* Any code editor (VS Code / IDLE / PyCharm)

---

#  Technologies Used

* **Programming Language:** Python
* **Concepts Used:**

  * Variables and Data Types
  * Lists and Dictionaries
  * Functions
  * Loops (while, for)
  * Conditional Statements (if-else)
  * File Handling (CSV module)

---

#  How to Run the Program

1. Create a folder for the project
2. Create a Python file named `expense.py`
3. Copy and paste the program code into the file
4. Open terminal or command prompt
5. Navigate to the project folder
6. Run the program using:

```bash id="runexp123"
python expense.py
```

---

#  Program Workflow

1. The program displays a menu with options
2. User selects an option:

   * Add expense
   * View expenses
   * Calculate total
   * Exit
3. If adding expense:

   * User enters name and amount
   * Data is stored in `expenses.csv`
4. If viewing expenses:

   * File is read and displayed
5. If calculating total:

   * All values are summed and shown
6. Program repeats until user exits
    #  Logic Explanation

* Expenses are stored in a **CSV file** as rows
* Each row contains:

  * Expense Name
  * Amount
* The program reads and writes data using Python’s `csv` module
* Total expense is calculated using a loop that adds all amounts
* Conditional statements are used to provide feedback


---
# Program
```
import csv
import tkinter as tk
from tkinter import messagebox
import matplotlib.pyplot as plt

FILE = "expenses.csv"

# -------- Functions -------- #

def add_expense():
    name = entry_name.get()
    amount = entry_amount.get()

    if name == "" or amount == "":
        messagebox.showwarning("Input Error", "Please enter all fields")
        return

    try:
        amount = float(amount)
    except:
        messagebox.showerror("Error", "Amount must be a number")
        return

    with open(FILE, 'a', newline='') as file:
        writer = csv.writer(file)
        writer.writerow([name, amount])

    messagebox.showinfo("Success", "Expense Added!")
    entry_name.delete(0, tk.END)
    entry_amount.delete(0, tk.END)


def view_expense():
    try:
        with open(FILE, 'r') as file:
            reader = csv.reader(file)
            output.delete('1.0', tk.END)
            for row in reader:
                output.insert(tk.END, f"{row[0]} - ₹{row[1]}\n")
    except FileNotFoundError:
        messagebox.showerror("Error", "No data found")


def total_expense():
    total = 0
    try:
        with open(FILE, 'r') as file:
            reader = csv.reader(file)
            for row in reader:
                total += float(row[1])
        messagebox.showinfo("Total Expense", f"₹{total}")
    except FileNotFoundError:
        messagebox.showerror("Error", "No data found")


def plot_expenses():
    names = []
    amounts = []

    try:
        with open(FILE, 'r') as file:
            reader = csv.reader(file)
            for row in reader:
                names.append(row[0])
                amounts.append(float(row[1]))

        if names:
            plt.figure()
            plt.bar(names, amounts)
            plt.xlabel("Expense Name")
            plt.ylabel("Amount (₹)")
            plt.title("Expense Graph")
            plt.xticks(rotation=45)
            plt.show()
        else:
            messagebox.showinfo("Info", "No data to plot")

    except FileNotFoundError:
        messagebox.showerror("Error", "No data found")


# -------- UI -------- #

root = tk.Tk()
root.title("Expense Tracker")
root.geometry("400x450")

# Labels
tk.Label(root, text="Expense Name").pack()
entry_name = tk.Entry(root)
entry_name.pack()

tk.Label(root, text="Amount").pack()
entry_amount = tk.Entry(root)
entry_amount.pack()

# Buttons
tk.Button(root, text="Add Expense", command=add_expense).pack(pady=5)
tk.Button(root, text="View Expenses", command=view_expense).pack(pady=5)
tk.Button(root, text="Total Expense", command=total_expense).pack(pady=5)
tk.Button(root, text="Show Graph", command=plot_expenses).pack(pady=5)

# Output Box
output = tk.Text(root, height=10)
output.pack()

root.mainloop()


```
#  Example Menu

```id="menuexp001"
1. Add Expense
2. View Expenses
3. Total Expense
4. Exit
Enter your choice:
```



#  Sample Output

###  Adding Expenses

```id="addexp001"
Enter expense name: Food
Enter amount: 200
Expense saved successfully!
```

```id="addexp002"
Enter expense name: Travel
Enter amount: 500
Expense saved successfully!
```
# Output
<img width="928" height="603" alt="image" src="https://github.com/user-attachments/assets/d5b58e67-baf0-42fe-abf2-ed24ba183c6c" />
<img width="496" height="588" alt="image" src="https://github.com/user-attachments/assets/fd204fe8-d000-4f5b-9e32-01579339fdf4" />
<img width="882" height="595" alt="image" src="https://github.com/user-attachments/assets/32cfa047-cf3c-4471-a119-91c434555202" />
<img width="793" height="676" alt="image" src="https://github.com/user-attachments/assets/959cc1fb-a92c-404b-a02d-271cd3b14087" />



#  Viewing Expenses

```id="viewexp001"
Expenses:
Food - ₹200
Travel - ₹500
```


#  Total Expense

```id="totalexp001"
Total Expense: ₹700
```


#  Future Enhancements

*  Add date-wise expense tracking
*  Categorize expenses (Food, Travel, Bills, etc.)
*  Graphical representation using `matplotlib`
*  GUI interface using `tkinter`
*  Search and filter expenses
*  Convert into mobile/web app



# Limitations

* No authentication system (anyone can access data)
* Limited to basic expense tracking
* No advanced analytics or reports
* Command-line interface only


## Testing

The program was tested with:

* Valid inputs (numbers, text)
* Invalid inputs (strings instead of numbers)
* Empty file scenarios
* Multiple entries



# Conclusion

The Expense Tracker System is a practical and beginner-friendly project that demonstrates how Python can be used to solve real-life problems. It helps users manage their daily expenses efficiently while also strengthening programming concepts such as file handling, loops, and conditionals.

This project can be further enhanced into a full-fledged financial management system with advanced features and a graphical interface.

