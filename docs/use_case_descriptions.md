# Use Case Descriptions — Maintenance Management System

---

## UC1 — Log Maintenance Request

| Field | Description |
|---|---|
| **Use Case ID** | UC1 |
| **Use Case Name** | Log Maintenance Request |
| **Actor(s)** | Technician |
| **Description** | A technician manually submits a new corrective maintenance request describing a fault or issue observed on a piece of equipment. |
| **Preconditions** | Technician is authenticated. Equipment record exists in the system. |
| **Postconditions** | A maintenance request is created with status "Pending" and the supervisor is notified via the Notification Service. |
| **Main Flow** | 1. Technician opens the maintenance request form. 2. Technician selects the equipment and describes the fault. 3. Technician submits the request. 4. System stores the request with status "Pending". 5. System notifies the supervisor (UC15). |
| **Alternative Flow** | 3a. Required fields are missing → system displays validation error; technician corrects and resubmits. |
| **Includes** | UC15 (Send Notifications) |

---

## UC2 — View Assigned Work Orders

| Field | Description |
|---|---|
| **Use Case ID** | UC2 |
| **Use Case Name** | View Assigned Work Orders |
| **Actor(s)** | Technician |
| **Description** | A technician views the list of work orders currently assigned to them, including job details, equipment information, and required spare parts. |
| **Preconditions** | Technician is authenticated. At least one work order is assigned to the technician. |
| **Postconditions** | Technician views the full details of their assigned work orders. |
| **Main Flow** | 1. Technician navigates to the Work Orders section. 2. System retrieves and displays all work orders assigned to the technician. 3. Technician selects a work order to view its full details including equipment info and required spare parts. |
| **Alternative Flow** | 2a. No work orders assigned → system displays an empty state message. |
| **Includes** | — |

---

## UC3 — Submit Work Order Completion

| Field | Description |
|---|---|
| **Use Case ID** | UC3 |
| **Use Case Name** | Submit Work Order Completion |
| **Actor(s)** | Technician |
| **Description** | After performing maintenance, a technician submits a completion report through the web or mobile application, providing labour hours, parts used, and notes. The Backend API is then responsible for recording the maintenance history, updating the spare parts inventory, updating equipment status, and setting the work order status to "Completed". |
| **Preconditions** | Technician is authenticated. Work order is in "Assigned" status and assigned to this technician. |
| **Postconditions** | Completion data is submitted by the technician. The Backend API records the maintenance history, deducts used parts from inventory, updates equipment status to "Operational", and sets work order status to "Completed". Supervisor is notified (UC15). |
| **Main Flow** | 1. Technician opens the assigned work order. 2. Technician fills in labour hours, parts used, and completion notes (UC4). 3. Technician submits the completion report via the application. 4. Backend API records the maintenance history entry. 5. Backend API deducts used spare parts from inventory. 6. Backend API updates equipment status to "Operational". 7. Backend API sets work order status to "Completed". 8. Backend API notifies the supervisor (UC15). |
| **Alternative Flow** | 3a. Submission fails due to a server error → system displays an error message; technician retries. |
| **Includes** | UC4 (Record Labour and Parts Used), UC15 (Send Notifications) |

---

## UC4 — Record Labour and Parts Used

| Field | Description |
|---|---|
| **Use Case ID** | UC4 |
| **Use Case Name** | Record Labour and Parts Used |
| **Actor(s)** | Technician |
| **Description** | As part of submitting work order completion (UC3), a technician records the labour hours spent and the spare parts consumed during the maintenance activity. |
| **Preconditions** | Technician is authenticated. Work order is open and assigned to the technician. Spare parts records exist in the inventory. |
| **Postconditions** | Labour hours and parts used are included in the completion submission. The Backend API will deduct the used parts from inventory upon submission. |
| **Main Flow** | 1. Technician opens the work order completion form (as part of UC3). 2. Technician enters labour hours. 3. Technician selects parts used and specifies quantities consumed. 4. Labour and parts data are included in the completion submission sent to the Backend API. |
| **Alternative Flow** | 3a. Requested part quantity exceeds available stock → system warns the technician; technician adjusts the quantity or flags a shortage. |
| **Includes** | — |

---

## UC5 — Review Maintenance Requests

| Field | Description |
|---|---|
| **Use Case ID** | UC5 |
| **Use Case Name** | Review Maintenance Requests |
| **Actor(s)** | Supervisor |
| **Description** | A supervisor views all pending maintenance requests (both manually submitted by technicians and auto-generated from IoT predictive alerts) to assess their details and priority. |
| **Preconditions** | Supervisor is authenticated. At least one maintenance request exists with status "Pending". |
| **Postconditions** | Supervisor has reviewed the request details and is ready to approve or reject. |
| **Main Flow** | 1. Supervisor navigates to the Maintenance Requests dashboard. 2. System retrieves and displays all pending requests with priority, equipment, and alert details. 3. Supervisor selects a request to view its full details. |
| **Alternative Flow** | 2a. No pending requests exist → system displays an empty state message. |
| **Includes** | — |

