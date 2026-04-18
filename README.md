# Banking System & Rupay Card Integration
A robust Python CLI application simulating a core banking environment. This system manages customer accounts, handles financial transactions, and integrates a simulated Rupay Network for debit card issuance.
**📌 Features**
KYC-Based Account Creation: Validates unique users via PAN and Aadhar numbers.
Automated Account Numbering: Generates standardized 12-digit SBI account numbers.
Financial Operations:
Deposit and Withdrawal with real-time balance updates.
Inter-account fund transfers with double-entry verification.
Balance inquiry.
Rupay Debit Card System:
Automatic ₹500 issuance fee deduction.
Eligibility check (requires minimum ₹500 balance).
3-year expiry date calculation.
Random CVV and unique 12-digit card number generation.
**🛠️ Code Analysis & Architecture**
The project utilizes Object-Oriented Programming (OOP) to maintain data integrity:
Bank Class: The central ledger. It uses private attributes (__customerDatabase) to prevent unauthorized access. It handles the core logic for account generation and balance mathematical operations.
Rupay Class: Acts as an external service provider. It maintains its own database of issued cards and ensures that card numbers are never duplicated across the network.
BankOperations Class: The controller layer. It translates user requests into bank actions, ensuring that rules (like "don't issue a card if balance is low") are enforced.
Customer Class: A standardized template for gathering user information.
**🧪 Comprehensive Test Cases**
The following table outlines the scenarios tested within this system:
Operation	Scenario	Input	Expected Result
1. Create Account	New User	Unique PAN/Aadhar	Account SBI000...01 created.
Duplicate User	Existing PAN/Aadhar	"Account already Exists".
2. Cash Withdrawal	Success	Valid ID + Amount < Balance	Balance deducted; Success message.
Insufficient Funds	Amount > Balance	"Low balance !".
Security Check	Wrong Account Name	"Account details Miss-matched".
3. Deposit	Standard Deposit	Valid Account + Name	Balance increases immediately.
4. Check Balance	Inquiry	Valid Account Number	Displays current accountBalance.
5. Transfer Money	Valid Transfer	Sender (Bal > 500), Valid Receiver	Sender -Amount; Receiver +Amount.
Failed Transfer	Sender (Bal < Amount)	"Low balance in sender's account".
Invalid Receiver	Wrong Receiver Details	"Account details miss-matched".
6. Get Debit Card	New Issuance	Balance >= ₹500	Balance -₹500; Card & CVV issued.
Low Balance	Balance < ₹500	"Minimum balance must be ₹500".
Already Issued	Repeat Request	"Debit card already exists".
**💻 Technical Implementation Details**
Data Privacy: All databases are prefixed with __ (double underscores), making them private to their respective classes.
Date Handling: Uses the datetime module to calculate a timedelta of 1095 days (3 years) for card expiry.
String Formatting: Uses .zfill(12) to ensure account numbers always maintain a 12-digit padding after the "SBI" prefix.
UI/UX: Uses a while True loop and match-case to provide a persistent, menu-driven interface.
⚠️ Important Notes
Runtime Memory: This application stores data in RAM. If you close the program, all accounts and transaction history will be deleted.
Input Validation: Ensure numeric fields (Mobile, Aadhar, Amount) are entered as digits to avoid ValueError.
**Future Enhancements**
Integration of phonePe and its operations on bank 
