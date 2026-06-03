# HealthMatch Sage Database Schema Documentation

## Core Tables

1. `profiles` — user profile + role flags (patient/doctor/admin context)
2. `doctors` — provider credentials, specialty, region, verification fields
3. `appointments` — patient-doctor appointment records
4. `appointment_slots` — doctor slot inventory with booking status
5. `health_checks` — symptom analysis and history data
6. `doctor_notifications` — event stream linking checks/appointments/providers
7. `emergency_calls` — Twilio call lifecycle, severity, location metadata

## Relationship Summary
- `appointments.user_id -> profiles.id`
- `appointments.doctor_id -> doctors.id`
- `appointment_slots.user_id -> profiles.id`
- `appointment_slots.doctor_id -> doctors.id`
- `doctor_notifications.appointment_id -> appointments.id`
- `doctor_notifications.health_check_id -> health_checks.id`
- `doctor_notifications.patient_id -> profiles.id`

## Security Model
- Row-Level Security enabled on appointment-related tables.
- Policies include:
  - patients can manage their own appointments
  - doctors can manage assigned appointments/slots
  - authenticated users can view verified doctors

## Query Examples

### Find upcoming patient appointments
```sql
select id, date, time, doctor_name, status
from appointments
where user_id = :user_id
  and date >= current_date
order by date, time;
```

### Find available slots by doctor/date
```sql
select id, start_time, end_time, status
from appointment_slots
where doctor_id = :doctor_id
  and date = :date
  and status = 'available'
order by start_time;
```

### Track critical emergency calls
```sql
select id, patient_name, severity, status, updated_at
from emergency_calls
where severity in ('high', 'critical')
order by updated_at desc;
```
