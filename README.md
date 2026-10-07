# Hostel Manager WhatsApp Automation

An AI-powered **WhatsApp hostel management system** built with **n8n** that allows hostel managers to manage resident records using natural-language **text messages and voice notes**.

Instead of filling out forms or manually editing spreadsheets, a hostel manager can simply send a WhatsApp message describing what they want to add, change, query, or update. The system uses AI to understand the message, identify the resident and relevant information, validate the request, and update the hostel's Google Sheets database.

---

## 🚀 Overview

The system is designed to simplify day-to-day hostel management by allowing managers to interact with their resident database directly through WhatsApp.

A manager can send information naturally, for example:

> "Ali has been assigned room 204 and his rent is 18000."

Later, the manager can send additional information separately:

> "Ali's CNIC is 35202-1234567-1."

Or:

> "Ali has paid his rent."

The system identifies the existing resident and updates only the relevant information instead of requiring the manager to resend the complete resident record.

The manager can also request a **PDF report** directly through WhatsApp.

The same functionality can be used through **voice notes**, allowing hostel managers to operate the system without needing to type structured commands.

---

## ✨ Features

### 📱 WhatsApp Management

* WhatsApp-based hostel management
* Natural-language text messages
* Voice-note based management
* Webhook-based message processing
* Automated WhatsApp responses

### 🤖 AI-Powered Understanding

* AI-based intent detection
* Natural-language information extraction
* Understands different ways of expressing the same request
* Supports incremental resident updates
* Extracts information from both typed messages and voice transcripts
* Handles natural English and Roman Urdu/Urdu-style communication
* Does not require rigid command formats

### 👤 Resident Management

* Add new residents
* Update existing residents
* Vacate residents
* Search for individual residents
* Query resident information
* Query unpaid residents
* Query total income
* Request specific resident fields

### 🔄 Incremental Resident Updates

Resident information does not need to be provided all at once.

For example:

```text
"Add Ali in room 204."
        ↓
Resident created

"Ali's CNIC is 35202-1234567-1."
        ↓
CNIC added to existing resident

"Ali's rent is 18000."
        ↓
Rent updated

"Ali has paid."
        ↓
Rent status updated
```

The system uses existing resident information to determine whether a message represents a **new resident or an update to an existing resident**.

It also aims to preserve existing information when only one field is being updated.

---

## 📄 PDF Reports

The manager can request a PDF report directly through the WhatsApp conversation.

For example:

> "Generate PDF."

The system processes the request and generates a PDF report containing the relevant hostel resident information.

This allows the manager to obtain a portable report without manually exporting or formatting the Google Sheet.

---

## 🛡️ Validation & Protection

The workflow includes several safeguards to prevent incorrect resident records.

* CNIC normalization
* 13-digit CNIC validation
* Duplicate CNIC protection
* Occupied-room protection
* Status-aware room reuse
* Vacated rooms can be assigned to new residents
* Resident-not-found handling
* Duplicate/ambiguous resident handling
* Validation before writing information to Google Sheets
* Conflict responses when a new resident cannot safely be added

---

## 🎙️ Voice Message Processing

The system supports WhatsApp voice notes.

The processing flow is:

```text
WhatsApp Voice Note
        ↓
WhatsApp API
        ↓
n8n Webhook
        ↓
Audio Download
        ↓
Speech-to-Text
        ↓
AI Information Extraction
        ↓
Validation & Resident Matching
        ↓
Google Sheets
        ↓
WhatsApp Response
```

Voice messages are transcribed before being passed to the AI extraction stage.

This allows a hostel manager to communicate with the system naturally instead of typing structured commands.

---

## 🔄 How It Works

```text
                WhatsApp
                   │
          ┌────────┴────────┐
          │                 │
       Text Message      Voice Note
          │                 │
          │            Speech-to-Text
          │                 │
          └────────┬────────┘
                   ↓
             n8n Webhook
                   ↓
          Message Processing
                   ↓
          AI Intent & Extraction
                   ↓
       Resident Identification
                   ↓
       Validation & Conflict Checks
                   ↓
          Google Sheets Database
                   ↓
        Automated WhatsApp Reply
```

PDF requests are routed through the appropriate PDF-generation workflow and delivered back to the manager through WhatsApp.

