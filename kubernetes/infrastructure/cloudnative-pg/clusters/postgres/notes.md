## Superuser access note

`enableSuperuserAccess: true` together with `superuserSecret` should allow login with the `postgres` user.

In my case, even though the Secret was configured correctly, password login still failed.

### What it looked like
Trying to connect with:

```bash
PGPASSWORD='strongpassword' psql -h postgres-rw -U postgres -d postgres
```

returned:

```text
FATAL: password authentication failed for user "postgres"
```

### Why this happens
The Secret may exist and be referenced correctly, but the password is not always applied in practice to the postgres user inside PostgreSQL.

That means:
- `enableSuperuserAccess` is enabled
- the Secret exists
- but the password was not actually synced to the `postgres` role

### How to fix it
Connect locally to PostgreSQL from the main pod and update the password manually:

```bash
kubectl exec -it -n cloudnative-pg postgres-1 -- bash
psql -U postgres -d postgres
```

Inside `psql`:

```sql
ALTER USER postgres WITH PASSWORD 'strongpassword';
```

Then test again:

```bash
PGPASSWORD='strongpassword' psql -h postgres-rw -U postgres -d postgres
```

If the connection succeeds, the issue is resolved.

## Note:

Superuser network access is disabled by default in CloudNativePG and should be enabled only when really needed for administrative or troubleshooting purposes.

This setup is intended for learning, testing, or temporary operational access. It is not recommended as the default approach for production environments.

