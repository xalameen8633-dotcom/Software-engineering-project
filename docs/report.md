# Maintenance Management System (MMS)
## Software Engineering Project Report

**Group Number:** 01  
**Course:** Software Engineering  
**Semester:** Spring 2026  
**Instructor:** Dr. Samer Elkababji  

## Group Members

| Student ID | Name | Commit Count |
|---|---|---:|
| 20210611   | Osama | 15 |
| 20210748   | Mira | 15 |
| 20210853   | Zina | 1 |
| 20220637   | Zakarea | 1 |

**GitHub Repository URL:**  
https://github.com/xalameen8633-dotcom/Software-engineering-project

**Version Information:**  
v1.0.0: Initial report version  

---

# 1. Project Overview

The Maintenance Management System (MMS) is a database-driven, sensor-integrated platform built to handle preventive, corrective, and predictive maintenance in industrial, commercial, or institutional environments. It gives technicians a way to log maintenance requests, lets supervisors review and assign work orders, and provides administrators with dashboards and KPI reports to keep track of overall maintenance performance.

One of the more interesting parts of the system is its IoT integration. Sensors attached to equipment continuously monitor conditions like temperature, vibration, and pressure. When a reading goes outside the normal range, the system automatically generates a predictive alert and creates a maintenance request without anyone having to manually report it. This helps catch problems early and reduces unexpected downtime.

## 1.1 System Purpose

The MMS is designed around five main roles:

- **Technician:** Logs corrective maintenance requests, views their assigned work orders, performs maintenance tasks in the field, and submits work order completion reports including labour hours and parts used.
- **Supervisor:** Reviews incoming maintenance requests, approves or rejects them, assigns technicians to work orders, monitors progress, and confirms closure once the work is done.
- **Administrator:** Monitors system-wide dashboards, KPI metrics, and maintenance reports.
- **IoT Sensors:** Continuously send equipment readings to the system so that abnormal conditions can be detected automatically.
- **Notification Service:** Handles delivery of email and SMS alerts to the right people at each stage of the workflow.

## 1.2 System Scope

The MMS covers the following functional areas:

- Logging corrective maintenance requests manually by technicians
- Monitoring IoT sensor readings for predictive maintenance detection
- Generating predictive alerts when thresholds are exceeded
- Automatically creating maintenance requests from sensor alerts
- Reviewing, approving, and rejecting maintenance requests
- Assigning and tracking work orders
- Submitting work order completion with labour hours and parts used
- Handling rework when completed work is unsatisfactory
- Confirming and closing work orders
- Monitoring KPIs and maintenance dashboards
- Sending notifications at each workflow event

---

# 2. Context Diagrams and Activity Diagram

## 2.1 Context Model

The C4 Level 1 Context Diagram shows the overall boundary of the Maintenance Management System and how it connects to the people and external systems that interact with it.

![C4 Level 1 Context Diagram](../out/UML/c4_L1_context/c4_L1_context.png)

### Internal Users
- **Technician:** Logs maintenance requests, views assigned work orders, and submits completion reports.
- **Supervisor:** Reviews requests, approves or rejects them, assigns work orders to technicians, tracks progress, and closes completed orders.
- **Administrator:** Monitors maintenance KPIs and views reports through the system dashboards.

### External Systems
- **IoT Sensors:** Send equipment condition readings (temperature, vibration, pressure) to the system for automated analysis.
- **Notification Service:** Delivers email and SMS notifications to technicians, supervisors, and administrators at key points in the workflow.

The context diagram establishes the system boundary and shows how the MMS sits at the center of the maintenance workflow, connecting field technicians, supervisors, administrators, and automated IoT-driven processes.

## 2.2 Container Model

The C4 Level 2 Container Diagram breaks down the internals of the MMS and shows how its technical components communicate with each other and with external systems.

![C4 Level 2 Container Diagram](../out/UML/c4_L2_container/c4_L2_container.png)

The system is made up of the following containers:

- **Web Application:** A browser-based interface used by technicians, supervisors, and administrators to interact with the system.
- **Mobile App:** A mobile interface aimed primarily at field technicians who need to receive and update work orders while on-site.
- **Backend API:** The core of the system. It handles authentication, maintenance requests, work orders, equipment records, spare parts inventory, and KPI calculations. All status updates and data writes go through this component.
- **Central Database:** Stores everything — work orders, equipment records, maintenance history, spare parts, alerts, users, and KPI data.
- **IoT Gateway:** Acts as the entry point for sensor data. It receives raw MQTT payloads from IoT devices and normalizes them before passing them on.
- **Alert Engine:** Reads threshold configurations from the database and evaluates incoming sensor events. When a reading exceeds a threshold, it triggers the Backend API to create a predictive maintenance request.
- **Notification Service:** An external service that receives triggers from the Backend API and delivers email or SMS messages to the relevant users.

Technicians, supervisors, and administrators interact with the system through the Web Application (or the Mobile App for field technicians). Both applications communicate with the Backend API over REST/JSON. The Backend API reads and writes to the Central Database and calls the Notification Service when workflow events occur.

