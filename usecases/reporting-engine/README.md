# Decoupled Reporting Engine

## 🧠 Context
Heavy report generation can stress production databases and affect UX. Running reports in the background (with dedicated infra) keeps the app responsive.

## 🎯 Goal
Offload reporting into a separate microservice:
- Connects to read-only replica DB
- Runs reports on schedule or on demand
- Saves output in object storage (e.g. S3)
- Notifies frontend/user via event or webhook

## 🛠 Architecture Sketch
- ReportingRequest event triggered via user or cron
- ReportingService queries data, renders report (CSV, PDF, etc.)
- Output stored + link sent back (via email or notification event)

## ✅ Implementation Tips
- Use Quartz or Hangfire for scheduling
- Separate DB connection string for replicas
- Use templating tools for PDFs (Handlebars, jsPDF, etc.)
