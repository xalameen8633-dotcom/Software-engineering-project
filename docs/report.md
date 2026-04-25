# Maintenance Management System (MMS)
## Software Engineering Project Report

**Group Number:** 01  
**Course:** Software Engineering  
**Semester:** Fall 2025  
**Instructor:** Dr. Samer Elkababji  

## Group Members

| Student ID | Name | Commit Count |
|---|---|---:|
| [ID] | Osama | [count] |
| [ID] | Mira | [count] |
| [ID] | Zina | [count] |
| [ID] | Zakarea | [count] |

**GitHub Repository URL:**  
https://github.com/xalameen8633-dotcom/Software-engineering-project

**Version Information:**  
v1.0.0: Initial report version  
v2.0.0: Updated version with diagrams and descriptions  

---

# 1. Project Overview

The **Maintenance Management System (MMS)** is a database-driven and sensor-integrated system designed to manage **preventive, corrective, and predictive maintenance** activities in industrial, commercial, or institutional environments. The system enables technicians to log maintenance requests, supervisors to review and assign work orders, and administrators to monitor maintenance performance through dashboards and KPI reports.

In addition, the system integrates with **IoT sensors** that continuously monitor equipment conditions such as temperature, vibration, and pressure. When abnormal readings are detected, the system can generate predictive alerts and automatically create maintenance requests. This helps organizations reduce downtime, improve maintenance planning, and increase operational efficiency.

## 1.1 System Purpose

The MMS serves multiple stakeholders:

- **Technician:** Logs maintenance requests, views assigned work orders, updates work progress, and submits work order completion.
- **Supervisor:** Reviews maintenance requests, approves or rejects requests, assigns technicians, monitors work order progress, and confirms closure.
- **Administrator:** Monitors dashboards, KPIs, and maintenance reports.
- **IoT Sensors:** Send abnormal sensor readings to the system for predictive maintenance detection.
- **Notification Service:** Sends alerts and work order notifications to relevant users.

## 1.2 System Scope

The system covers the following functional areas:

- Logging corrective maintenance requests
- Monitoring sensor readings for predictive maintenance
- Generating predictive alerts
- Automatically creating maintenance requests
- Approving and assigning work orders
- Tracking work order progress
- Recording labour and spare parts used
- Confirming and closing completed work orders
- Monitoring KPIs and dashboards
- Sending maintenance notifications

---

# 2. Context Diagrams and Activity Diagram

## 2.1 Context Model

The **C4 Level 1 Context Diagram** defines the Maintenance Management System boundary and illustrates its interactions with main users and external systems. All interacting entities are categorized according to their roles and responsibilities.

![C4 Level 1 Context Diagram](../out/UML/c4_L1_context/c4_L1_context.png)

### Internal Users
- **Technician:** Logs maintenance requests, views assigned work orders, and submits completion updates.
- **Supervisor:** Reviews requests, approves them, assigns work orders, tracks progress, and closes requests.
- **Administrator:** Monitors maintenance KPIs and generates reports.

### External Systems
- **IoT Sensors:** Provide abnormal readings related to equipment condition.
- **Notification Service:** Sends alerts and assignment notifications to supervisors and technicians.

The context model establishes the overall system boundary and shows how the MMS acts as the central platform coordinating maintenance operations between human users and external services.

## 2.2 Activity Diagram

The activity diagram illustrates the predictive maintenance workflow with swimlanes representing the main participants in the process.

![Activity Diagram](../out/UML/activity_diagram/activity_diagram.png)

### Key Activities
1. IoT sensors send abnormal sensor readings.
2. The system analyzes the readings and generates a predictive alert.
3. A predictive maintenance request is automatically created.
4. The supervisor is notified and reviews the request.
5. If approved, a technician is assigned.
6. The technician performs the maintenance work and submits completion.
7. The supervisor reviews the result and either closes the work order or requests rework.
8. The administrator monitors the updated KPIs and dashboards.

This activity diagram describes the end-to-end predictive maintenance workflow in the Maintenance Management System. The process begins when IoT sensors detect an abnormal reading and forward it to the system. The system evaluates the reading, creates a predictive maintenance request, and notifies the supervisor. After the supervisor reviews and approves the request, a technician is assigned to perform the maintenance task. Once the task is completed, the technician submits the work results, and the supervisor either confirms closure or returns the work for reprocessing. The process ensures that predictive maintenance requests are handled systematically and that maintenance performance is reflected in the system dashboards.

---

# 3. Use Case Models and Interaction Design

## 3.1 Selected Primary Actors

The primary actors selected from the context model are:

- **Technician**
- **Supervisor**
- **Administrator**
- **IoT Sensors**

From the context diagram, these actors interact with the Maintenance Management System to perform the core maintenance operations. Based on these interactions, the following UML artefacts have been produced:

- **Composite use case diagram** for the Maintenance Management System
- **Sequence diagram – High-Level (Stakeholders)**
- **Sequence diagram – Detailed (Developers)**

These diagrams are consistent with the context view, which shows that technicians, supervisors, administrators, and IoT sensors all interact with MMS in different ways to support maintenance workflows.

## 3.2 Composite Use Case Diagram

The composite use case diagram shows the main use cases supported by the Maintenance Management System.

![Use Case Diagram](../out/UML/usecase/use_case.png)

The use case diagram shows that the system supports:
- Logging maintenance requests
- Viewing assigned work orders
- Reviewing maintenance requests
- Approving or rejecting requests
- Assigning technicians
- Tracking work order progress
- Submitting work order completion
- Recording labour and parts used
- Sending notifications
- Monitoring dashboards and KPIs
- Processing sensor readings
- Generating predictive alerts
- Auto-creating maintenance requests

## 3.3 Use Case Descriptions

The tabular use case descriptions for the Maintenance Management System are provided in a separate file:

`docs/use_case_descriptions.md`

These descriptions define the use case name, actors, goal, preconditions, postconditions, main success scenario, and alternative flows for the main system functions.

---

# 4. Sequence Diagrams

## 4.1 High-Level Sequence Diagram

This sequence diagram shows the stakeholder-level interaction for the predictive maintenance workflow.

![Sequence Diagram High Level](../out/UML/sequence-stakeholders/sequence_highlevel.png)

### Key Interactions
1. IoT sensors send abnormal sensor readings to the system.
2. The system analyzes the reading and creates a predictive maintenance request.
3. The supervisor is notified of the new request.
4. The supervisor reviews the request and approves it.
5. The system assigns the work order to a technician.
6. The technician performs the maintenance and submits completion.
7. The supervisor reviews the result and closes the work order.
8. The administrator views updated KPI dashboards.

This high-level sequence diagram presents the predictive maintenance workflow from a business and stakeholder perspective. It emphasizes the interactions between IoT sensors, the Maintenance Management System, the supervisor, the technician, and the administrator. The diagram captures the major workflow events without focusing on internal implementation details.

## 4.2 Detailed Sequence Diagram

The detailed sequence diagram provides the developer-level interaction of the Maintenance Management System. It shows the internal communication between the technical components involved in handling predictive maintenance requests.

![Sequence Diagram Detailed](../out/UML/sequence-developers/sequence_detailed.png)

The detailed sequence diagram includes interactions between:
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

This developer-level diagram explains how sensor data flows through the system, how abnormal readings are evaluated, how predictive maintenance requests are created and stored, how notifications are generated, and how user actions update the work order lifecycle. Compared with the stakeholder-level diagram, this version provides more technical detail about the system internals, database operations, and notification flow.

---