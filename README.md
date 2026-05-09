# Software-engineering-project

## 1. Group Info

**Group Number:** Group 01  

**Case Study:**  
Maintenance Management System  

**Student IDs + Names:**

20210748 — Mira Nebal Hendawi  
20210611 — Osama Eltayyeb Alameen  
20210853 — Zina Maher Alhijazeen  
20220637 — Zakaria Zakarya Alkashef  

**Course + Instructor:**  
Software Engineering — Dr. Samer Elkababji  

---

## 2. Overview

### System Purpose

The Maintenance Management System (MMS) is designed to manage and track maintenance operations in industrial, commercial, or institutional environments.

The system supports:

- Corrective maintenance requests logged by technicians when equipment faults or breakdowns occur
- Preventive maintenance requests logged by technicians for scheduled or routine maintenance
- Predictive maintenance alerts triggered by abnormal IoT sensor readings

The system helps reduce downtime, improve maintenance tracking, manage spare parts, and support KPI monitoring such as downtime, response time, and repair cost.

### Tools Used

- PlantUML
- Markdown
- GitHub
- Visual Studio Code 
- Pandoc

---

## 3. Diagrams

- **Context Diagram (C4 Level 1):** Shows the system boundary and how technicians, supervisors, administrators, IoT sensors, and the notification service interact with MMS.
- **Container Diagram (C4 Level 2):** Shows the internal architecture of MMS, including the Web Application, Backend API, Database, IoT Sensors, and Notification Service.
- **Activity Diagrams:** Show the maintenance workflows separated into corrective, preventive, and predictive maintenance.
- **Use Case Diagram:** Shows the main system functionalities and how each actor interacts with them.
- **Use Case Descriptions:** Provide tabular descriptions for each use case, including actors, preconditions, postconditions, main flows, extensions, and included use cases.
- **Sequence Diagrams:** Show the interaction flow for each use case.
  - **High-Level Sequence Diagrams:** Show stakeholder-level communication between actors, MMS, and external systems.
  - **Detailed Sequence Diagrams:** Show developer-level processing between the Web Application, Backend API, Database, and Notification Service.
- **Class Diagram:** Represents the static structure of the system, including classes, attributes, operations, inheritance, associations, aggregation, and composition.
- **State Diagram:** Models the lifecycle of a maintenance request and work order from pending request to closure, including rework when needed.
- **State-Stimulus Table:** Describes the events, actions, and next states for the work order lifecycle.

---

## 4. Repo Structure

```text
/docs
  se_report_group_01.md
  se_report_group_01.pdf

/uml
  Context/
    context_diagram.puml
    container_diagram.puml
    activity_diagrams/

  Interactions/
    usecase_diagram.puml
    usecase_description.md
    sequence_diagrams/

  Structure/
    class_diagram.puml

  Behavior/
    state_diagram.puml
    state_stimulus_table.md

README.md
```

---

## 5. Contributions

### Member Roles

- Osama — C4 Diagrams and Activity Diagrams  
- Mira — Use Case Diagram and Use Case Descriptions  
- Zina — Sequence Diagrams  
- Zakaria — Class Diagram and State Diagram  

### Commit Count

| Member | Commits |
|---|---:|
| Osama | 15 |
| Mira | 39 |
| Zina | 14 |
| Zakaria | 11 |
