# Banking-System
def create_account(name):
    # Firstly we have create Function for the user with initial balance of zero (0) and an empty transaction history.
    account = {
        "name": name,
        "balance": 0.0,
        "transactions": []
    }
    print(f"Account for {name} created with balance ${account['balance']}.")
    return account

def deposit(account, amount):
    #01 Then create Function to deposit money into the account. Ensures the deposit is positive and records the transaction.
    if amount <= 0:
        print("Deposit amount must be positive.")
        return account
    #02 Update balance and record the deposit
    account['balance'] += amount
    account['transactions'].append(f"Deposit: ${amount}. New Balance: ${account['balance']}")
    #03 Write the transaction to a file
    with open(f"{account['name']}_transactions.txt", "a") as file:
        file.write(f"Deposit: ${amount}. New Balance: ${account['balance']}\n")
    print(f"Deposited ${amount}. New balance: ${account['balance']}")
    return account

def withdraw(account, amount):
    #01 Function to withdraw money from the account. Checks if the user has sufficient balance and records the transaction.
    if amount <= 0:
        print("Withdrawal amount must be positive.")
        return account
    if amount > account['balance']:
        print("Insufficient balance!")
        return account
    #02 Update balance and record the withdrawal
    account['balance'] -= amount
    account['transactions'].append(f"Withdrawal: ${amount}. New Balance: ${account['balance']}")
    #03 Write the transaction to a file
    with open(f"{account['name']}_transactions.txt", "a") as file:
        file.write(f"Withdrawal: ${amount}. New Balance: ${account['balance']}\n")
    print(f"Withdrew ${amount}. New balance: ${account['balance']}")
    return account

def check_balance(account):
    # Function to check and display the current balance in the account.
    print(f"Current balance: ${account['balance']}")
    return account

def print_statement(account):
    # Function to print the transaction statement showing all deposits and withdrawals.
    print(f"Account Statement for {account['name']}:")
    if not account['transactions']:
        print("No transactions made.")
        return
    for transaction in account['transactions']:
        print(transaction)

def main():
    # Main function to run the banking system example.
    # Step 1: Create an account for Subhan
    account = create_account("Muhammad Subhan")
    # Step 2: Subhan deposits $500
    account = deposit(account, 500)
    # Step 3: Subhan withdraws $200
    account = withdraw(account, 200)
    # Step 4: Subhan checks his balance
    account = check_balance(account)
    # Step 5: Print the transaction statement
    print_statement(account)

if _name_ == "_main_":
    main()
