# Certificate Renewal Email Automation Workflow

This project is a full-featured **automated email system** built in [n8n](https://n8n.io/) for sending personalized certificate renewal and maintenance reminders based on data from Excel sheets. It automates filtering, formatting, decision-making, and personalized email delivery with attachments.

---

## 💼 Use Case

Companies often need to notify clients before their F-GAS certification expires. This workflow ensures that:
- Emails are sent exactly 1 or 2 months before expiration
- Clients who haven't renewed receive follow-ups
- The Excel database is updated with a timestamp
- Dynamic attachments are included based on the certifying entity (ENTE)

---

## ⚙️ Workflow Overview

### 🔁 Main Steps:
1. **Trigger** at scheduled time (e.g., daily at 12:33)
2. **Read** the Excel database (`.xlsx`)
3. **Check** each client’s expiration date (`Scadenza Azienda`)
4. **Decide** if it's time to send the:
   - First email (2 months before)
   - Second email (1 month before)
   - Re-certification reminders
5. **Generate PDF attachment paths** dynamically
6. **Attach relevant documents** based on ENTE
7. **Send personalized Gmail messages**
8. **Update Excel** with “Sent on [date/time]” in the correct status column

---

## 📁 Required Fields (Excel)

| Column Name         | Description                  |
|---------------------|------------------------------|
| `Nome`, `Cognome`   | Client’s name                |
| `Scadenza Azienda`  | Certification expiry (Excel date) |
| `Num. Contratto Smart` | Contract number           |
| `Email`             | Target email address         |
| `ENTE`              | Certifying body (e.g., RINA) |
| `Link Portale F-gas`| Online link for compliance   |
| `Renewal Confirmed` | Optional: used for follow-ups |

---

## 📨 Email Logic Highlights

- Uses `Set` nodes to format date/time and flags like `equalCheck`
- Separate conditions for each type of reminder (first, second, re-certificate)
- Generates human-readable dates from Excel-style numbers
- Personalizes subject, body, and signature
- Adds attachments depending on the ENTE value

---

## 📦 Attachments

Includes:
- General PDFs (e.g., privacy notice, forms)
- ENTE-specific PDFs (e.g., `RINA.pdf`)

Each email carries:
- `n` static documents
- `1` dynamic attachment if `ENTE` matches a known certifier

---

## 📌 Status Tracking

Each email updates:
- `First Email Status`: `Sent on dd/mm/yyyy at hh:mm`
- `Second Email Status`: same format
- `Status`: marked `not sent` if skipped

---

## 🛠 Technologies Used

- **n8n** (workflow automation)
- **Gmail API**
- **JavaScript (custom logic in Code nodes)**
- **Excel XLSX file parsing**
- **Dynamic branching + attachments**

---

## 📂 How to Use

1. Upload your `.xlsx` database to n8n’s local path
2. Update attachment file paths in the `Code` nodes
3. Ensure Gmail credentials are connected
4. Import the workflow (`.json`) into n8n
5. Enable scheduled execution

---

## 📄 License

This project is under the MIT License.


