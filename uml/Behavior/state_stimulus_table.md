# State-Stimulus Table — Work Order Lifecycle

| Current State | Stimulus / Event | Action / Response | Next State |
|---|---|---|---|
| — | Maintenance request is submitted or predictive request is created | System stores the request with status pending and prepares it for supervisor review | Pending Request |
| Pending Request | Supervisor approves maintenance request | System creates a work order and prepares it for assignment | Created |
| Pending Request | Supervisor rejects maintenance request | System updates the request status and sends rejection notification | Rejected |
| Created | Supervisor assigns technician | System records the technician assignment and sends work order notification | Assigned |
| Assigned | Technician views assigned work order and starts work | System displays work order details and marks the work order as active | In Progress |
| In Progress | Technician submits work order completion | System records maintenance history, labour hours, parts used, updates equipment status, deducts spare parts, and notifies supervisor | Completed |
| Completed | Supervisor reviews and approves completed work | System closes the work order and updates KPI reports | Closed |
| Completed | Supervisor is not satisfied and requests rework | System records rework notes and sends rework notification to technician | Rework Requested |
| Rework Requested | Technician performs rework | System reopens the work order for active maintenance | In Progress |
| Closed | — | Terminal state — no further transitions | — |
| Rejected | — | Terminal state — no further transitions | — |