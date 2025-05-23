# 🧩 n8n Automation: Webhook to Google Sheets Logger

This workflow listens for incoming POST requests via a webhook, extracts form or payload data, and logs the information into a designated Google Sheets document. Ideal for logging submissions, tracking data, or building lightweight backends.

🔗 Workflow Structure

```
Webhook → Set Node → Google Sheets Node
```

🚀 Features

- Accepts JSON data from any client (e.g., frontend forms, Postman, API).
- Adds a timestamp and formats the payload.
- Logs data to a specific Google Sheet.
- Easily extendable with notifications (Slack, Email, Discord, etc.).

🛠️ Setup Instructions

1. Clone or Import Workflow into n8n

- Use the n8n editor to **create a new workflow**.
- Add the nodes as shown in the structure above.
- Make sure n8n is running (locally or on a server).

2. Webhook Node Configuration

- Method: `POST`  
- Path: `/log-entry` (or any name)
- Use this endpoint in your application or Postman:
  ```
  http://localhost:5678/webhook-test/log-entry
  ```

Example Payload

```json
{
  "name": "Ashley",
  "email": "ashley@example.com",
  "message": "This is a test message."
}
```

3. Set Node (Transform & Enrich Data)

Add the following fields:
- `fullName` → `{{$json["name"]}}`
- `emailId` → `{{$json["email"]}}`
- `message` → `{{$json["message"]}}`
- `receivedAt` → `{{new Date().toISOString()}}`

4. Google Sheets Node Configuration

- Operation: `Append Row`
- Resource: `Sheet Within Document`
- Spreadsheet: Your chosen document
- Worksheet: The tab name (e.g., `Logs`)

Map the fields:

| Sheet Column     | Value                         |
|------------------|-------------------------------|
| fullName         | `{{$json["fullName"]}}`       |
| emailId          | `{{$json["emailId"]}}`        |
| message          | `{{$json["message"]}}`        |
| receivedAt       | `{{$json["receivedAt"]}}`     |

Make sure the **column headers in your sheet match these keys**.

📌 Use Cases

- Log contact form submissions
- Capture webhook payloads
- Build integrations without a backend
- Store incoming data in structured format

📈 Future Improvements (Optional)

- Add Slack/Discord notifications  
- Add data validation  
- Store backups to Airtable or Notion  
- Add error catching flow

👤 Created By

Ashley Mathias  
n8n + Automation Developer  
Connect on [LinkedIn](https://www.linkedin.com/in/ashleymathias/) | GitHub | Portfolio