---

## UC6 — Approve or Reject Request

| Field | Description |
|---|---|
| **Use Case ID** | UC6 |
| **Use Case Name** | Approve or Reject Request |
| **Actor(s)** | Supervisor |
| **Description** | After reviewing a maintenance request, a supervisor decides to approve it — triggering work order creation and technician assignment — or reject it with a stated reason. |
| **Preconditions** | Supervisor is authenticated. A maintenance request is in "Pending" status. |
| **Postconditions** | If approved: request status set to "Approved", a work order is created and assigned (UC7), and the technician is notified (UC15). If rejected: request status set to "Rejected" and the relevant party is notified (UC15). |
| **Main Flow** | 1. Supervisor reviews the request details (UC5). 2. Supervisor selects Approve and chooses an available technician. 3. System creates a work order and assigns it to the technician (UC7). 4. System notifies the technician of the assignment (UC15). |
| **Alternative Flow** | 2a. Supervisor selects Reject → system prompts for a rejection reason → request status set to "Rejected" → notification sent (UC15). |
| **Includes** | UC7 (Assign Work Order to Technician), UC15 (Send Notifications) |

---

## UC7 — Assign Work Order to Technician

| Field | Description |
|---|---|
| **Use Case ID** | UC7 |
| **Use Case Name** | Assign Work Order to Technician |
| **Actor(s)** | Supervisor |
| **Description** | Upon approving a maintenance request, the Backend API creates a work order and the supervisor assigns it to an available technician. |
| **Preconditions** | Maintenance request has been approved (UC6). At least one technician is available in the system. |
| **Postconditions** | Work order is created with status "Assigned". The assigned technician is notified (UC15). |
| **Main Flow** | 1. System creates a new work order linked to the approved request. 2. Supervisor selects an available technician to assign. 3. Backend API sets the work order status to "Assigned" with the selected technician. 4. System notifies the technician via the Notification Service (UC15). |
| **Alternative Flow** | 2a. No available technicians listed → supervisor can still proceed with assignment and note scheduling constraints. |
| **Includes** | UC15 (Send Notifications) |

---

## UC8 — Track Work Order Progress

| Field | Description |
|---|---|
| **Use Case ID** | UC8 |
| **Use Case Name** | Track Work Order Progress |
| **Actor(s)** | Supervisor |
| **Description** | A supervisor monitors the real-time status and progress of all active work orders to ensure they are completed on time. |
| **Preconditions** | Supervisor is authenticated. At least one active work order exists in the system. |
| **Postconditions** | Supervisor is aware of the current status and progress of all active work orders. |
| **Main Flow** | 1. Supervisor navigates to the Work Orders tracking dashboard. 2. System retrieves and displays all active work orders with their current statuses and technician assignments. 3. Supervisor selects individual work orders to view detailed progress. |
| **Alternative Flow** | 2a. No active work orders exist → system displays an empty state message. |
| **Includes** | — |

---

## UC9 — Confirm and Close Work Order

| Field | Description |
|---|---|
| **Use Case ID** | UC9 |
| **Use Case Name** | Confirm and Close Work Order |
| **Actor(s)** | Supervisor |
| **Description** | After a technician submits a completion report, the supervisor reviews the work and either confirms closure — which triggers KPI recalculation — or reopens the work order for rework. |
| **Preconditions** | Supervisor is authenticated. Work order is in "Completed" status. |
| **Postconditions** | If satisfactory: work order status set to "Closed", KPI metrics updated, administrator can view updated dashboard. If unsatisfactory: work order status set to "Rework Required", technician notified (UC15). |
| **Main Flow** | 1. Supervisor receives a completion notification. 2. Supervisor reviews the completed work order and maintenance history. 3. Supervisor confirms the work is satisfactory and closes the work order. 4. Backend API sets work order status to "Closed" and recalculates KPI metrics. |
| **Alternative Flow** | 3a. Work unsatisfactory → supervisor adds rework notes → Backend API sets status to "Rework Required" → technician notified (UC15). |
| **Includes** | UC15 (Send Notifications) |

---

## UC10 — Monitor KPIs and Dashboards

| Field | Description |
|---|---|
| **Use Case ID** | UC10 |
| **Use Case Name** | Monitor KPIs and Dashboards |
| **Actor(s)** | Administrator |
| **Description** | An administrator monitors system-wide key performance indicators such as equipment downtime, average response time, and repair costs through live dashboards. |
| **Preconditions** | Administrator is authenticated. Closed work orders and KPI data exist in the database. |
| **Postconditions** | Administrator views current KPI metrics and can identify performance trends. |
| **Main Flow** | 1. Administrator navigates to the KPI Dashboard. 2. System retrieves and displays aggregated KPI metrics. 3. Administrator reviews metrics across equipment, departments, and time periods. |
| **Alternative Flow** | 2a. No KPI data available yet → system displays a zero-state dashboard with guidance. |
| **Includes** | — |

---

## UC11 — View Maintenance Reports

