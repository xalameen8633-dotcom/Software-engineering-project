## Use Case Descriptions

### UC1 — Log Corrective Maintenance Request

| Field | Description |
|---|---|
| **Use Case ID** | UC1 |
| **Use Case Name** | Log Corrective Maintenance Request |
| **Actor(s)** | Technician |
| **Description** | A technician logs a corrective maintenance request when equipment has a fault, breakdown, or issue that requires repair. |
| **Preconditions** | Technician is authenticated. Equipment record exists in the system. |
| **Postconditions** | Corrective maintenance request is stored and supervisor is notified. |
| **Main Flow** | 1. Technician identifies equipment fault or breakdown. 2. Technician enters corrective request details. 3. System validates the request data. 4. System stores the corrective maintenance request. 5. System sends a new request notification to the supervisor. 6. Technician receives confirmation. |
| **Extensions** | Invalid or missing request details → system shows an error → technician corrects and resubmits. |
| **Includes** | Send Notifications |

---

### UC2 — Log Preventive Maintenance Request

| Field | Description |
|---|---|
| **Use Case ID** | UC2 |
| **Use Case Name** | Log Preventive Maintenance Request |
| **Actor(s)** | Technician |
| **Description** | A technician logs a preventive maintenance request for scheduled or routine maintenance before equipment failure occurs. |
| **Preconditions** | Technician is authenticated. Equipment record exists in the system. Scheduled maintenance need is identified. |
| **Postconditions** | Preventive maintenance request is stored and supervisor is notified. |
| **Main Flow** | 1. Technician identifies scheduled maintenance need. 2. Technician enters preventive request details. 3. System validates the request data. 4. System stores the preventive maintenance request. 5. System sends a new request notification to the supervisor. 6. Technician receives confirmation. |
| **Extensions** | Invalid or missing request details → system shows an error → technician corrects and resubmits. |
| **Includes** | Send Notifications |

---

### UC3 — Assign and Track Work Order

| Field | Description |
|---|---|
| **Use Case ID** | UC3 |
| **Use Case Name** | Assign and Track Work Order |
| **Actor(s)** | Supervisor |
| **Description** | A supervisor assigns a maintenance request as a work order to a technician and tracks the work order status after a valid assignment. |
| **Preconditions** | Supervisor is authenticated. A maintenance request exists. |
| **Postconditions** | If the assignment is valid, a work order is created, the technician is notified, and the supervisor can track the work order status. |
| **Main Flow** | 1. Supervisor receives a maintenance request notification. 2. Supervisor selects the maintenance request and technician. 3. System validates the assignment. 4. System creates the work order. 5. System sends a work order notification to the technician. 6. System confirms the assignment to the supervisor. 7. Supervisor views and tracks the work order status. |
| **Extensions** | Invalid assignment or technician unavailable → system shows an error message → work order is not created until the assignment is corrected. |
| **Includes** | Send Notifications |

---

### UC4 — Update Work Order

| Field | Description |
|---|---|
| **Use Case ID** | UC4 |
| **Use Case Name** | Update Work Order |
| **Actor(s)** | Technician |
| **Description** | A technician updates an assigned work order to show progress, completion, labour hours, and parts used. The system updates related records to keep data consistent. |
| **Preconditions** | Technician is authenticated. Work order is assigned to the technician. |
| **Postconditions** | Work order, maintenance history, spare parts inventory, and work order status are updated. Supervisor is notified. |
| **Main Flow** | 1. Technician views assigned work order. 2. Technician performs maintenance work. 3. Technician records labour and parts used. 4. Technician submits the work order update. 5. System validates the update details. 6. System updates the work order. 7. System updates maintenance history and spare parts inventory. 8. System sends a completion notification to the supervisor. 9. Technician receives confirmation. |
| **Extensions** | Invalid or missing update details → system shows an error → technician corrects and resubmits. Supervisor requests rework → technician performs rework and updates the work order again. |
| **Includes** | Send Notifications |

---

### UC5 — Handle Predictive Maintenance Alert

| Field | Description |
|---|---|
| **Use Case ID** | UC5 |
| **Use Case Name** | Handle Predictive Maintenance Alert |
| **Actor(s)** | IoT Sensors |
| **Description** | IoT sensors send abnormal equipment readings to the system. The system processes the readings, stores the sensor alert, and creates a predictive maintenance request. |
| **Preconditions** | IoT sensors are active. Equipment record exists in the system. |
| **Postconditions** | If the reading is abnormal, sensor alert and predictive maintenance request are stored, and supervisor is notified. |
| **Main Flow** | 1. IoT sensors detect abnormal temperature, vibration, or pressure reading. 2. IoT sensors send the abnormal sensor reading to the system. 3. System validates the sensor data. 4. System performs threshold checking and predictive diagnostics. 5. System stores the sensor alert. 6. System creates a predictive maintenance request. 7. System sends a predictive maintenance request notification to the supervisor. |
| **Extensions** | Invalid sensor data → system ignores the reading or returns an error. Normal reading → system stores the sensor reading only and no alert is created. |
| **Includes** | Send Notifications |

---

### UC6 — Monitor KPI Reports

| Field | Description |
|---|---|
| **Use Case ID** | UC6 |
| **Use Case Name** | Monitor KPI Reports |
| **Actor(s)** | Administrator |
| **Description** | Administrator monitors KPI reports such as downtime, response time, and repair cost. |
| **Preconditions** | Administrator is authenticated. |
| **Postconditions** | KPI reports are displayed to the administrator. |
| **Main Flow** | 1. Administrator opens KPI dashboard. 2. System retrieves maintenance data. 3. System calculates KPIs such as downtime, response time, and maintenance costs. 4. System displays KPI reports. |
| **Extensions** | No maintenance data available → system displays an empty KPI report message. |
| **Includes** | None |