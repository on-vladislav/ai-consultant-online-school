# System Architecture

## Overview

The project is an AI-powered consultant for an online English school.

The system combines:

- a public website created in Tilda
- an embedded AI widget created in Voiceflow
- dialog routing and recommendation logic
- lead collection
- Google Sheets integration for storing applications
- Telegram integration for notifying the administrator

The goal of the system is to automate the first stage of communication with potential students.

---

## High-Level Architecture

User
↓
Website (Tilda)
↓
Embedded Voiceflow Widget
↓
AI Router
├── FAQ Scenario
├── Course Recommendation Scenario
└── Lead Collection Scenario
↓
Integrations
├── Google Sheets
└── Telegram


---

# Components

## 1. Website (Tilda)

The website is the client-facing layer of the system.

It includes:

- homepage
- courses and schedule page
- reviews page
- about page

Its main purpose is to present the school and provide entry points to the AI assistant.

Buttons on the website are linked to the widget and open the chat assistant.

---

## 2. Voiceflow Widget

The Voiceflow widget is embedded into the website using JavaScript.

It provides the conversational interface between the user and the AI system.

The widget is published in the production environment.

---

## 3. AI Router

The AI Router is responsible for understanding user intent and redirecting the user to the correct dialog scenario.

Supported intent branches:

- FAQ
- course recommendation
- lead collection

This allows the system to separate dialog logic into smaller modules.

---

## 4. FAQ Scenario

The FAQ scenario handles standard user questions, such as:

- what courses are available
- how the classes are conducted
- what format is used
- schedule-related questions

This branch is designed to reduce the administrator's workload by handling repetitive requests.

---

## 5. Course Recommendation Scenario

The recommendation scenario helps the user choose a course.

The recommendation is based on:

- learning goal
- current language level
- age

The system collects these variables and then recommends the most suitable course.

Core variables used:

- `goal`
- `level`
- `age`
- `course`

---

## 6. Lead Collection Scenario

The lead collection scenario gathers the data necessary for submitting an application.

Collected fields:

- `lead_name`
- `lead_contact`
- `lead_interest`
- `level`
- `age`
- `course`
- `lead_comment`

After collecting the required information, the system forms a lead and sends it to external services.

---

# Integrations

## 7. Google Sheets

Google Sheets is used as a lightweight lead storage system.

Each application is stored as a new row containing:

- date
- user name
- contact
- learning goal
- level
- age
- selected course
- comment
- lead status

This acts as a simple MVP CRM.

---

## 8. Telegram

Telegram is used for administrator notifications.

When a new lead is submitted, the system sends a structured message containing:

- date
- name
- contact
- learning interest
- level
- age
- course
- comment
- lead status

This allows the administrator to react quickly to incoming applications.

---

# Dialog Logic

The conversation is designed as a modular dialog architecture.

Key principles:

- routing by intent
- required variables
- exit conditions
- reusable variables
- production deployment

This makes the system easier to scale and maintain.

---

# Data Flow
User opens the website

User starts the Voiceflow widget

AI Router detects the user’s intent

User enters one of the scenarios:

FAQ

Recommendation

Lead

If a lead is created:

data is written to Google Sheets

admin receives notification in Telegram

User receives confirmation message


---

# Variables Used in the System

## Recommendation variables

- `goal`
- `level`
- `age`
- `course`

## Lead variables

- `lead_name`
- `lead_contact`
- `lead_interest`
- `lead_comment`
- `lead_status`
- `vf_date`

---

# Limitations

The project currently depends on:

- Voiceflow runtime credits
- availability of external APIs
- production publishing of the widget

On the free plan, the assistant may stop responding when runtime credits are exhausted.

---

# Future Improvements

Possible future development:

- CRM integration
- analytics system
- multi-agent architecture
- email automation
- voice interface
- messenger integrations
- improved knowledge base management

---

# Conclusion

The system demonstrates how AI can be embedded into a real business website to automate communication, improve conversion, and reduce manual lead processing.

This project combines prompt engineering, dialog architecture, frontend embedding, and API-based automation into one practical MVP solution.