| Field | Description |
|---|---|
| **Use Case ID** | UC11 |
| **Use Case Name** | View Maintenance Reports |
| **Actor(s)** | Administrator |
| **Description** | An administrator views detailed maintenance reports including work order histories, equipment maintenance records, spare parts usage, and cost summaries. |
| **Preconditions** | Administrator is authenticated. Maintenance history data exists in the database. |
| **Postconditions** | Administrator has access to the requested filtered report data. |
| **Main Flow** | 1. Administrator navigates to the Reports section. 2. Administrator selects a report type and applies filters (date range, equipment, technician). 3. System retrieves and displays the filtered report. |
| **Alternative Flow** | 3a. No data matches the applied filters → system displays an empty result with a suggestion to adjust filters. |
| **Includes** | — |

---

## UC12 — Process Sensor Readings

| Field | Description |
|---|---|
| **Use Case ID** | UC12 |
| **Use Case Name** | Process Sensor Readings |
| **Actor(s)** | IoT Sensors (external system) |
| **Description** | IoT sensors continuously publish readings (temperature, vibration, pressure) to the IoT Gateway via MQTT. The Gateway normalizes the payload and forwards it to the Alert Engine for threshold evaluation. |
| **Preconditions** | IoT sensors are active and connected to the MQTT broker. Equipment records exist in the system. |
| **Postconditions** | A normalized sensor event is delivered to the Alert Engine for evaluation. |
| **Main Flow** | 1. IoT sensor detects a reading and publishes a MQTT payload. 2. IoT Gateway receives and normalizes the payload. 3. IoT Gateway forwards the normalized event to the Alert Engine. 4. Alert Engine evaluates the reading against configured thresholds (UC13). |
| **Alternative Flow** | 2a. Payload is malformed → IoT Gateway discards it and logs an error. |
| **Includes** | UC13 (Generate Predictive Alert) |

---

## UC13 — Generate Predictive Alert

| Field | Description |
|---|---|
| **Use Case ID** | UC13 |
| **Use Case Name** | Generate Predictive Alert |
| **Actor(s)** | Alert Engine (internal system) |
| **Description** | When a sensor reading exceeds a configured threshold, the Alert Engine generates a predictive alert record and triggers the automatic creation of a maintenance request. |
| **Preconditions** | A normalized sensor event has been received by the Alert Engine. Threshold configuration exists in the database for the given equipment and metric. |
| **Postconditions** | An alert record is stored in the database. Automatic creation of a maintenance request is triggered (UC14). |
| **Main Flow** | 1. Alert Engine retrieves the threshold configuration for the equipment and metric. 2. Sensor reading exceeds the threshold → Alert Engine generates a predictive alert. 3. Alert Engine stores the alert record and triggers maintenance request creation (UC14). |
| **Alternative Flow** | 1a. Reading is within the normal range → Alert Engine logs the reading as normal; no alert is generated. |
| **Includes** | UC14 (Auto-Create Maintenance Request) |

---

## UC14 — Auto-Create Maintenance Request

| Field | Description |
|---|---|
| **Use Case ID** | UC14 |
| **Use Case Name** | Auto-Create Maintenance Request |
| **Actor(s)** | Alert Engine (internal system) |
| **Description** | Upon generating a predictive alert, the Alert Engine calls the Backend API to automatically create a maintenance request of type "predictive" and notify the responsible supervisor. |
| **Preconditions** | A predictive alert has been generated (UC13). Equipment and supervisor records exist in the database. |
| **Postconditions** | Maintenance request created with status "Pending". Supervisor notified via the Notification Service (UC15). |
| **Main Flow** | 1. Alert Engine sends a request to the Backend API to create a maintenance request linked to the alert. 2. Backend API stores the request with type "predictive" and status "Pending". 3. Backend API retrieves the responsible supervisor's contact details. 4. Backend API triggers a notification to the supervisor (UC15). |
| **Alternative Flow** | 1a. Backend API is unreachable → Alert Engine retries the request; if the failure persists, the error is logged. |
| **Includes** | UC15 (Send Notifications) |

---

## UC15 — Send Notifications

| Field | Description |
|---|---|
| **Use Case ID** | UC15 |
| **Use Case Name** | Send Notifications |
| **Actor(s)** | Notification Service (external system) |
| **Description** | The Backend API triggers the external Notification Service to deliver email or SMS alerts to the relevant actors at key workflow events: new request created, work order assigned, work completed, request rejected, rework required, and rework completed. |
| **Preconditions** | A triggering workflow event has occurred. Recipient contact details exist in the database. |
| **Postconditions** | The notification is delivered to the target actor via email or SMS. A delivery confirmation is returned to the Backend API. |
| **Main Flow** | 1. Backend API sends a notification request to the Notification Service with recipient details, notification type, and payload. 2. Notification Service delivers the message via email or SMS. 3. Notification Service returns a delivery confirmation to the Backend API. |
| **Alternative Flow** | 2a. Delivery fails → Notification Service retries the delivery; if the message remains undeliverable, the Backend API logs the failure. |
| **Includes** | — |

---
