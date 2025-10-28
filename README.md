 🤖 AI Expense Tracker

An intelligent expense tracking system built with n8n that automatically processes and records your expenses through natural conversation. Simply chat about your purchases, and the AI handles the rest!

![n8n Workflow](https://img.shields.io/badge/n8n-Workflow-orange)
![OpenAI](https://img.shields.io/badge/OpenAI-Powered-green)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-Integration-blue)

 ✨ Features

- 💬 Conversational Interface: Natural language input via chat trigger
- 🧠 Smart Field Extraction: AI Agent automatically parses:
  - Transaction type (Credit/Debit)
  - Expense category
  - Amount
  - Running total balance
- 📊 Automated Recording: Direct integration with Google Sheets
- 🚨 Low Balance Alerts: Automatic email when balance < ₹10,000
- ✨ Beautiful Formatting: Chat Model optimizes responses for:
  - User-friendly chat replies
  - Clean Google Sheets entries
  - Professional Gmail notifications
- 💾 Context Retention: Simple Memory maintains conversation flow and balance tracking

 🏗️ Architecture

The workflow consists of five main components:

1. Chat Trigger - Receives chat messages from users
2. AI Agent - Processes natural language using OpenAI
3. Simple Memory - Stores conversation context and balance data
4. Google Sheets - Records expense transactions
5. Gmail - Sends notification emails for important alerts

 🔄 Workflow Process

```
User Input → AI Agent (Extract Fields) → Google Sheets (Record) → Balance Check → 
Gmail Alert (if < 10000) → Chat Model (Format Response) → User
```

1. Chat Trigger: User sends a message about transaction (e.g., "I bought phone of 112000")
2. AI Agent: Extracts and structures data into fields:
   - Credit/Debit
   - Type of Expense
   - Amount
   - Total Balance
3. Google Sheets: Records the transaction with all fields
4. Conditional Check: If balance drops below 10,000
5. Gmail: Sends low balance alert email with formatted message
6. OpenAI Chat Model: Optimizes and beautifies the response for:
   - User chat reply
   - Google Sheets entry formatting
   - Gmail notification text
7. Simple Memory: Maintains conversation context and running balance

 📋 Prerequisites

- [n8n](https://n8n.io/) instance (cloud or self-hosted)
- OpenAI API key
- Google Account with Sheets API access
- Gmail API credentials

 🚀 Setup Instructions

 1. Clone the Workflow

Import the workflow JSON into your n8n instance:
- Download the workflow file
- Go to n8n → Workflows → Import from File
- Select the downloaded JSON

 2. Configure Credentials

Set up the following credentials in n8n:

OpenAI API
- Navigate to Credentials → Add Credential → OpenAI
- Enter your OpenAI API key

Google Sheets
- Add Google OAuth2 credentials
- Authorize access to Google Sheets

Gmail
- Add Gmail OAuth2 credentials
- Authorize access to send emails

 3. Set Up Google Sheet

Create a Google Sheet with the following columns (as extracted by AI Agent):

| Date | Credit/Debit | Type of Expense | Amount | Total |
|------|--------------|-----------------|--------|-------|

 4. Configure Workflow Nodes

Chat Trigger
- Set up your preferred chat interface
- Configure webhook or messaging platform

AI Agent (Field Extractor)
- Create prompt to extract: Credit/Debit, Type of Expense, Amount, Total
- Example prompt structure:
```
Extract the following from user input:
- Is this a Credit or Debit?
- What type of expense is this?
- What is the amount?
- Calculate the new total balance
```

Google Sheets Node
- Link to your expense tracking spreadsheet
- Map extracted fields to sheet columns

Conditional Node
- Set condition: `Total Balance < 10000`
- Routes to Gmail when condition is true

OpenAI Chat Model
- Configure to optimize and format responses
- Used for beautifying:
  - Chat replies to user
  - Google Sheets data entries
  - Gmail alert messages

Gmail Node
- Set recipient email address
- Use formatted text from Chat Model

Simple Memory
- Initialize with starting balance
- Configure to store conversation context

 5. Activate Workflow

- Click "Activate" in the top right corner
- The workflow is now ready to process expenses!

 💡 Usage Examples

Simply chat with the system naturally:

```
"I bought a phone for 112000"
→ Records: Debit of 112000, updates balance to -104000, sends low balance alert

"Spent 500 on groceries"
→ Records: Debit of 500 in Groceries category

"Received salary of 50000"
→ Records: Credit of 50000, updates balance
```

 🎯 Key Components

 1. Chat Trigger
- Entry point for user messages
- Captures natural language transaction inputs

 2. AI Agent (Field Extractor)
- Purpose: Parses user input into structured fields
- Output Fields:
  - Credit/Debit classification
  - Type of expense (category)
  - Amount
  - Total balance (running calculation)
- Example: "I bought phone of 112000" → {type: "Debit", category: "Electronics", amount: 112000, balance: -104000}

 3. Google Sheets Integration
- Records structured transaction data
- Maintains expense history with all extracted fields
- Updates running balance automatically

 4. Conditional Logic (Balance Monitor)
- Checks if balance < ₹10,000
- Triggers alert workflow when threshold is breached

 5. OpenAI Chat Model (Response Optimizer)
- Triple-purpose formatting:
  - Crafts user-friendly chat responses
  - Formats data beautifully for Google Sheets entries
  - Generates professional Gmail notification text
- Ensures consistent, polished communication across all channels

 6. Gmail Notification
- Sends formatted low balance alerts
- Uses optimized text from Chat Model
- Keeps you informed about account status

 7. Simple Memory
- Stores conversation context
- Tracks running balance between messages
- Enables continuity across multiple transactions

 📊 Sample Output

When you log an expense:

```
Input: "I bought phone of 112000"

Output: "The purchase of the phone for 112000 has been recorded 
as a Debit, and the new total balance is -104000. An alert email 
has been sent to you regarding the low bank balance."
```

 🔧 Customization

 Modify Alert Threshold
Update the condition node to change when low balance alerts trigger

 Add Categories
Enhance the AI prompt to recognize custom expense categories

 Change Memory Structure
Modify the Simple Memory node to store additional fields

 Custom Email Templates
Edit the Gmail node to personalize notification messages

 📈 Future Enhancements

- [ ] Add support for multiple currencies
- [ ] Implement expense analytics and insights
- [ ] Create monthly/weekly spending reports
- [ ] Add receipt image processing
- [ ] Support for multiple bank accounts
- [ ] Budget tracking and warnings
- [ ] Export functionality (PDF, CSV)

 🐛 Troubleshooting

Workflow not triggering?
- Ensure the workflow is activated
- Check chat interface connectivity

AI not extracting data correctly?
- Review OpenAI API key validity
- Adjust AI prompt for better accuracy

Sheets not updating?
- Verify Google Sheets credentials
- Check sheet permissions

 📝 License

MIT License - feel free to use and modify for your needs



Built with ❤️ using n8n automation

Making expense tracking as easy as having a conversation!
