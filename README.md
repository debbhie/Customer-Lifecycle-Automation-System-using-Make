# Customer Lifecycle Automation System using Make

## Overview
This project focuses on designing and implementing an end-to-end customer lifecycle automation system, covering the journey from lead acquisition to customer engagement and retention.

The system automates user tracking, lifecycle stage progression, and communication workflows to ensure timely follow-ups, improve engagement, and reduce churn risk.

It also introduces a structured data model to monitor how quickly users are engaged after signup and how they progress through different lifecycle stages.

## Data Source

The dataset simulates user activity from a B2B SaaS application with both free and paid plans.
<img width="2560" height="1600" alt="user" src="https://github.com/user-attachments/assets/df209459-70c9-4734-98f0-904a40eab490" />

User interactions such as:

* signup
* login
* feature usage
* onboarding completion
* inactivity
* upgrade

are captured as events and stored in Airtable.
<img width="2560" height="1600" alt="event" src="https://github.com/user-attachments/assets/c072e7c9-54b8-4467-9d5e-40a41ab2727b" />

Synthetic data was used to simulate realistic user behavior and test the automation system under varying conditions.

## Problem Statement

The objective of this project is to design a fully automated lifecycle system that ensures users who sign up for the application are properly tracked, engaged, and followed up.

Many systems fail due to:

* Delayed or inconsistent follow-ups
* Lack of visibility into user engagement
* Inability to track lifecycle progression

This project addresses these gaps by automating lifecycle transitions, scoring user activity, and triggering timely communication based on user behavior.

## System Design & KPI Framework

The system is built around tracking user activity and translating it into actionable lifecycle insights.

Key components:
* Event Tracking
* User actions are captured in an Event table and categorized by type (e.g., signup, feature usage, inactivity).
* Event Scoring System
* Each event type is assigned a value to represent user engagement level.
* User-Level Aggregation
* Event scores are rolled up into the Users table to calculate an overall engagement or usage score.
* Lifecycle Progression
  
- Based on user activity and scores, users are automatically moved across lifecycle stages such as:
  *  New Signup
  * Onboarding
  * Engaged
  * Power User
  * Churn Risk
- Lifecycle Logging
  * All stage transitions are recorded in a Lifecycle Log table for visibility and auditing.
  * Automated Messaging
  * Emails are triggered based on lifecycle stage and logged in a Message table to track communication history.
 
  ## Automation Architecture
- Scenario 1: Lifecycle Management (Airtable)

This scenario monitors user activity and updates lifecycle stages dynamically.

Workflow:

  * Trigger: New or updated event in Airtable
  * Identify event type (e.g., signup, feature_used, inactivity_detected)
  * Assign value based on event type
  * Update user’s cumulative engagement score
  * Evaluate lifecycle stage based on defined thresholds
  * Update the user’s lifecycle stage
  * Log the transition in the Lifecycle Log table

 This ensures that lifecycle progression is data-driven and continuously updated.
 <img width="2560" height="1600" alt="log" src="https://github.com/user-attachments/assets/d6b4b35c-84d8-447e-aaab-25c8d82d6f9b" />


- Scenario 2: Communication Automation (Airtable + Gmail)

This scenario handles lifecycle-based email communication.

<img width="2560" height="1362" alt="1" src="https://github.com/user-attachments/assets/5cd62d37-7eea-4cd0-b23e-68c8f3c261c8" />

Workflow:

  * Trigger: Change in lifecycle stage
  * Retrieve user details (email, name, stage)
  * Identify appropriate message template based on lifecycle stage
  * Send personalized email via Gmail
  * Log the message in the Message table with:
    * Date sent
    * Status
    * Lifecycle stage
    * Subject
    * Message type
    * User ID
<img width="2447" height="1346" alt="prod email" src="https://github.com/user-attachments/assets/47ebb811-8fdb-48cb-a767-710391591377" />

 This ensures:

* Timely follow-ups
* Consistent communication
* Full visibility into messaging activity
  
<img width="2560" height="1362" alt="1" src="https://github.com/user-attachments/assets/f4a764ec-979c-4f65-95af-01895d9bf7b5" />


<img width="2560" height="1596" alt="Message" src="https://github.com/user-attachments/assets/d5b8998f-61a4-430a-a6ba-dfc079989c63" />

## Key Insights

* User behavior is diverse, with events such as feature usage, onboarding completion, and inactivity indicating different engagement levels.
* Lifecycle transitions are effectively captured, showing users progressing between stages such as New Signup, Onboarding, and Engaged.
* Communication coverage is not uniform, as not all users receive lifecycle emails, highlighting potential gaps in trigger conditions or timing.
* Event-to-message mismatch exists, where some users generate activity without corresponding communication, indicating opportunities to improve follow-up logic.
* Timing of engagement varies, suggesting that response speed and automation timing can be optimized further.

## Recommendations
* Improve email coverage logic
* Ensure all users entering key lifecycle stages receive appropriate communication.
* Introduce SLA-based triggers
* Add time-based conditions (e.g., send email if no activity after X days).
* Enhance lifecycle scoring model
* Refine event weights to better reflect user intent and engagement.
* Implement monitoring dashboard
  Track KPIs such as:
  * email coverage rate
  * time to first engagement
  * lifecycle progression rate
* Add fallback/error handling
Log missing data or failed triggers to improve system reliability.
