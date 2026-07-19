# Architecture

Contains

- System Architecture
                             SENTINELAI GUARD
         AI-Powered Digital Public Safety Intelligence Platform

 ┌───────────────────────────────────────────────────────────────────────────┐
 │                                USERS                                      │
 │                                                                           │
 │  👤 Citizens   👮 Police   🏦 Banks   📡 Telecom   🛡️ Administrator       │
 └───────────────────────────────┬───────────────────────────────────────────┘
                                 │
                                 ▼
 ┌───────────────────────────────────────────────────────────────────────────┐
 │                          FRONTEND (React + Vite)                          │
 │                                                                           │
 │ Dashboard │ Scam Detection │ Currency Detection │ Voice Analysis          │
 │ URL Scanner │ QR Scanner │ Crime Map │ AI Chatbot │ Reports               │
 └───────────────────────────────┬───────────────────────────────────────────┘
                                 │ REST API
                                 ▼
 ┌───────────────────────────────────────────────────────────────────────────┐
 │                    FASTAPI BACKEND & API GATEWAY                          │
 │ Authentication │ Validation │ Business Logic │ Report Engine              │
 └───────────────────────────────┬───────────────────────────────────────────┘
                                 │
                                 ▼
 ┌───────────────────────────────────────────────────────────────────────────┐
 │                              AI ENGINE                                    │
 │                                                                           │
 │ DistilBERT → Scam Text Detection                                          │
 │ YOLOv8 + OpenCV → Counterfeit Currency Detection                          │
 │ Whisper → Voice Transcription                                             │
 │ XGBoost → Risk Scoring                                                    │
 │ RAG/LLM → AI Chatbot                                                      │
 └───────────────────────────────┬───────────────────────────────────────────┘
                                 │
               ┌─────────────────┴─────────────────┐
               ▼                                   ▼
 ┌──────────────────────────┐        ┌─────────────────────────────┐
 │ MongoDB Database         │        │ External Services           │
 │                          │        │                             │
 │ Users                    │        │ Google Maps API             │
 │ Reports                  │        │ Email/SMS Gateway           │
 │ Evidence                 │        │ Government APIs             │
 │ Notifications            │        │ Future NCRB Integration     │
 │ Chat History             │        │                             │
 │ Audit Logs               │        └─────────────────────────────┘
 │ Crime Data               │
 └───────────────┬──────────┘
                 ▼
 ┌───────────────────────────────────────────────────────────────────────────┐
 │                             OUTPUTS                                       │
 │ AI Reports │ Risk Score │ Alerts │ Dashboard │ Crime Heatmap │ Analytics  │
 └───────────────────────────────────────────────────────────────────────────┘
- Data Flow Diagram
                    +----------------------+
                  |      Citizen         |
                  +----------+-----------+
                             |
                             | Uploads
                             ▼
                    +-------------------+
                    | React Frontend    |
                    +---------+---------+
                              |
                              | REST API
                              ▼
                   +----------------------+
                   | FastAPI Backend      |
                   +----------+-----------+
                              |
         +--------------------+----------------------+
         |                    |                      |
         ▼                    ▼                      ▼
+----------------+   +----------------+   +----------------+
| Scam Detector  |   | Currency AI    |   | Voice AI       |
| DistilBERT     |   | YOLOv8/OpenCV  |   | Whisper        |
+--------+-------+   +--------+-------+   +--------+-------+
         |                    |                    |
         +---------+----------+----------+---------+
                   |                     |
                   ▼                     ▼
            +-------------------------------+
            | AI Risk Engine (XGBoost)      |
            +---------------+---------------+
                            |
                            ▼
                 +-------------------------+
                 | MongoDB Database        |
                 +---------------+---------+
                                 |
               +-----------------+-----------------+
               |                 |                 |
               ▼                 ▼                 ▼
         Police Dashboard   Bank Dashboard   Citizen Dashboard
- ER Diagram
 Users
-----
user_id (PK)
name
email
phone
password
role
created_at
      |
      | 1
      |
      | N
Reports
-------
report_id (PK)
user_id (FK)
report_type
description
status
created_at
      |
      | 1
      |
      | N
Evidence
--------
evidence_id (PK)
report_id (FK)
file_url
evidence_type
uploaded_at

Users
 |
 | 1
 |
 | N
Notifications
-------------
notification_id (PK)
user_id (FK)
title
message
status
created_at

ScamDetection
-------------
scam_id (PK)
report_id (FK)
message
prediction
confidence
risk_score

CurrencyDetection
-----------------
currency_id (PK)
report_id (FK)
image_path
prediction
confidence

VoiceAnalysis
-------------
voice_id (PK)
report_id (FK)
transcript
prediction
confidence

CrimeLocation
-------------
crime_id (PK)
latitude
longitude
city
state
crime_type
risk_level

ChatHistory
-----------
chat_id (PK)
user_id (FK)
question
answer
timestamp

AuditLogs
---------
log_id (PK)
user_id (FK)
action
ip_address
timestamp
