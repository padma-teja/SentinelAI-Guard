# AI Models

DistilBERT
YOLOv8
Whisper
XGBoost
OpenCV

Each model is documented with its purpose and integration.
AI Models Used in SentinelAI Guard

SentinelAI Guard integrates multiple Artificial Intelligence models to detect and prevent cyber fraud, counterfeit currency, digital arrest scams, phishing attacks, and voice-based scams. Each model is selected based on its strengths in solving a specific problem.
| AI Model       | Purpose                                                                           | Input                               | Output                                    | Integration in SentinelAI Guard                                                                                   |
| -------------- | --------------------------------------------------------------------------------- | ----------------------------------- | ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **DistilBERT** | Detect scam messages, phishing emails, WhatsApp chats, and digital arrest scripts | SMS, Email, Chat, Text              | Scam / Genuine + Confidence Score         | Used in the Scam Detection module to classify suspicious text and generate AI explanations.                       |
| **YOLOv8**     | Detect counterfeit currency and security features in banknotes                    | Currency Image                      | Real / Fake + Bounding Boxes + Confidence | Used in the Currency Detection module for real-time note analysis on uploaded or camera-captured images.          |
| **Whisper**    | Convert speech into text for scam analysis                                        | Voice Recording                     | Transcript                                | Used in the Voice Analysis module to transcribe suspicious calls before AI classification.                        |
| **XGBoost**    | Calculate fraud risk and generate threat scores                                   | AI outputs, metadata, user activity | Risk Score (0–100)                        | Acts as the centralized Risk Engine by combining outputs from all AI modules to produce an overall threat level.  |
| **OpenCV**     | Image preprocessing and feature extraction                                        | Images (Currency, QR Code)          | Enhanced Images & Features                | Used before YOLOv8 for image enhancement, edge detection, cropping, QR decoding, and security feature extraction. |

Model Integration Workflow
                User Input
                     │
     ┌───────────────┼────────────────┐
     │               │                │
     ▼               ▼                ▼
 Text Message     Currency Image   Voice Recording
     │               │                │
     ▼               ▼                ▼
 DistilBERT      OpenCV          Whisper
     │               │                │
     ▼               ▼                ▼
 Scam Result    Processed Image   Transcript
                     │                │
                     ▼                ▼
                  YOLOv8        DistilBERT
                     │                │
          Counterfeit Result   Scam Classification
                     └───────┬──────────────┘
                             ▼
                        XGBoost Risk Engine
                             │
                             ▼
              Threat Score + Confidence + Recommendation
                             │
                             ▼
                 Dashboard, Reports & Alerts
AI Pipeline
User Input
     │
     ▼
Input Validation
     │
     ▼
AI Model Selection
     │
     ▼
Model Inference
     │
     ▼
Risk Engine (XGBoost)
     │
     ▼
Threat Analysis
     │
     ▼
Dashboard & Report Generation
