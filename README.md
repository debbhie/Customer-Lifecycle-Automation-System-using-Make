# Customer Lifecycle Automation System using Make

## Overview
This project focuses on designing and implementing an end-to-end customer lifecycle automation system, covering the journey from lead acquisition to customer engagement and retention.

The system automates user tracking, lifecycle stage progression, and communication workflows to ensure timely follow-ups, improve engagement, and reduce churn risk.

It also introduces a structured data model to monitor how quickly users are engaged after signup and how they progress through different lifecycle stages.

## Data Source

The dataset simulates user activity from a B2B SaaS application with both free and paid plans.

User interactions such as:

* signup
* login
* feature usage
* onboarding completion
* inactivity
* upgrade

are captured as events and stored in Airtable.

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
