# User Flow — Complete Work Item

```text
Open Work Item
  |
Complete
  |
Validate permission
  |
Check completion rules
  |
If incomplete subtasks:
    require explicit confirmation + reason
  |
Persist completion
  |
Audit
  |
Emit WorkItemCompleted
  |
Cancel pending reminder instances
  |
Async notification / analytics
```

A completed Work Item may be reopened only within a configurable reopen window.
