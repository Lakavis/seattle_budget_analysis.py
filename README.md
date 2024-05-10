import csv

# Function to format currency
def format_currency(amount):
    return "${:,.2f}".format(amount)

# Dictionary to store department expenses
department_expenses = {}

# Replace 'path_to_csv_file.csv' with the actual path to the CSV file you downloaded
csv_file_path = 'path_to_csv_file.csv'

# Read the CSV file
with open(csv_file_path, newline='', encoding='utf-8') as csvfile:
    reader = csv.DictReader(csvfile)
    for row in reader:
        department = row['Department']
        expense = float(row['2012 Actual'].replace(',', ''))
        
        # Aggregate expenses for each department
        if department in department_expenses:
            department_expenses[department] += expense
        else:
            department_expenses[department] = expense

# Print the results
print("Department\tTotal Expenses")
print("-" * 30)
for department, expense in department_expenses.items():
    print(f"{department}\t{format_currency(expense)}")
