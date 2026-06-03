# HealthMatch Sage API Specification

## Authentication and Session
- Client uses Supabase Auth through `@supabase/supabase-js`.
- Protected routes enforced in `RequireAuth` and `AuthContext`.

## Supabase Edge Functions

### `POST /functions/v1/analyze-symptoms`
**Purpose:** AI-powered differential analysis from symptoms.

**Request (JSON):**
```json
{
  "symptoms": ["fever", "headache"],
  "severity": "medium",
  "duration": "2 days",
  "height": 172,
  "weight": 70,
  "previousConditions": ["asthma"],
  "medications": ["paracetamol"]
}
```

**Response (JSON excerpt):**
```json
{
  "conditions": [
    {
      "name": "Viral Infection",
      "diagnosticConfidence": "Moderate",
      "urgencyLevel": "Low"
    }
  ],
  "overallClinicalAssessment": {
    "urgencyClassification": "moderate"
  }
}
```

### `POST /functions/v1/analyze-medical-report`
**Purpose:** Parses uploaded report (image/pdf) and returns structured interpretation.

**Request (JSON):**
```json
{
  "file": "base64-data",
  "fileName": "cbc-report.pdf",
  "fileType": "application/pdf",
  "language": "simple-english"
}
```

### `POST /functions/v1/emergency-call`
**Purpose:** Initiates Twilio call and creates `emergency_calls` record.

### `POST /functions/v1/call-status`
**Purpose:** Fetches Twilio call status by SID.

### `POST /functions/v1/call-status-webhook`
**Purpose:** Twilio callback to persist call progress.

### `POST /functions/v1/collect-symptoms`
### `POST /functions/v1/collect-severity`
### `POST /functions/v1/collect-location`
**Purpose:** TwiML call-flow gather endpoints for emergency triage.

### `GET /functions/v1/call-twiml`
**Purpose:** Returns TwiML script that drives voice prompts.

### `POST /functions/v1/groq-chat`
**Purpose:** Conversational inference endpoint backed by Groq-compatible API.

## Reliability/Security Notes
- CORS headers are configured on edge functions.
- Sensitive keys are loaded from environment variables.
- Clinical outputs include explicit disclaimers for professional review.
