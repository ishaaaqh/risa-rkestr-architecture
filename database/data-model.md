# Database Model

This is the conceptual starting point. Physical schema is created incrementally with versioned migrations.

## Identity

- users
- authentication_identities
- authentication_sessions
- security_events

## Workspace

- workspaces
- workspace_memberships
- roles
- permissions
- role_permissions
- workspace_invitations

## Work

- work_items
- subtasks
- work_item_dependencies
- work_sessions
- attachments

## Classification

- categories
- contexts / context configuration as required
- work item classification attributes

## Reminder / Notification

- reminder_plans
- reminder_instances
- notification_preferences
- notification_templates
- notification_deliveries
- in_app_notifications

## Platform

- outbox_events
- audit_events

The exact physical schema is refined when each sprint is implemented.
