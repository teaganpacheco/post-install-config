# osTicket Post-Installation Configuration Troubleshooting

Use this guide when the Lab 2 configuration does not behave as expected.

---

## 1. Cannot Access the Admin Panel

Confirm you are using an osTicket account with administrative privileges.

Staff URL:

```text
http://localhost/osTicket/scp/login.php
```

After signing in, look for the **Admin Panel** link.

If the account is an Agent without administrative access, the Admin Panel may not be available.

---

## 2. Agent Cannot See a Ticket

Check:

1. Which Department owns the ticket?
2. What is the Agent's primary Department?
3. Does the Agent have extended access to the ticket's Department?
4. Is the ticket assigned directly to another Agent or Team?
5. Is the Agent a member of an assigned Team?

Do not immediately grant broad access. Determine which access rule is responsible first.

---

## 3. Department Does Not Appear During Transfer

Check the Department's status.

A disabled or archived Department may not be available for normal routing.

Confirm:

```text
Admin Panel
> Agents
> Departments
```

and verify that the intended Department is active.

---

## 4. Help Topic Does Not Appear to Users

Check:

```text
Admin Panel
> Manage
> Help Topics
```

Verify:

- Help Topic is Active
- Help Topic is not configured as staff-only/private
- Parent topic settings are appropriate
- The end-user portal has been refreshed

---

## 5. Ticket Routes to the Wrong Department

Inspect the Help Topic.

Verify:

```text
Help Topic
> New Ticket Options
> Department
```

Also remember that other osTicket mechanisms, such as Ticket Filters, can affect routing in more advanced environments.

For this lab, keep the environment simple enough that the Help Topic behavior is easy to observe.

---

## 6. Wrong SLA Is Applied

Check all possible SLA sources used in your lab.

Start with:

```text
Help Topic
Department
System Default
```

For this project, the recommended Help Topic configuration explicitly assigns the expected SLA.

Verify that the intended Help Topic contains the correct SLA Plan.

---

## 7. Ticket Becomes Overdue Unexpectedly

Inspect:

- SLA grace period
- SLA schedule
- Department schedule
- System schedule
- Ticket Due Date

A manually assigned Due Date can also make a ticket overdue.

---

## 8. Agent Cannot Sign In

Verify:

- Agent account is active
- Username/email is correct
- Password is correct
- Agent was created under Admin Panel > Agents
- You are using the Staff Control Panel URL

```text
http://localhost/osTicket/scp/login.php
```

Do not confuse an **Agent** account with an **End User** account.

---

## 9. End User Cannot Create a Ticket

Open:

```text
http://localhost/osTicket
```

Check:

```text
Admin Panel
> Settings
> Users
```

Review registration and ticket-submission settings.

The exact wording may vary by version. Validate the actual client-portal behavior after every change.

---

## 10. John Can Still See a Ticket After Transfer

Do not assume this is an error.

Check whether John has:

- Extended Department access
- Team access
- Direct assignment
- Another permission that grants visibility

This is one of the key concepts that Lab 3 is designed to explore.

---

## Troubleshooting Method

Use this sequence:

```text
1. Identify the object involved
2. Determine its configured relationship
3. Identify the expected access/routing behavior
4. Reproduce the issue
5. Change one setting
6. Retest
7. Document what changed
```

For example:

```text
Ticket
  -> Help Topic
  -> Department
  -> SLA
  -> Agent access
```

Follow the chain rather than changing unrelated settings.
