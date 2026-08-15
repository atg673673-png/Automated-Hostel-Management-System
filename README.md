# 🏠 Hostel Manager WhatsApp Automation

An AI-powered WhatsApp automation system built with **n8n** that allows hostel managers to send resident information through **text messages or voice notes**. The system processes the incoming messages, extracts the required information, and automatically stores the data in **Google Sheets**.

## 🚀 Overview

This project is designed to simplify hostel management by reducing the need for manually entering resident information.

Instead of manually updating records, a hostel manager can send a WhatsApp message or voice note containing information such as:

* Resident name
* Room number
* Contact number
* Monthly rent
* Other relevant hostel information

The automation receives the message, processes it using AI, extracts the required information, and updates the corresponding Google Sheet automatically.

## ✨ Features

* 📱 WhatsApp-based communication
* 💬 Text message processing
* 🎙️ Voice note processing
* 🤖 AI-powered information extraction
* 📊 Automatic Google Sheets updates
* ⚙️ Fully automated n8n workflow
* 🔄 Webhook-based message processing

## 🔄 How It Works

```text
WhatsApp Message / Voice Note
            ↓
       WhatsApp API
            ↓
        n8n Webhook
            ↓
     Message Processing
            ↓
        AI Processing
            ↓
   Information Extraction
            ↓
      Google Sheets
```

The manager sends the required information through WhatsApp. The n8n workflow receives the message through a webhook and determines how the message should be processed.

For voice notes, the audio is processed and converted into text before being passed to the AI processing stage.

The AI identifies the relevant information and structures it into the required fields. Finally, the extracted information is stored in Google Sheets.

## 🛠️ Technologies Used

* **n8n** — Workflow automation
* **WhatsApp API** — Message communication
* **AI / LLM** — Message understanding and information extraction
* **Google Sheets API** — Data storage
* **Cloudflare Tunnel** — Securely exposing the local n8n instance
* **JavaScript** — Data processing and workflow logic

## 📸 Workflow

Add a screenshot of the complete n8n workflow here.

```text
![n8n Workflow](screenshots/workflow.png)
```

## 💡 Example Use Case

A hostel manager can send a message such as:

> "Ali has been assigned room 204 and his monthly rent is 18,000."

The automation processes the message, identifies the relevant information, and stores it in the appropriate Google Sheets fields.

The same process can be performed using a voice note.

## ⚙️ Requirements

To run this project, you will need:

* n8n
* WhatsApp API access
* An AI model/API
* Google Sheets API access
* Cloudflare Tunnel or another method for exposing the n8n webhook
* A Google account for the spreadsheet

## 🔐 Security

API keys, access tokens, passwords, and other sensitive credentials should **not** be stored directly in this repository.

Credentials should be configured through n8n's credential system or environment variables.

## 📌 Project Status

**Active Development**

The core automation workflow has been developed and tested. Additional improvements and features may be added in future versions.

## 🔮 Future Improvements

* Resident record search through WhatsApp
* Automatic rent-status tracking
* Payment reminders
* Improved natural-language commands
* Multiple hostel support
* Better error handling and validation
* Database integration
* Admin dashboard

## 👨‍💻 Author

**Muhammad Ali Tahir**

Software Engineering Student
FAST NUCES Islamabad
