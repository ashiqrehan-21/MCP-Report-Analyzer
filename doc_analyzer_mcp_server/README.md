# MCP Document Analyzer Server

This project is an MCP (Model Context Protocol) server designed to analyze document reports and send email summaries.
Note: With MCP you can write tools to any extent and change the functionality as per liking.

## Setup

1. **Install dependencies:**
   ```sh
   pip install -r requirements.txt
   ```

2. **Prepare reports:**
   Place your `.docx` or `.txt` report files in the `doc_analyzer_mcp_server/reports/` directory.

## Running the Server

To start the MCP server:
```sh
python doc_analyzer_mcp_server/src/main.py
```

## Sending Email Summaries

The email tools require you to provide your SMTP username (email) and app password as arguments. **These are required and not read from environment variables or .env files.**

### Example: Sending a Report Summary Email

You can call the `send_report_summary_email` tool (or function) with the following arguments:

- `recipient`: Recipient email address (comma-separated for multiple)
- `filename`: Name of the report file in the `reports/` directory
- `smtp_user`: Your SMTP username (your email address)
- `smtp_password`: Your SMTP password or app password
- `smtp_server`: (Optional) SMTP server address (default: `smtp.gmail.com`)
- `smtp_port`: (Optional) SMTP server port (default: `587`)
- `custom_message`: (Optional) Custom message to include in the email

**Example usage in Python:**
```python
send_report_summary_email(
    recipient="someone@example.com",
    filename="your_report.docx",
    smtp_user="your_email@gmail.com",
    smtp_password="your_app_password"
)
```

### Example: Sending a Custom Email
```python
sendmail(
    recipient="someone@example.com",
    subject="Test Email",
    body="This is a test.",
    smtp_user="your_email@gmail.com",
    smtp_password="your_app_password"
)
```

## Notes
- **Do not hardcode your SMTP credentials in the codebase.** Always provide them at runtime.
- The server listens on port 8000 by default. You can change this by setting the `FASTMCP_PORT` environment variable or editing the `mcp.json` config.
- For security, use an app password for Gmail or similar providers.

## Troubleshooting
- If you get an error about missing SMTP credentials, ensure you are passing both `smtp_user` and `smtp_password` as arguments.
- If you have issues with email delivery, check your SMTP server settings and credentials.
