# 📩 T2G Email Summary Bot (UiPath REFramework)

This is the **Queue Processor** component of the Talents2Germany email automation solution. It pulls structured metadata from Orchestrator, logs or stores relevant information if needed, and sends a summary notification email once all queue items are processed.

Built using UiPath’s Robotic Enterprise Framework (REFramework) in C#.

---

### 📌 What It Does

- ✅ Retrieves email metadata from the Orchestrator queue (`FilteredEmailsQueue`)
- ✅ Validates and logs the data (if needed)
- ✅ Tracks number of processed items
- ✅ Sends a single summary email when processing is complete

---

### 🔄 REFramework Logic

#### 1. **Init**
- Load configuration values and assets

#### 2. **Get Transaction Data**
- Retrieve queue items one at a time from `FilteredEmailsQueue`

#### 3. **Process Transaction**
- Increment counter
- Track sender or log details if necessary
- Compose summary when last item is processed
- Send summary email via Outlook

#### 4. **End Process**
- Clean up resources

---

### 📧 Summary Email Sample

```text
Subject: Email Automation Summary – Talents2Germany

Hello,

The automation successfully processed 12 email inquiries from the queue.

Best regards,  
T2G Automation Bot
```
---

### 📂 Orchestrator Setup

#### Queue
| Name               | Purpose                                |
|--------------------|----------------------------------------|
| `FilteredEmailsQueue` | Holds one queue item per parsed email |

#### Assets
| Name              | Type | Description                                  |
|-------------------|------|----------------------------------------------|
| `ExcelReportPath` | Text | Full path to Excel file in `Data\Output`     |
| `NotificationEmail` | Text | Summary recipient (used by Handler)         |

---

### 📁 Running the Bot

1. Open this project in UiPath Studio (C#)
2. Ensure Outlook is configured
3. Update `Config.xlsx` with the correct paths and values
4. Ensure assets and queue are created in Orchestrator
5. Run in attended or unattended mode