The IoT pipeline is separate from the main user-facing flow. Sensors publish readings via MQTT to the IoT Gateway, which normalizes the data and forwards it to the Alert Engine. The Alert Engine checks the reading against stored thresholds and, if needed, calls the Backend API to create a maintenance request automatically.

## 2.3 Activity Diagram

The activity diagram shows the end-to-end predictive maintenance workflow using swimlanes to separate the responsibilities of each participant.

![Activity Diagram](../out/UML/activity_diagram/activity_diagram.png)

### Key Activities
1. An IoT sensor detects an abnormal reading and publishes it via MQTT.
2. The IoT Gateway normalizes the payload and forwards it to the Alert Engine.
3. The Alert Engine compares the reading against the configured threshold.
4. If the threshold is exceeded, a predictive alert is generated and the Backend API automatically creates a maintenance request.
5. The supervisor is notified and reviews the request.
6. If approved, the supervisor assigns a technician and the work order is issued.
7. The technician receives the assignment, performs the maintenance, and submits a completion report.
8. The Backend API records the maintenance history, updates the inventory and equipment status, and notifies the supervisor.
9. The supervisor reviews the result and either closes the work order or sends it back for rework.
10. If rework is needed, the technician is notified, performs additional work, and resubmits. The supervisor then reviews again and closes the order.
11. Once closed, KPI metrics are updated and the administrator can view the updated dashboards.

---

# 3. Use Case Models and Interaction Design

## 3.1 Selected Primary Actors

The primary actors for this system, taken from the context model, are:

- **Technician**
- **Supervisor**
- **Administrator**
- **IoT Sensors**

These are the actors that directly initiate or participate in the system's main use cases. Based on their interactions with the MMS, we produced the following UML artefacts:

- Composite use case diagram
- High-level sequence diagram (stakeholders)
- Detailed sequence diagram (developers)

All three artefacts are consistent with the context model and reflect the same set of actors and workflows.

## 3.2 Composite Use Case Diagram

The use case diagram shows all the main use cases supported by the Maintenance Management System and how they relate to each actor.

![Use Case Diagram](../out/UML/usecase/use_case.png)

The diagram covers the following use cases:

- Logging corrective maintenance requests
- Viewing assigned work orders
- Submitting work order completion (including recording labour and parts used)
- Reviewing maintenance requests
- Approving or rejecting requests
- Assigning work orders to technicians
- Tracking work order progress
- Confirming and closing work orders
- Monitoring KPI dashboards
- Viewing maintenance reports
- Processing IoT sensor readings
- Generating predictive alerts
- Auto-creating maintenance requests from alerts
- Sending notifications

## 3.3 Use Case Descriptions

The tabular use case descriptions for the Maintenance Management System are provided in a separate file:

`docs/use_case_descriptions.md`

Each entry includes the use case name, actors involved, preconditions, postconditions, main success scenario, and alternative flows.

---

# 4. Sequence Diagrams

## 4.1 High-Level Sequence Diagram

This diagram shows the predictive maintenance workflow from the perspective of the stakeholders, without going into internal system details.

![Sequence Diagram High Level](../out/UML/sequence-stakeholders/sequence_highlevel.png)

### Key Interactions
1. An IoT sensor sends an abnormal reading to the MMS.
2. The system analyzes the reading, generates a predictive alert, and automatically creates a maintenance request.
3. The supervisor is notified and reviews the request.
4. The supervisor approves the request and assigns a technician.
5. The technician acknowledges the work order, performs the maintenance, and submits the completion report.
6. The supervisor is notified and reviews the completed work order.
7. If the work is satisfactory, the supervisor closes the order and the administrator sees the updated KPI dashboard.
8. If the work is unsatisfactory, the supervisor sends it back for rework. The technician receives the rework notification, performs the additional work, and resubmits. The supervisor then reviews and closes the order.
9. If the request is rejected from the start, the supervisor rejects it and receives a confirmation.

The high-level diagram focuses on the business flow and stakeholder interactions rather than how the system handles things internally. It gives a clear picture of who is responsible for each step.

## 4.2 Detailed Sequence Diagram

The detailed diagram shows the same workflow but at the developer level, including the internal communication between system components.

![Sequence Diagram Detailed](../out/UML/sequence-developers/sequence_detailed.png)

The participants in this diagram are:

- **IoT Sensors**
- **IoT Gateway / MQTT Broker**
- **Alert Engine**
- **Web Application**
- **Backend API**
- **Central Database**
- **Notification Service**
- **Supervisor**
- **Technician**
- **Administrator**

This diagram traces how sensor data flows from the IoT Gateway through the Alert Engine and into the Backend API, how maintenance requests and work orders are stored in the database, how notifications are triggered at each step, and how user actions through the Web Application drive the work order lifecycle. It also covers the rework path in full — from the supervisor reopening the work order, through the technician resubmitting, to the supervisor closing it after a second review.

Compared to the stakeholder diagram, this version is more useful for developers as it shows the specific API calls, data passed between components, and the exact sequence of database operations performed by the Backend API.

---
