## Use Case Descriptions

### UC1 — Log Maintenance Request

| Field | Description |
|---|---|
| **Use Case ID** | UC1 |
| **Use Case Name** | Log Maintenance Request |
| **Actor(s)** | Technician |
| **Description** | A technician logs a maintenance request for equipment that needs preventive or corrective maintenance. |
| **Preconditions** | Technician is authenticated. Equipment record exists in the system. |
| **Postconditions** | Maintenance request is stored and supervisor is notified. |
| **Main Flow** | 1. Technician enters request details. 2. System validates the request data. 3. System stores the maintenance request. 4. System sends a new request notification to the supervisor. 5. Technician receives confirmation. |
| **Extensions** | Invalid or missing request details → system shows an error → technician corrects and resubmits. |
| **Includes** | Send Notifications |

### UC2 — Assign and Track Work Order

| Field | Description |
|---|---|
| **Use Case ID** | UC2 |
| **Use Case Name** | Assign and Track Work Order |
| **Actor(s)** | Supervisor |
| **Description** | A supervisor assigns a work order to a technician and tracks its status. |
| **Preconditions** | Supervisor is authenticated. A maintenance request exists. |
| **Postconditions** | Work order is created, technician is notified, and work order status can be tracked. |
| **Main Flow** | 1. Supervisor selects a maintenance request. 2. Supervisor assigns the work order to a technician. 3. System validates the assignment. 4. System creates the work order. 5. System sends a work order notification to the technician. 6. Supervisor tracks the work order status. |
| **Extensions** | Request is rejected → system updates request status and sends rejection notification to technician. |
| **Includes** | Send Notifications |

### UC3 — Update Work Order

| Field | Description |
|---|---|
| **Use Case ID** | UC3 |
| **Use Case Name** | Update Work Order |
| **Actor(s)** | Technician |
| **Description** | A technician updates an assigned work order to show progress or completion. The system performs all update operations within a database transaction to ensure data consistency. |
| **Preconditions** | Technician is authenticated. Work order is assigned to the technician. |
| **Postconditions** | Work order, maintenance history, and spare parts inventory are updated. Supervisor is notified. |
| **Main Flow** | 1. Technician enters work order update. 2. System validates the update details. 3. System updates the work order. 4. System updates maintenance history and spare parts inventory. 5. System sends a completion notification to the supervisor. 6. Technician receives confirmation. |
| **Extensions** | Invalid or missing update details → system shows an error → technician corrects and resubmits. |
| **Includes** | Send Notifications |

### UC4 — Handle Sensor Alert

| Field | Description |
|---|---|
| **Use Case ID** | UC4 |
| **Use Case Name** | Handle Sensor Alert |
| **Actor(s)** | IoT Sensors |
| **Description** | IoT sensors send readings to the system. If the reading is abnormal, the system creates a sensor alert and maintenance request. |
| **Preconditions** | IoT sensors are active. Equipment record exists in the system. |
| **Postconditions** | If abnormal, sensor alert and maintenance request are stored, and supervisor is notified. |
| **Main Flow** | 1. IoT sensors send sensor reading. 2. System validates the sensor data. 3. System performs threshold checking and predictive diagnostics on sensor data. 4. If reading is abnormal, system stores sensor alert. 5. System creates maintenance request. 6. System sends sensor alert notification to supervisor. |
| **Extensions** | Invalid sensor data → system ignores the reading or returns an error. Normal reading → system stores the sensor reading only and no alert is created. |
| **Includes** | Send Notifications |

### UC5 — Monitor KPI Reports

| Field | Description |
|---|---|
| **Use Case ID** | UC5 |
| **Use Case Name** | Monitor KPI Reports |
| **Actor(s)** | Administrator |
| **Description** | Administrator monitors KPI reports such as downtime, response time, and repair cost. |
| **Preconditions** | Administrator is authenticated. Maintenance data exists in the system. |
| **Postconditions** | KPI reports are displayed to the administrator. |
| **Main Flow** | 1. Administrator opens KPI dashboard. 2. System retrieves maintenance data. 3. System calculates KPIs such as downtime, response time (MTTR), and maintenance costs. 4. System displays KPI reports. |
| **Extensions** | No maintenance data available → system displays an empty KPI report message. |
| **Includes** | None |