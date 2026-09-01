# Lab 2 Configuration Reference

Use this as a compact reference after you have completed the detailed walkthrough in the main README.

---

## Role

| Object | Value |
|---|---|
| Role | Supreme Admin |

---

## Departments

| Department | Purpose | Suggested Type |
|---|---|---|
| Support | General Help Desk / Tier 1 | Public |
| SysAdmins | Systems Administration | Private |
| Online Banking | Specialized Business Application Support | Private |

---

## Team

| Team | Members |
|---|---|
| Major Incident Team | John, Jane |

---

## Agents

| Agent | Primary Department | Role |
|---|---|---|
| Jane | SysAdmins | Supreme Admin |
| John | Support | Supreme Admin |

---

## End Users

| User |
|---|
| Karen |
| Ken |

---

## SLA Plans

| SLA | Grace Period | Schedule | Use Case |
|---|---:|---|---|
| Sev-A | 1 hour | 24/7 | Critical outage |
| Sev-B | 4 hours | 24/7 | Significant incident |
| Sev-C | 8 hours | Business Hours | Routine request |

---

## Help Topics

| Help Topic | Department | Priority | SLA |
|---|---|---|---|
| Business Critical Outage | Online Banking | Emergency | Sev-A |
| Personal Computer Issues | Support | Normal | Sev-B |
| Equipment Request | Support | Normal | Sev-C |
| Password Reset | Support | High | Sev-B |
| Other | Support | Normal | Sev-C |

---

## URLs

### Staff Control Panel

```text
http://localhost/osTicket/scp/login.php
```

### End-User Portal

```text
http://localhost/osTicket
```

---

## Lab 3 Dependency

Do not substantially change the objects above before completing Lab 3.

The next lab uses these settings to demonstrate:

- Department-based ticket access
- Ticket transfers
- SLA changes
- Priority
- Agent ownership
- Escalation
- Ticket resolution
