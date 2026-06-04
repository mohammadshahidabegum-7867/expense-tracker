import csv

FILE_NAME = "expenses.csv"

def add_expense():
    date = input("Enter Date (DD-MM-YYYY): ")
    category = input("Enter Category: ")
    amount = float(input("Enter Amount: "))

    with open(FILE_NAME, "a", newline="") as file:
        writer = csv.writer(file)
        writer.writerow([date, category, amount])

    print("Expense Added Successfully!\n")

def view_expenses():
    try:
        with open(FILE_NAME, "r") as file:
            reader = csv.reader(file)

            print("\nDate\t\tCategory\tAmount")
            print("-" * 40)

            for row in reader:
                print(f"{row[0]}\t{row[1]}\t\t{row[2]}")

    except FileNotFoundError:
        print("No expenses found.\n")

def total_expense():
    total = 0

    try:
        with open(FILE_NAME, "r") as file:
            reader = csv.reader(file)

            for row in reader:
                total += float(row[2])

        print(f"\nTotal Expense = ₹{total}\n")

    except FileNotFoundError:
        print("No expenses found.\n")

while True:
    print("===== EXPENSE TRACKER =====")
    print("1. Add Expense")
    print("2. View Expenses")
    print("3. Calculate Total Expense")
    print("4. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":
        add_expense()
    elif choice == "2":
        view_expenses()
    elif choice == "3":
        total_expense()
    elif choice == "4":
        print("Thank You!")
        break
    else:
        print("Invalid Choice")
