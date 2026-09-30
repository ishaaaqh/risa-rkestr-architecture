# API Error Contract

The error contract should provide at minimum:

- Timestamp
- HTTP status
- Stable error code
- Human-readable message
- Request/correlation ID
- Optional field validation details

Example conceptual shape:

```text
{
  status,
  code,
  message,
  correlationId,
  details
}
```

Do not expose stack traces, SQL errors, secrets, internal infrastructure details, or sensitive authorization information.
