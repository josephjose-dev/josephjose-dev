# ClinicIQ — Intelligent Clinic Management System

**Project type:** Hackathon prototype  
**Event:** Odoo Buildathon 2026, BITS Pilani Dubai Campus  
**Recognition:** Most Promising Idea  
**Repository:** [josephjose-dev/odoo-hackaathon-CLINICIQ](https://github.com/josephjose-dev/odoo-hackaathon-CLINICIQ)

## Project scope

ClinicIQ is a clinic management module built on Odoo 19 under the Public & Institutional ERP theme. It brings patient records, appointments, prescriptions, and rule-based workflow automation into one application.

The project explores prioritisation and validation within an ERP workflow. Its scores are implemented as explicit formulas rather than trained predictive models.

## Implementation

### Relational data modelling

The module defines seven models: patients, appointments, prescriptions, prescription lines, chronic conditions, allergies, and medicines. Odoo ORM relationships connect appointments and prescriptions to patient records.

### Computed scores

Patient scores combine age, condition severity, missed appointments, and the stored days since a completed visit. Scores are capped at 100 and mapped to four categories.

Appointment no-show scores use missed-appointment history and appointment type. These are heuristic scores, not calibrated probabilities.

### Scheduled workflow automation

Two scheduled actions run at daily intervals. One flags active patients with a score of at least 70; the other marks scheduled or confirmed appointments from earlier dates as missed. The configuration does not explicitly set midnight as the execution time.

### Prescription validation

The issue action rejects prescriptions with no medicine lines or with a detected allergy conflict. The current conflict check compares medicine names with recorded allergy names exactly. It demonstrates a validation workflow; it does not cover all clinical allergy relationships or drug interactions.

### Change tracking

Patient and appointment models use Odoo's mail tracking features. Automatic critical-state changes also post a chatter message. This supports visibility into selected changes, rather than establishing a complete audit of every action.

## Technology

Python, Odoo 19, Odoo ORM with PostgreSQL, XML views, Odoo Scheduled Actions, and Python validation exceptions.

## Recognition

The supplied project README states that ClinicIQ received **Most Promising Idea** at Odoo Buildathon 2026, a multi-university event organised by ACM BPDC, Microsoft Tech Club, and Google Developer Group. The repository includes award and participation materials.

## Engineering lessons

- Computed fields make business rules explicit and connect changes across related records.
- Scheduled actions can automate recurring work inside an existing platform.
- Validation and state transitions belong in backend workflows.
- A prototype's claims should match its implemented behavior and validation evidence.

## Source references

- [Patient model](https://github.com/josephjose-dev/odoo-hackaathon-CLINICIQ/blob/main/models/clinic_patient.py)
- [Appointment model](https://github.com/josephjose-dev/odoo-hackaathon-CLINICIQ/blob/main/models/clinic_appointment.py)
- [Prescription model](https://github.com/josephjose-dev/odoo-hackaathon-CLINICIQ/blob/main/models/clinic_prescription.py)
- [Scheduled actions](https://github.com/josephjose-dev/odoo-hackaathon-CLINICIQ/blob/main/data/clinic_cron.xml)
