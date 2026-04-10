# Integrations administrative panel

## Objective
Allow administrative profiles to track operational health of integrations and run quick tests without accessing raw technical logs.

## Permissions
- Web access: authenticated users `is_staff` or `is_superuser`.
- APIs:
  - `GET /api/admin/integracoes/health/`
  - `POST /api/admin/integracoes/testar/`
  - Both restricted to `is_staff`/`is_superuser`.

## What the screen displays
- Current status (`online`, `partial`, `offline`, `not_configured`, `authentication_error`, `timeout`).
- Configuration/operationality.
- Last check, last success and last failure.
- Summary type of the problem (`error_type`).
- Latency indicator (`low`, `medium`, `high`, `not_available`).
- Recent logs simplified by integration.

## Actions
- **Test all**: runs complete healthcheck.
- **Test again** (per line): runs test only for the chosen integration.

## UX Guidelines
- UI avoids stack traces and shows `friendly_message`.
- During execution, buttons are disabled to avoid competing calls.
- Explicit Empty state when there are no monitored integrations.