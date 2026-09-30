import csv
import os


FILE_NAME = os.path.join(
    os.path.dirname(os.path.abspath(__file__)),
    "expenses.csv"
)


def load_expenses():
    expenses = []

    if not os.path.exists(FILE_NAME):
        return expenses

    try:
        with open(FILE_NAME, "r", newline="", encoding="utf-8") as file:
            reader = csv.DictReader(file)

            for row in reader:
                expenses.append({
                    "name": row["name"],
                    "amount": float(row["amount"]),
                    "category": row["category"],
                    "date": row["date"]
                })

    except (OSError, ValueError, KeyError):
        print("Warning: Could not load saved expenses.")

    return expenses


def save_expenses(expenses):
    try:
        with open(FILE_NAME, "w", newline="", encoding="utf-8") as file:
            fieldnames = ["name", "amount", "category", "date"]

            writer = csv.DictWriter(file, fieldnames=fieldnames)
            writer.writeheader()
            writer.writerows(expenses)

    except OSError:
        print("Error: Could not save expenses.")


def view_expenses(expenses):
    print("\n--- Your Expenses ---")

    if not expenses:
        print("No expenses recorded yet.")
        return

    for number, expense in enumerate(expenses, start=1):
        print(
            f"{number}. "
            f"{expense['name']} | "
            f"${expense['amount']:.2f} | "
            f"{expense['category']} | "
            f"{expense['date']}"
        )


def update_expense(expenses):
    if not expenses:
        print("\nNo expenses available to update.")
        return

    view_expenses(expenses)

    try:
        number = int(input("\nEnter the expense number to update: "))

        if number < 1 or number > len(expenses):
            print("Invalid expense number.")
            return

        expense = expenses[number - 1]

        print("\nEnter the new information.")

        name = input(f"Enter new name ({expense['name']}): ").strip()
        amount = input(f"Enter new amount ({expense['amount']:.2f}): ").strip()
        category = input(f"Enter new category ({expense['category']}): ").strip()

        if name:
            expense["name"] = name

        if amount:
            try:
                new_amount = float(amount)

                if new_amount <= 0:
                    print("Amount must be greater than zero.")
                    return

                expense["amount"] = new_amount

            except ValueError:
                print("Please enter a valid amount.")
                return

        if category:
            expense["category"] = category

        save_expenses(expenses)

        print("\nExpense updated successfully!")

    except ValueError:
        print("Please enter a valid number.")


# Load expenses from CSV
expenses = load_expenses()

# Show expenses before updating
print("\nExpenses before updating:")
view_expenses(expenses)

# Test Update Expense
update_expense(expenses)

# Show expenses after updating
print("\nExpenses after updating:")
view_expenses(expenses)


# Other operations will be added one by one later
