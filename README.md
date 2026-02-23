class BankAccount:
    def __init__(self, acc_no, name, balance=0):   # ✅ FIXED
        self.acc_no = acc_no
        self.name = name
        self.balance = balance
        self.transactions = []

    # DEPOSIT
    def deposit(self, amount):
        if amount <= 0:
            print("❌ Enter valid deposit amount")
            return

        self.balance += amount
        self.transactions.append(f"Deposited ₹{amount}")

        print("\n===== DEPOSIT DETAILS =====")
        print("Account Number:", self.acc_no)
        print("Account Holder:", self.name)
        print("You have deposited ₹", amount)
        print("Current Balance:", self.balance)

    # WITHDRAW
    def withdraw(self):
        print("\nCurrent Balance:", self.balance)

        try:
            amount = float(input("Enter amount to withdraw: "))
        except ValueError:
            print("❌ Invalid amount")
            return

        if amount <= 0:
            print("❌ Enter valid withdrawal amount")
        elif amount > self.balance:
            print("❌ Insufficient balance")
        else:
            self.balance -= amount
            self.transactions.append(f"Withdrawn ₹{amount}")
            print("✅ Withdrawal Successful")
            print("Remaining Balance:", self.balance)

    # BALANCE CHECK
    def display_balance(self):
        print("Current Balance:", self.balance)

    # TRANSACTION HISTORY
    def show_transactions(self):
        print("\n===== TRANSACTION HISTORY =====")
        if not self.transactions:
            print("No transactions yet.")
        else:
            for t in self.transactions:
                print(t)


accounts = {}


# CREATE ACCOUNT
def create_account():
    acc_no = input("Enter Account Number: ").strip()

    if not acc_no.isdigit() or len(acc_no) != 5:
        print("❌ Enter valid account number (must be exactly 5 digits)")
        return

    if acc_no in accounts:
        print("Account already exists!")
        return

    name = input("Enter Account Holder Name: ").strip()
    accounts[acc_no] = BankAccount(acc_no, name)
    print("✅ Account Created Successfully")


def get_account():
    acc_no = input("Enter Account Number: ").strip()
    return accounts.get(acc_no)


# MAIN MENU
while True:
    print("\n===== BANK MENU =====")
    print("1. Create Account")
    print("2. Deposit")
    print("3. Withdraw")
    print("4. Check Balance")
    print("5. Transaction History")
    print("6. Exit")

    choice = input("Enter choice: ").strip()

    if choice == "1":
        create_account()

    elif choice == "2":
        acc = get_account()
        if acc:
            try:
                amt = float(input("Enter amount to deposit: "))
                acc.deposit(amt)
            except ValueError:
                print("❌ Invalid amount")
        else:
            print("Account not found!")

    elif choice == "3":
        acc = get_account()
        if acc:
            acc.withdraw()
        else:
            print("Account not found!")

    elif choice == "4":
        acc = get_account()
        if acc:
            acc.display_balance()
        else:
            print("Account not found!")

    elif choice == "5":
        acc = get_account()
        if acc:
            acc.show_transactions()
        else:
            print("Account not found!")

    elif choice == "6":
        print("🙏 Thank you for using Banking System")
        break

    else:
        print("Invalid choice! Try again.")
