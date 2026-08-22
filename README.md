# Business Process Management — Assignment

## Student Details

| Field              | Details                                      |
| ------------------ | -------------------------------------------- |
| Name               | Vinay Kartheek Bathala                       |
| Register Number    | RA2411026010953 & AD2                        |
| Programme          | B.Tech – Computer Science (AI & ML)          |
| Department         | Department of Computer Science & Engineering |
| Institution        | SRMIST Kattankulathur                        |
| Course             | Business Process Management                  |
| Faculty            | Kishore Anthuvan Sahayaraj K SIR             |
| Academic Year      | 2026 – 2027                                  |
| Date of Submission | 15 August 2026                               |

---

## Assignment Topic

BPMN Process Modelling — Three Scenarios

1. Employee Leave Approval
2. Online Purchase Order Processing
3. IT Service Request Handling

## Scenario 1 – Employee Leave Approval

**File:** `scenario1_employee_leave_approval.bpmn`

### Description

This process models the complete lifecycle of an employee leave request through the HR system.

### Process Flow

| Step | Description |
|------|-------------|
| **Start Event** | Employee submits a leave request |
| **Task 1** | HR system checks the employee's leave balance |
| **Gateway 1** | *Sufficient Leave Balance?* (Exclusive Gateway) |
| **Path A – YES** | Request forwarded to manager for approval |
| **Gateway 2** | *Manager Decision?* (Exclusive Gateway) |
| **Path A1 – Approved** | System updates leave balance → sends approval notification → **End** |
| **Path A2 – Rejected** | System sends rejection notification → **End** |
| **Path B – NO** | System sends insufficient-balance notification → **End** |

### BPMN Elements Used

- ✅ **Start Event** – Triggered when employee submits leave request
- ✅ **Tasks** – Check Leave Balance, Send to Manager, Update Balance, Notifications (4 tasks)
- ✅ **Exclusive Gateways (XOR)** – Two gateways: balance check and manager decision
- ✅ **End Events** – Three distinct end events: Approved, Rejected, Insufficient Balance

### Key Decision Points

```
Leave Balance Check
  ├── Sufficient  → Manager Approval
  │     ├── Approved → Update Balance → Notify Approval → END
  │     └── Rejected → Notify Rejection → END
  └── Insufficient → Notify Insufficient Balance → END
```

---

## Scenario 2 – Online Purchase Order Processing

**File:** `scenario2_online_purchase_order.bpmn`

### Description

This process models an end-to-end online purchase order, from order placement through shipment confirmation, with handling for stock unavailability and payment failures.

### Process Flow

| Step | Description |
|------|-------------|
| **Start Event** | Customer places an order |
| **Task 1** | System checks product availability |
| **Gateway 1** | *Product Available?* (Exclusive Gateway) |
| **Path A – Unavailable** | Notify customer out of stock → **End** |
| **Path B – Available** | Process payment |
| **Gateway 2** | *Payment Successful?* (Exclusive Gateway) |
| **Path B1 – Failed** | Notify customer payment failure → **End** |
| **Path B2 – Success** | Confirm order → Prepare shipment → Ship order → Send shipping confirmation → **End** |

### BPMN Elements Used

- ✅ **Start Event** – Customer places order
- ✅ **Tasks** – 8 tasks covering availability, payment, confirmation, preparation, shipping, notifications
- ✅ **Exclusive Gateways (XOR)** – Two gateways: availability check and payment result
- ✅ **End Events** – Three end events: Successfully Shipped, Out of Stock, Payment Failed
- ✅ **Multiple Process Paths** – Three distinct termination paths

### Key Decision Points

```
Check Availability
  ├── Unavailable → Notify Out of Stock → END
  └── Available  → Process Payment
        ├── Failed  → Notify Payment Failure → END
        └── Success → Confirm Order → Prepare → Ship → Notify → END
```

---

## Scenario 3 – IT Service Request Handling

**File:** `scenario3_it_service_request.bpmn`

### Description

This process models the full lifecycle of an IT support request from initial employee submission to final resolution notification, including severity-based routing and escalation to an external provider.

### Process Flow

| Step | Description |
|------|-------------|
| **Start Event** | Employee reports an IT problem |
| **Task 1** | Employee submits IT support request |
| **Task 2** | IT Help Desk registers the request |
| **Task 3** | Help Desk checks severity of the problem |
| **Gateway 1** | *Severity Level?* (Exclusive Gateway) |
| **Path A – Low** | Assign to Support Technician |
| **Path B – High** | Assign to Senior Technician |
| **Merge Gateway** | Both paths converge (Exclusive Merge) |
| **Task 6** | Technician investigates the problem |
| **Gateway 2** | *Can Be Resolved Internally?* (Exclusive Gateway) |
| **Path A – Yes** | Technician fixes the problem |
| **Path B – No** | Escalate to external service provider |
| **Merge Gateway** | Both resolution paths converge |
| **Task 9** | Help Desk updates request status |
| **Task 10** | Send resolution notification to employee |
| **End Event** | IT request resolved |

### BPMN Elements Used

- ✅ **Start Event** – Employee reports IT problem
- ✅ **Multiple Tasks** – 8 tasks spanning submission, registration, severity check, assignment, investigation, fix/escalation, status update, notification
- ✅ **Exclusive Gateways (XOR)** – Two split gateways (severity + resolution) and two merge gateways
- ✅ **Alternative Paths** – Low vs. High severity; Internal fix vs. External escalation
- ✅ **End Event** – Single end event: IT Request Resolved

### Key Decision Points

```
Check Severity
  ├── Low Severity  → Assign Support Technician ─┐
  └── High Severity → Assign Senior Technician  ─┴→ Investigate Problem
                                                         │
                                                 Can Resolve Internally?
                                                  ├── Yes → Fix Problem ──────────┐
                                                  └── No  → Escalate External ───┘
                                                                │
                                                        Update Request Status
                                                                │
                                                    Send Resolution Notification
                                                                │
                                                              END
```

---

## Repository Structure

```
bpmn-assignment/
├── README.md                               ← This file
├── scenario1_employee_leave_approval.bpmn  ← Scenario 1 BPMN model
├── scenario2_online_purchase_order.bpmn    ← Scenario 2 BPMN model
└── scenario3_it_service_request.bpmn       ← Scenario 3 BPMN model
```

---

## BPMN Element Legend

| Symbol | Element | Purpose |
|--------|---------|---------|
| ⬤ (thin ring) | Start Event | Marks the beginning of a process |
| ⬤ (thick ring) | End Event | Marks the end of a process |
| ▭ | Task | A unit of work performed in the process |
| ◇ (X marker) | Exclusive Gateway | Routes to exactly ONE path based on a condition |
| ◇ (no marker) | Merging Gateway | Merges two alternative incoming paths |
| → | Sequence Flow | Shows the order of process elements |

---
