🛠️ How to Set Up the CC Spends Tracker System (No Coding Experience Needed)

This guide assumes you're using:

Gmail (to receive transaction emails)
Google Sheets (to log and reconcile data)
Google Apps Script (for automation)

🔧 Step 1: Create Your Google Sheets File
Open Google Sheets.
Create a new spreadsheet and name it something like CC Spend Tracker.
Add the following sheets (tabs) at the bottom:
Infinia – to log credit card transactions
Common account – to log matching savings account debits
CC processing log – for logging email processing status
Unmatched Emails – (optional) for unmatched UPI credit emails
Processing Log – (optional) to track script executions

In the Infinia and Common account sheets, create headers in row 1 like this:
In Infinia sheet:

Message ID	Date	Time	Amount	Merchant	Reconciliation ID

In Common account sheet:

Message ID	Amount	Name	UPI ID	Date	Time	Ref	Reconciliation ID

Don't worry if some columns are initially empty — the script fills them in.

💻 Step 2: Open the Apps Script Editor
Go to Extensions → Apps Script in your Google Sheet.
Delete any code that appears by default.
Create three separate script files:
captureHDFCCardSpends
captureCommonAccountCredits_Latest
reconcileInfiniaAndCommonAccount
Paste in the cleaned code from GitHub CCspendstracker.

📝 Step 3: Update Spreadsheet ID
If any script uses:

SpreadsheetApp.openById('YOUR-SPREADSHEET-ID-HERE')
Replace 'YOUR-SPREADSHEET-ID-HERE' with your actual spreadsheet ID:

You’ll find it in the URL of your sheet:
https://docs.google.com/spreadsheets/d/THIS_PART_IS_YOUR_ID/edit

🔐 Step 4: Grant Permissions
Click on each function name (top dropdown in Apps Script).
Click ▶️ Run.
The first time you run it, Google will ask for permissions.
Review and allow them.
You only have to do this once.

🔁 Step 5: Run the Scripts
You can now run each function manually:

captureHDFCCardSpends() → logs credit card transaction emails into the Infinia sheet.
captureCommonAccountCredits_Latest() → logs incoming savings account credits into the Common account sheet.
reconcileInfiniaAndCommonAccount() → matches credit card spends and corresponding savings reimbursements and assigns them a Reconciliation ID.
🕒 Step 6: (Optional) Automate with Time-Driven Triggers
In Apps Script, go to Triggers (clock icon on left).
Click + Add Trigger.
Choose a function (e.g., captureHDFCCardSpends).
Choose Time-driven and how often to run (e.g., every hour).
Repeat for other functions.

✅ You're Done!
You now have:

A credit card + UPI tracking system.
Email-to-Sheet logging.
Automated reconciliation between your credit card and savings account.
Optionally, logs for failed/mismatched entries for easy debugging.
💡 Tips
If you change sheet names or headers, update the script too.
Set a reasonable cap (like 20–50 emails per run) to avoid timeouts.
Manually re-run the functions if you make changes to email formats or headers.
