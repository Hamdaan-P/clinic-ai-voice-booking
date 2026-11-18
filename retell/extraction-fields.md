# Retell AI: Post Call Extraction Fields

After each call, Retell analyses the transcript and extracts these fields.
They arrive in the webhook payload at `call → call_analysis → custom_analysis_data`.

| Field | Type | What it captures | Example (test data) |
|---|---|---|---|
| `patient_name` | Text | Caller's full name | Suraj Kumar |
| `patient_phone` | Text | 10-digit mobile number, no +91 | 9XXXXXXXXX |
| `chief_complaint` | Text | Reason for the visit | Fever and headache |
| `appointment_date` | Text | Chosen date, YYYY-MM-DD | 2026-10-06 |
| `appointment_time` | Text | Chosen time, 24-hour HH:MM | 14:00 |

## Design notes

- The webhook fires on `call_analyzed`, **not** `call_ended`. `call_ended` fires before extraction finishes, so the custom fields would be missing.
- Retell's dashboard "Test" webhook sends a sample without custom fields, so Make.com had to learn the data structure from a real test call.
