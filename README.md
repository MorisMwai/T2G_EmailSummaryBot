# 📩 T2G Email Summary Bot (UiPath REFramework)

This is the **Queue Processor** component of the Talents2Germany email automation solution.  
It consumes email metadata from Orchestrator, optionally logs details for auditing, and sends a single summary notification once all items are processed.

Built using UiPath’s Robotic Enterprise Framework (REFramework) in C#.

---

### 📌 What It Does

- ✅ Retrieves email metadata from the Orchestrator queue (`FilteredEmailsQueue`)
- ✅ Logs or stores transaction details if needed
- ✅ Tracks processed item count, including:
  - Total processed partnership/investor emails
  - Total processed CV-related emails
- ✅ Sends a summary email to a configured recipient

---

### 🛠 Tech Stack

- UiPath Studio (REFramework – C#)
- Orchestrator Queues & Assets
- Outlook Integration for email summary

---

### 🔄 REFramework Logic

#### 1. **Init**
- Load configuration values and assets

#### 2. **Get Transaction Data**
- Pull queue items from `FilteredEmailsQueue` one at a time until empty

#### 3. **Process Transaction**
- Increment counters
- Track sender details (optional logging)
- If the item is a **summary type**, store `ProcessedEmails` and `ProcessedEmailsWithAttachments`
- Compose and send a summary email using collected counters:
  - `ProcessedEmails`
  - `ProcessedEmailsWithAttachments`

#### 4. **End Process**
- Dispose resources and log completion

---

### 📧 Summary Email Sample

```text
Subject: Email Automation Summary – Talents2Germany

Hello,

The automation successfully processed:
- 10 partnership/investor emails
- 2 CV emails with attachments

Best regards,
T2G Automation Bot
```
---

### 📂 Orchestrator Setup

#### Queue
| Name               | Purpose                                        |
|--------------------|------------------------------------------------|
| `FilteredEmailsQueue` | 	Holds all processed email data and summary |

#### Assets
| Name              | Type | Description                                  |
|-------------------|------|----------------------------------------------|
| `NotificationEmail` | Text | Email address to receive the summary report |

---

### 📁 Running the Bot

1. Open in UiPath Studio (C#)
2. Configure Outlook for sending summary email
3. Ensure Config.xlsx contains correct values
4. Validate assets and queue in Orchestrator
5. Execute in attended or unattended mode
