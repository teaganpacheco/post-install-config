# osTicket: Post-Installation Configuration

This project continues the **CourseCareers IT osTicket lab series** by configuring a newly installed osTicket instance for realistic help desk operations.

In the previous project, we deployed the infrastructure and installed osTicket. In this lab, we turn that blank installation into a functioning IT support environment by configuring **roles, departments, teams, agents, users, SLA plans, and help topics**.

> **CourseCareers IT Lab 2:** Configure osTicket for Help Desk Operations

---

## Project Objectives

By completing this project, you will:

- Distinguish between the osTicket **Admin Panel** and **Agent Panel**
- Configure role-based permissions for help desk staff
- Build departments that control ticket ownership and visibility
- Create a cross-functional team
- Create help desk agents and assign organizational access
- Create end users who will submit support requests
- Configure Service Level Agreement (SLA) plans
- Configure Help Topics for ticket categorization and routing
- Validate that the help desk is ready for ticket-lifecycle exercises
- Understand how ticketing configuration supports real IT service operations

---

## Prerequisite Project

Complete **Lab 1: Deploy and Install osTicket** before beginning this project.

Repository:

[osTicket: Prerequisites and Installation](https://github.com/teaganpacheco/osticket-prereqs)

At minimum, you should already have:

- A running Windows Server 2022 Azure VM
- IIS installed and working
- PHP configured
- MySQL running
- osTicket installed successfully
- Access to the osTicket Staff Control Panel
- Access to the osTicket end-user portal

---

## Technologies and Concepts

- osTicket
- Help Desk Administration
- Ticketing Systems
- IT Service Management (ITSM)
- Role-Based Access Control (RBAC)
- Departments
- Teams
- Agents
- End Users
- Service Level Agreements (SLAs)
- Ticket Priorities
- Help Topics
- Ticket Routing
- Least Privilege
- Access Control
- Escalation Workflows

---

# How osTicket Organizes the Help Desk

Before configuring the system, understand the purpose of each object.

```text
Help Desk
|
+-- Roles
|   └── What an Agent is allowed to do
|
+-- Departments
|   └── Where tickets are owned and which Agents can access them
|
+-- Teams
|   └── Cross-functional groups of Agents
|
+-- Agents
|   └── IT staff who work tickets
|
+-- Users
|   └── Customers who submit tickets
|
+-- SLA Plans
|   └── Expected resolution time / overdue thresholds
|
└-- Help Topics
    └── User-facing categories that can drive routing, priority, and SLA
```

A useful way to remember the model:

> **Role = permissions**  
> **Department = organizational ownership/access**  
> **Team = cross-functional collaboration**  
> **SLA = time expectation**  
> **Help Topic = intake and routing logic**

---

# Lab Environment

This project uses the osTicket environment from Lab 1.

## Staff Control Panel

```text
http://localhost/osTicket/scp/login.php
```

## End-User Portal

```text
http://localhost/osTicket
```

Sign in to the Staff Control Panel using the administrator account created during Lab 1.

---

# Part 1 — Understand the Admin Panel and Agent Panel

After signing in, observe that osTicket provides two different administrative experiences.

## Admin Panel

The **Admin Panel** is used to configure the help desk itself.

Examples include:

- Roles
- Departments
- Teams
- Agents
- SLA Plans
- Help Topics
- System settings

## Agent Panel

The **Agent Panel** is the operational interface used by help desk staff.

Examples include:

- Viewing queues
- Working tickets
- Creating tickets
- Managing users
- Assigning or transferring tickets
- Posting replies and internal notes
- Resolving and closing tickets

### Verify Your Work

Switch between **Admin Panel** and **Agent Panel** and identify where each major configuration area lives.

---

# Part 2 — Configure Roles

Navigate to:

```text
Admin Panel
└── Agents
    └── Roles
```

Roles define what actions an Agent is authorized to perform.

## Create a Role

Create:

```text
Name: Supreme Admin
```

For this training environment, grant the role broad ticket-management permissions so it can be used by the lab agents.

> **Real-world note:** Production environments should follow least privilege. Do not give every technician unrestricted administrative permissions simply because it is convenient.

### Why Roles Matter

Roles are an example of **Role-Based Access Control (RBAC)**.

Instead of assigning individual permissions separately to every employee, permissions are grouped into roles and those roles are assigned to staff.

Common real-world examples might include:

```text
Help Desk Technician
Senior Help Desk Technician
Desktop Support
Network Administrator
Help Desk Manager
System Administrator
```

---

# Part 3 — Configure Departments

Navigate to:

```text
Admin Panel
└── Agents
    └── Departments
```

Departments are one of the most important objects in osTicket.

They are used for:

- Ticket ownership
- Ticket routing
- Agent visibility
- Department-specific SLA behavior
- Organizational separation

## Required Departments

Ensure the following departments exist:

### Support

```text
Department: Support
Type: Public
```

Use this as the general help desk / desktop support department.

### SysAdmins

```text
Department: SysAdmins
Type: Private
```

This represents a systems administration group.

### Online Banking

```text
Department: Online Banking
Type: Private
```

This represents a specialized application or business-service support group.

> At least one department must remain public. The **Support** department provides that public/default help desk function in this lab.

---

# Part 4 — Understand Department Access

Department membership affects which tickets an Agent can see and work.

This becomes important in Lab 3.

Example:

```text
John
└── Primary Department: Support

Jane
└── Primary Department: SysAdmins
```

If a ticket is transferred from Support to SysAdmins, John's access may change depending on his department access configuration.

This allows ticketing systems to separate work between groups.

### Real-World Example

A Tier 1 Help Desk technician might be able to view:

```text
General Support
Password Reset
Hardware Support
```

but not:

```text
Human Resources
Payroll
Executive Support
Cybersecurity Investigations
```

Department access helps enforce those boundaries.

---

# Part 5 — Configure a Team

Navigate to:

```text
Admin Panel
└── Agents
    └── Teams
```

Create:

```text
Team Name: Major Incident Team
```

Teams are different from departments.

A **Department** represents normal organizational ticket ownership.

A **Team** can combine Agents from different departments for a particular issue or workflow.

## Example

```text
Major Incident Team
├── Help Desk Agent
├── System Administrator
├── Network Administrator
└── Application Support Engineer
```

A major outage may require all of these specialties even though they normally belong to separate departments.

> Do not create **Online Banking** as a Team in this lab. It is a Department because Lab 3 will transfer ownership of a banking outage to that department.

---

# Part 6 — Configure Agents

Navigate to:

```text
Admin Panel
└── Agents
    └── Agents
```

Agents are the IT professionals who work support tickets.

Create two lab Agents.

---

## Agent 1 — Jane

Example configuration:

```text
Name: Jane
Primary Department: SysAdmins
Role: Supreme Admin
```

Create a unique lab email/username and password.

Jane represents a systems administrator.

---

## Agent 2 — John

Example configuration:

```text
Name: John
Primary Department: Support
Role: Supreme Admin
```

Create a unique lab email/username and password.

John represents a Help Desk / Tier 1 support technician.

---

## Team Membership

Add **Jane** and **John** to:

```text
Major Incident Team
```

This demonstrates that Agents from different departments can participate in the same Team.

### Security Note

Do not reuse your:

- Azure password
- Windows Server password
- MySQL password
- osTicket administrator password

Create separate credentials for the lab Agent accounts.

---

# Part 7 — Configure End Users

Switch to:

```text
Agent Panel
└── Users
```

Create two end users:

```text
Karen
Ken
```

Use lab email addresses that you can distinguish from Agent accounts.

These accounts represent customers or employees who submit support requests.

---

# Part 8 — Configure User Ticket Access

Navigate to:

```text
Admin Panel
└── Settings
    └── Users
```

For this lab series, configure the help desk so students can create tickets through the client portal without introducing unnecessary account-registration complexity.

The goal is to ensure you can complete Lab 3 by submitting tickets as end users.

> Depending on the osTicket version and configuration, the wording of registration settings may differ slightly. Validate the behavior from the end-user portal rather than relying only on the checkbox label.

### Verify Your Work

Open:

```text
http://localhost/osTicket
```

Confirm that an end user can reach the ticket submission workflow.

---

# Part 9 — Configure SLA Plans

Navigate to:

```text
Admin Panel
└── Manage
    └── SLA Plans
```

An SLA Plan defines the amount of time a ticket can remain unresolved before it becomes overdue.

Create the following plans.

---

## Sev-A

```text
Name: Sev-A
Grace Period: 1 hour
Schedule: 24/7
Status: Active
```

Use for business-critical incidents.

Examples:

- Company-wide outage
- Revenue-generating service unavailable
- Critical business application unavailable

---

## Sev-B

```text
Name: Sev-B
Grace Period: 4 hours
Schedule: 24/7
Status: Active
```

Use for significant problems that require timely attention but are not complete business outages.

Examples:

- Executive workstation failure
- Important application issue
- Department-impacting incident

---

## Sev-C

```text
Name: Sev-C
Grace Period: 8 hours
Schedule: Business Hours
Status: Active
```

Use for normal requests and lower-impact issues.

Examples:

- Equipment requests
- Routine software requests
- General support questions

---

# SLA vs. Priority

These concepts are related, but they are not identical.

## Priority

Priority represents how important or urgent the ticket is relative to other work.

Examples:

```text
Low
Normal
High
Emergency
```

## SLA

The SLA defines the expected time window before the ticket becomes overdue.

Example:

```text
Emergency Priority
+
Sev-A SLA
=
Critical ticket expected to receive rapid attention
```

A ticket can have a priority and an SLA at the same time.

---

# Part 10 — Configure Help Topics

Navigate to:

```text
Admin Panel
└── Manage
    └── Help Topics
```

Help Topics provide user-friendly categories during ticket creation.

They can also drive ticket routing and other properties behind the scenes.

Create the following topics.

---

## Business Critical Outage

Recommended configuration:

```text
Help Topic: Business Critical Outage
Department: Online Banking
Priority: Emergency
SLA Plan: Sev-A
Status: Active
```

This will support the banking outage scenario in Lab 3.

---

## Personal Computer Issues

Recommended configuration:

```text
Help Topic: Personal Computer Issues
Department: Support
Priority: Normal
SLA Plan: Sev-B
Status: Active
```

---

## Equipment Request

Recommended configuration:

```text
Help Topic: Equipment Request
Department: Support
Priority: Normal
SLA Plan: Sev-C
Status: Active
```

---

## Password Reset

Recommended configuration:

```text
Help Topic: Password Reset
Department: Support
Priority: High
SLA Plan: Sev-B
Status: Active
```

---

## Other

Recommended configuration:

```text
Help Topic: Other
Department: Support
Priority: Normal
SLA Plan: Sev-C
Status: Active
```

---

# Why Help Topics Matter

The customer should not need to understand the internal IT organization.

A user can simply select:

```text
Password Reset
```

Instead of deciding whether the ticket belongs to:

```text
Help Desk
Identity and Access Management
Active Directory Team
Security Operations
```

The ticketing system can use the Help Topic to route the request correctly.

This creates a better customer experience and more consistent ticket categorization.

---

# Part 11 — Validate the Configuration

Before moving to Lab 3, review the system.

## Roles

- [ ] Supreme Admin exists

## Departments

- [ ] Support exists
- [ ] SysAdmins exists
- [ ] Online Banking exists

## Teams

- [ ] Major Incident Team exists
- [ ] Jane is a member
- [ ] John is a member

## Agents

- [ ] Jane exists
- [ ] Jane's primary department is SysAdmins
- [ ] John exists
- [ ] John's primary department is Support

## Users

- [ ] Karen exists
- [ ] Ken exists

## SLA Plans

- [ ] Sev-A — 1 hour / 24x7
- [ ] Sev-B — 4 hours / 24x7
- [ ] Sev-C — 8 hours / Business Hours

## Help Topics

- [ ] Business Critical Outage
- [ ] Personal Computer Issues
- [ ] Equipment Request
- [ ] Password Reset
- [ ] Other

---

# Part 12 — Functional Validation

Do not validate configuration only by looking at the Admin Panel.

Test the help desk as a user.

## Test Ticket

From:

```text
http://localhost/osTicket
```

Create a temporary test ticket using:

```text
Help Topic: Personal Computer Issues
Subject: Lab validation ticket
```

Then sign in to the Agent Panel as John.

Verify:

- The ticket appears in the appropriate queue
- The ticket is associated with Support
- The expected SLA is applied
- The expected priority is applied
- John can open the ticket

After validating the configuration, close the test ticket.

---

# Expected Help Desk Design

At the end of the project, your environment should approximately resemble:

```text
CourseCareers Help Desk
|
+-- Departments
|   |
|   +-- Support
|   |   └── John
|   |
|   +-- SysAdmins
|   |   └── Jane
|   |
|   └-- Online Banking
|
+-- Team
|   |
|   └-- Major Incident Team
|       ├── John
|       └── Jane
|
+-- Users
|   ├── Karen
|   └── Ken
|
+-- SLA Plans
|   ├── Sev-A (1 hour)
|   ├── Sev-B (4 hours)
|   └── Sev-C (8 hours)
|
└-- Help Topics
    ├── Business Critical Outage
    ├── Personal Computer Issues
    ├── Equipment Request
    ├── Password Reset
    └── Other
```

---

# Completion Criteria

You are ready for Lab 3 when:

- [ ] The osTicket installation from Lab 1 is operational
- [ ] Roles are configured
- [ ] Departments are configured
- [ ] Major Incident Team is configured
- [ ] Jane and John can sign in as Agents
- [ ] Karen and Ken exist as end users
- [ ] SLA Plans are active
- [ ] Help Topics are active
- [ ] A user can submit a ticket
- [ ] Help Topic routing behaves as expected
- [ ] John can view a Support ticket
- [ ] You understand the difference between a Department and a Team

---

# Troubleshooting

A dedicated troubleshooting guide is available here:

[docs/troubleshooting.md](docs/troubleshooting.md)

A compact configuration reference is available here:

[docs/configuration-reference.md](docs/configuration-reference.md)

---

# Suggested Portfolio Evidence

Capture screenshots showing:

1. osTicket Admin Panel
2. Roles configuration
3. Departments list
4. Major Incident Team
5. Agent list
6. Jane's department configuration
7. John's department configuration
8. SLA Plans
9. Help Topics
10. End-user ticket submission form
11. Successful validation ticket in the Agent Panel

Store sanitized screenshots in:

```text
images/
```

> Do not expose passwords, authentication tokens, personal email addresses, or other sensitive information in screenshots.

---

# Skills Demonstrated

This project demonstrates practical experience with:

- Help desk administration
- IT ticketing systems
- IT Service Management concepts
- Role-Based Access Control (RBAC)
- Access control
- User and Agent administration
- Departmental ticket routing
- Cross-functional teams
- Service Level Agreements
- Ticket prioritization
- Ticket categorization
- Help Topics
- Escalation concepts
- Least privilege
- Operational validation
- Technical documentation

---

# Interview Talking Points

After completing the project, you should be able to explain:

### Why would a company use Departments?

Departments separate ticket ownership and control which groups of technicians can access specific categories of support work.

### How is a Team different from a Department?

Departments represent normal organizational ownership and access boundaries. Teams allow Agents from different departments to collaborate on specialized issues.

### What is an SLA?

An SLA establishes the expected service window for a ticket and can determine when the ticket becomes overdue.

### Why use Help Topics?

Help Topics provide understandable categories for users while allowing the help desk to automatically apply internal routing, priority, SLA, and assignment rules.

### Why does ticket categorization matter?

Consistent categorization improves routing, reporting, staffing decisions, trend analysis, SLA measurement, and identification of recurring problems.

---

# Real-World Considerations

A production help desk would normally require additional planning around:

- Identity provider / SSO integration
- MFA
- Email integration
- Role separation
- Least privilege
- Ticket retention
- Privacy
- Sensitive-data handling
- Escalation policies
- SLA reporting
- Knowledge management
- Asset management
- Monitoring
- Change management
- Backup and disaster recovery
- Audit logging

The purpose of this lab is to learn the underlying operating model before introducing those additional enterprise controls.

---

# Next Lab

**Lab 3: Work Tickets Through the Ticket Lifecycle** will use this configuration to practice:

- Ticket intake
- Triage
- Priority and SLA evaluation
- Assignment
- Department transfers
- Access control
- Escalation
- Troubleshooting documentation
- User communication
- Resolution
- Closure

---

## Author

Created as part of the **CourseCareers Information Technology** hands-on lab series.

This repository is intended for educational and portfolio use.
