# fPROG103-BSEM1205-Group-6-Software-Engineering-
MCH Connect is a digital prototype that supports health  bridge the gap between care giver and maternal mothers 
 MCH Connect

Maternal and Child Health Connect — a unified digital platform that equips Community Health Workers (CHWs) and clinic staff with mobile-first tools to register patients, schedule antenatal/postnatal care, capture clinical vitals, and automatically flag danger signs for urgent follow-up.


Built for resource-limited settings: offline-first data capture, automated SMS alerting, and HL7 FHIR-based interoperability with national health information systems (e.g. DHIS2).



Show Image Show Image Show Image


Table of Contents


Overview
Live Prototype
Key Features
Screenshots
System Design
Tech Stack
Project Structure
Getting Started
Functional & Non-Functional Requirements
Database Design
Development Methodology
SDG Alignment
Documentation
Roadmap
Contributing
License



Overview

Community Health Workers are often the only point of contact a pregnant woman has with the health system between formal antenatal appointments — yet most CHWs still rely on paper registers with no automated way to flag danger signs, track missed visits, or report coverage upward. MCH Connect replaces that paper trail with a responsive digital platform purpose-built for the maternal and child health (MCH) care pathway.

The system is designed offline-first: CHWs can register patients and record vitals with zero network connectivity, with data syncing automatically once a connection becomes available.

Live Prototype

An interactive, responsive HTML/JS prototype is included at prototype/mch-connect-prototype.html — open it directly in any browser, no build step required.

It demonstrates all four core modules end-to-end with realistic sample data, an offline/sync simulation, automated risk-alert generation, and a fully responsive layout (sidebar nav on desktop, bottom tab bar on mobile).

Key Features

ModuleDescriptionCHW DashboardLive caseload stats, weekly visit tracker, ANC/PNC coverage ring, and a searchable/filterable patient list with visit-status badges.Registration & VitalsPatient enrolment with auto-generated clinic IDs, plus a vitals form (BP, blood sugar, weight, temperature, fetal heart rate) that checks clinical thresholds live.Appointments & Check-insSchedule ANC/PNC/immunization visits by provider and date; track status through Scheduled → Checked in → Completed.Notifications & AlertsAuto-generated high-risk alerts from out-of-range vitals or missed visits, plus a full SMS reminder/alert log with one-tap batch reminders.

Cross-cutting capabilities:


🔌 Offline-first — an always-visible sync status indicator shows queued vs. synced records.
🚨 Automated risk alerting — vitals are evaluated against configurable thresholds at point of entry.
🔗 Interoperability — data model maps to HL7 FHIR resources for exchange with DHIS2.
🔐 Role-based access — CHW / Nurse / Doctor / Administrator roles scope data access.
📱 Fully responsive — one codebase, from Android phones to desktop clinic consoles.


Screenshots


Place exported PNGs in assets/screenshots/ (see Project Structure) — filenames below match the images already generated for the project documentation.



CHW DashboardRegistration & VitalsShow ImageShow Image

Appointments & Check-insNotifications & AlertsShow ImageShow Image

<p align="center">
  <img src="assets/screenshots/screen-mobile.png" width="260" alt="Mobile responsive view">
</p>
System Design

Full diagrams live in assets/diagrams/ and in the project report (see Documentation).


Use Case Diagram — actors (CHW, Nurse/Doctor, Patient, Administrator, DHIS2) and their interactions with the system. assets/diagrams/usecase.png
Activity Diagram (swimlane) — the visit → vitals → threshold check → alert escalation workflow across CHW, System, and Nurse lanes. assets/diagrams/activity.png
Entity-Relationship Diagram — Users, Patients, Visits, Alerts, Appointments, SMS_Log. assets/diagrams/erd.png
SDLC / Delivery Loop — Accenture-style Plan → Design → Build → Test → Deploy → Operate loop used to plan the build. assets/diagrams/sdlc.png
Delivery Timeline — 19-week planning Gantt chart. assets/diagrams/gantt.png


Tech Stack

Prototype (this repo)


HTML5, CSS3 (custom properties, responsive Grid/Flexbox), vanilla JavaScript — no build step, no external runtime dependencies
In-memory application state (demo data resets on reload)


