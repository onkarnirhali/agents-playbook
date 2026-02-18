# Security and Privacy Standards

## Baseline

1. Follow least privilege for tokens, credentials, and logs.
2. Never expose secrets in client-side code or logs.
3. Store sensitive auth material encrypted at rest where applicable.

## Privacy Controls

1. Retention model is hybrid:
- raw email text retained for short window
- embeddings and task outcome signals retained longer
2. Users must have data export and delete controls by Beta.
3. Privacy behavior must match policy text and in product settings.

## Auditability

1. Log authentication, provider link changes, AI operations, and admin actions.
2. Restrict log access by role.
3. Preserve integrity of audit history.
