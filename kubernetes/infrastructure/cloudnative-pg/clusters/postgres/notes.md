## Superuser access note

`enableSuperuserAccess: true` together with `superuserSecret` should allow login with the `postgres` user.

In practice, even when the Secret is configured correctly, password authentication may still fail.

---

### What it looks like

```bash
PGPASSWORD='strongpassword' psql -h postgres-rw -U postgres -d postgres
```

```text
FATAL: password authentication failed for user "postgres"
```

---

### Why this happens

The Secret exists and is referenced, but the password is not always applied to the `postgres` role inside PostgreSQL.

That means:
- `enableSuperuserAccess` is enabled  
- the Secret exists  
- but the actual role password was not updated  

---

### How to fix it

1. Find the primary pod:

```bash
kubectl exec -it -n cloudnative-pg postgres-1 -- psql -U postgres -d postgres -c "select pg_is_in_recovery();"
kubectl exec -it -n cloudnative-pg postgres-2 -- psql -U postgres -d postgres -c "select pg_is_in_recovery();"
```

- `t` → replica  
- `f` → primary  

---

2. Connect to the primary pod:

```bash
kubectl exec -it -n cloudnative-pg <PRIMARY_POD> -- psql -U postgres -d postgres
```

---

3. Update the password:

```sql
ALTER USER postgres WITH PASSWORD 'strongpassword';
```

---

4. Verify:

```bash
kubectl exec -it -n cloudnative-pg postgres-1 -- bash -c "PGPASSWORD='strongpassword' psql -h postgres-rw -U postgres -d postgres"
```

If the connection succeeds, the issue is resolved.

---

## Connecting to a specific database

To connect to a specific database, change only the database name and user.

### Example (linkding)

```bash
PGPASSWORD='<PASSWORD>' psql -h postgres-rw -U linkding -d linkding
```

### In pgAdmin

- Host: postgres-rw.cloudnative-pg.svc.cluster.local
- Port: 5432
- Database: linkding
- Username: linkding
- Password: from `linkding-db-secret`

### List available databases

```sql
\l
```

---

## Note

- Running `ALTER USER` on a replica will fail with:
  cannot execute ALTER ROLE in a read-only transaction

- You must execute it on the primary node.

- Superuser network access is disabled by default in CloudNativePG and should be enabled only when really needed.

This setup is suitable for learning and troubleshooting, not as a production default.