---

## 🧠 Resident-Aware Updates

One of the important parts of the system is that updates are **resident-aware**.

Instead of treating every message as a completely new record, the workflow can use information already stored in Google Sheets to identify the relevant resident.

This allows messages such as:

> "Update Ali's room to 305."

or:

> "Add Ali's CNIC."

to modify the existing resident record rather than creating another resident.

The system is designed to update only the information relevant to the current message while preserving other existing resident data.

---

## 📊 Google Sheets Database

Google Sheets is currently used as the resident database.

Resident records include information such as:

* Resident Key
* Name
* CNIC
* Room number
* Contact number
* Room rent
* Rent status
* Personal address
* Person status
* Last updated

The workflow performs validation and resident matching before writing changes to the spreadsheet.

---

## 🔎 Query & Reporting

The manager can also request information from the resident database through WhatsApp.

Supported query functionality includes:

* Individual resident lookup
* Requesting specific resident information
* Unpaid resident queries
* Total income queries
* General resident information queries
* PDF report generation

The system retrieves the relevant information from Google Sheets and returns the result through WhatsApp.

---

## 🛠️ Technologies Used

* **n8n** — Workflow automation and business logic
* **WhatsApp Cloud API** — WhatsApp communication
* **Groq API** — AI information extraction and speech-to-text
* **GPT OSS 120B** — Natural-language resident information extraction
* **Whisper Large V3 Turbo** — Voice transcription
* **Google Sheets API** — Resident data storage
* **JavaScript** — Data processing, validation, matching, and workflow logic
* **Cloudflare Tunnel** — Exposing the local n8n webhook during development/testing
* **PDF generation** — Automated resident report generation

---

## 📸 Workflow

Add a screenshot of the complete n8n workflow here.

![n8n Workflow](screenshots/workflow.png)

---

## 💡 Example

A manager could send:

> "Ali is staying in room 204 and his rent is 18000."

The system can extract the resident information and create the resident record.

Later, the manager could send:

> "Ali's CNIC is 35202-1234567-1."

The system identifies Ali and adds the CNIC to his existing record.

Another message could be:

> "Ali moved to room 305."

The system updates Ali's room without requiring the manager to resend his other information.

The manager can also send:

> "Generate PDF."

The system generates the available hostel report and provides it through WhatsApp.

The same interactions can be performed using WhatsApp voice notes.

---

## ⚙️ Requirements

To run the project, you will need:

* n8n
* WhatsApp Cloud API access
* Groq API access
* Google Sheets API access
* A Google account for the resident database
* A publicly accessible webhook URL
* Cloudflare Tunnel or another suitable tunneling/hosting solution when running n8n locally

---

## 🔐 Security

Sensitive credentials should **never** be committed to the repository.

This includes:

* WhatsApp access tokens
* API keys
* Google credentials
* Authentication tokens
* Webhook secrets
* Other private configuration

Credentials should be managed through **n8n's credential system** or environment variables.

---

## 📌 Project Status

**Active Development**

The core hostel resident management system has been developed and tested.

Current functionality includes:

* WhatsApp text processing
* WhatsApp voice-note processing
* AI-powered information extraction
* New resident creation
* Incremental resident updates
* Resident lookup and queries
* Resident vacating
* CNIC validation and normalization
* Duplicate CNIC protection
* Occupied-room protection
* Room reuse after a resident is vacated
* Resident-aware updates
* Google Sheets database integration
* Automated WhatsApp responses
* PDF report generation

The system is being further hardened and prepared for real-world hostel deployment.

---

## 🔮 Future Improvements

Planned functionality includes:

* Automatic monthly rent reminders
* Resident payment mode
* Payment confirmation workflow
* Payment proof collection
* Payment verification
* Payment history
* Automated manager notifications
* Automated payment follow-ups
* Monthly rent reports
* Multiple-hostel support
* Advanced reporting
* Database migration from Google Sheets
* Admin/dashboard interface
* Production hosting and deployment

These features are part of the future roadmap and are **not considered part of the current core workflow** unless implemented separately.

---

## 👨‍💻 Author

**Muhammad Ali Tahir**

Software Engineering Student — FAST NUCES Islamabad
