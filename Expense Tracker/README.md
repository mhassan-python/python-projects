Personal Expense Tracker

A simple Python program for managing personal expenses using a CSV file.

Features

* Loads saved expenses from expenses.csv
* Displays all recorded expenses
* Updates an existing expense
* Allows changing:
    * Expense name
    * Amount
    * Category
* Saves updated expenses back to the CSV file
* Handles basic input and file errors

Technologies Used

* Python
* CSV
* OS

How It Works

The program reads expense information from an expenses.csv file.

Each expense contains:

* Name – Name of the expense
* Amount – Cost of the expense
* Category – Expense category
* Date – Date of the expense

The program first displays the saved expenses. It then asks the user to select an expense and enter new information. After the update, the changes are saved back to the CSV file.

CSV File

The program uses the following columns in expenses.csv:

name,amount,category,date

Example:

Lunch,15.50,Food,2026-10-01
Taxi,25.00,Transport,2026-10-02

How to Run

1. Make sure Python is installed.
2. Keep Expense Tracker.py and expenses.csv in the same folder.
3. Open the project in Visual Studio Code.
4. Run:

python “Expense Tracker.py”

5. Follow the instructions shown in the terminal.

Project Structure

Expense Tracker/
│
├── Expense Tracker.py
├── expenses.csv
└── README.md

Future Improvements

More expense-management features can be added later, such as:

* Adding new expenses
* Deleting expenses
* Calculating total expenses
* Showing expenses by category
* More advanced expense management

Author

Muhammad Hassan