Target production architecture


Mobile client: Android, offline-first local data store
Web console: clinic/district administrator dashboard
Backend: REST/sync API, threshold-evaluation and SMS orchestration services
Interoperability: HL7 FHIR (Patient, Encounter, Observation resources) ↔ DHIS2
Messaging: SMS gateway for reminders and danger-sign alerts


Project Structure

mch-connect/
├── prototype/
│   └── mch-connect-prototype.html     # Interactive responsive prototype (open directly in browser)
├── docs/
│   └── MCH_Connect_University_Presentation.docx   # Full project report (see Documentation)
├── assets/
│   ├── diagrams/
│   │   ├── usecase.png
│   │   ├── activity.png
│   │   ├── erd.png
│   │   ├── sdlc.png
│   │   ├── gantt.png
│   │   └── impact.png
│   └── screenshots/
│       ├── screen-dashboard.png
│       ├── screen-register.png
│       ├── screen-appointments.png
│       ├── screen-alerts.png
│       └── screen-mobile.png
└── README.md

Getting Started

No build tools or dependencies are required to view the prototype.

bashgit clone https://github.com/<your-org>/mch-connect.git
cd mch-connect
open prototype/mch-connect-prototype.html   # macOS
# or: xdg-open prototype/mch-connect-prototype.html   (Linux)
# or: double-click the file in Explorer          (Windows)

Alternatively, serve it locally:

bashcd prototype
python3 -m http.server 8000
# then visit http://localhost:8000/mch-connect-prototype.html

Use the sync pill in the top bar to simulate going offline — new records queue locally and flush automatically once you toggle back online.

Functional & Non-Functional Requirements

Functional

IDRequirementFR1Register patients with a unique, auto-generated clinic ID.FR2Offline-first data entry for registration and vitals, with automatic sync once online.FR3Automated SMS alerts when recorded vitals breach configured high-risk thresholds.FR4Visual dashboards/reports on coverage, visit adherence, and alert status.FR5Scheduling and status tracking of ANC/PNC/immunization appointments.FR6HL7 FHIR-based data exchange with DHIS2.

Non-Functional

IDRequirementNFR1Interoperability — HL7 FHIR compliance for all external data exchange.NFR2Scalability — concurrent sync from thousands of CHWs without degradation.NFR3Security — encryption at rest and in transit; role-based access control.NFR4Usability — operable by CHWs with limited digital literacy in the field.NFR5Availability — core registration/vitals workflows fully functional offline.

Database Design

Core entities: Users · Patients · Visits · Alerts · Appointments · SMS_Log, with role-based access enforced at the Users entity. Full ERD: assets/diagrams/erd.png.

Development Methodology

Planned using an Accenture-style, agile SDLC: a continuous six-phase loop — Plan & Discover → Design → Build → Test → Deploy → Operate & Optimise — with Build executed as three independent agile sprints (one per functional module) across a 19-week delivery timeline. See assets/diagrams/sdlc.png and assets/diagrams/gantt.png.

SDG Alignment

MCH Connect is scoped against the UN 2030 Agenda for Sustainable Development, primarily:


SDG 3 — Good Health & Well-being (reducing maternal/newborn mortality)
SDG 5 — Gender Equality
SDG 9 — Industry, Innovation & Infrastructure
SDG 10 — Reduced Inequalities
SDG 17 — Partnerships for the Goals


See assets/diagrams/impact.png for projected coverage impact and relative SDG contribution.

Documentation

The full project report — abstract, problem definition, UML models, system/database design, SDG alignment, screen-by-screen analysis, and requirements — is available at docs/MCH_Connect_University_Presentation.docx.

Roadmap


 Wire the prototype to a persistent backend (replace in-memory state)
 Implement real offline storage/sync (e.g. IndexedDB + background sync)
 Build the HL7 FHIR / DHIS2 integration layer
 Native Android client for field CHWs
 Pilot deployment at a single clinic catchment area
 Admin/DHIS2 export view and role-based login


Contributing

Issues and pull requests are welcome. Please open an issue to discuss significant changes before submitting a PR.

License

License to be determined by the project owner. Add a LICENSE file to this repository to specify usage terms.
