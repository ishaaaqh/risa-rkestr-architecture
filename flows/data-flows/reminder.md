# Data Flow — Reminder

```text
Work Item
 + Classification
 + Deadline
 + Planning
 + Workspace policy
       |
Reminder Policy Engine
       |
Reminder Plan
       |
Reminder Instances
       |
Scheduler / Worker
       |
Notification Request
       |
Notification System
       |
In-App / Push / Email
```

Reminder policy hierarchy:

1. Mandatory Workspace Policy
2. Explicit Work Item Reminder
3. Work Item-specific Policy
4. Workspace Default
5. System Default
