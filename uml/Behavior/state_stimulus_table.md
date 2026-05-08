# State-Stimulus Table — Work Order Lifecycle

| Current State | Stimulus / Event | Action / Response | Next State |
|---|---|---|---|
| — | Corrective/preventive request is logged or predictive request is created | System stores the maintenance request with pending status and sends a notification to the supervisor | Pending Request |
| Pending Request | Supervisor selects request and assigns technician | System validates the assignment and creates a work order from the maintenance request | Created |
| Created | Work order is created successfully | System records the technician assignment and sends work order notification to the technician | Assigned |
| Assigned | Technician views assigned work order and starts work | System displays work order details and marks the work order as active | In Progress |
| In Progress | Technician submits work order completion | System records maintenance history, labour hours, parts used, updates spare parts inventory, updates work order status, and notifies supervisor | Completed |
| Completed | Supervisor reviews completed work and closes work order | System updates work order status to closed and updates KPI reports | Closed |
| Completed | Supervisor requests rework | System updates work order status to rework requested and sends rework notification to the technician | Rework Requested |
| Rework Requested | Technician performs rework | System reopens the work order for active maintenance | In Progress |
| Closed | — | Terminal state — no further transitions | — |