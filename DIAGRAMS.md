# HealthMatch Sage Diagram Catalog

## 1) System Architecture Diagram
```
[React SPA] --> [Supabase Auth] --> [Postgres + RLS]
     |                |                    |
     +--> [Edge Functions: Gemini + Twilio Integrations]
```

## 2) User Authentication Flow
```
User -> Login UI -> Supabase Auth -> Session
Session -> AuthContext -> RequireAuth -> Protected Routes
```

## 3) Appointment Booking Workflow
```
Select Doctor -> View Slots -> [Available?]
                     | yes             | no
                 Book Slot        Suggest Alternatives
```

## 4) Data Flow Diagram (L0/L1/L2)
```
L0: Patient/Doctor/Admin <-> HealthMatch Core
L1: Core <-> Auth, Scheduling, AI, Emergency
L2: Emergency <-> Twilio Gather <-> Supabase updates
```

## 5) Entity Relationship Diagram
```
profiles 1--* appointments *--1 doctors
profiles 1--* health_checks
appointments 1--* doctor_notifications
profiles 1--* emergency_calls
```

## 6) Use Case Diagram (Roles)
- **Patient**: signup/login, health check, appointments, emergency, report analysis
- **Provider**: manage slots, view assigned appointments, process notifications
- **Admin**: verify doctors, governance oversight, monitor KPIs

## 7) API Request/Response Flow
```
Client -> /functions/v1/analyze-symptoms -> Gemini
Client -> /functions/v1/emergency-call -> Twilio Call API
Twilio webhooks -> /functions/v1/call-status-webhook
```

## 8) Database Schema Diagram
- Tables: `profiles`, `doctors`, `appointments`, `appointment_slots`, `health_checks`, `doctor_notifications`, `emergency_calls`
- Relationships enforced through foreign keys + RLS policies.

## 9) Deployment Pipeline
```
Code Commit -> Build -> Vercel Deploy
                |
         Supabase Functions + Migrations Deploy
```

## 10) State Machine (Appointment)
```
available -> booked -> completed
              |
           cancelled
```

## 11) Component Hierarchy
```
App
└── AuthProvider
    └── MainLayout
        ├── Dashboard
        ├── HealthCheck
        ├── Appointments
        └── Emergency / MedicalReports
```

## 12) Security Architecture
- JWT auth sessions
- Route guards (`RequireAuth`)
- Supabase Row-Level Security policies
- Secret-managed integrations for Gemini/Twilio

## 13) Critical Sequence Diagram
```
Patient -> HealthCheck -> analyze-symptoms -> Response
Patient -> Appointment -> DB slot reserve -> Notification
Patient -> Emergency -> Twilio gather -> Call completion
```

## 14) Network Topology
```
Browser <-> Vercel Frontend <-> Supabase API/Postgres
                           <-> Supabase Edge Functions
                               <-> Gemini / Twilio
```

## 15) Gantt Chart (High-Level)
```
Planning | Design | Build | Test | Security | Deploy | Documentation
```
