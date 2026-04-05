## linkding-secret example

This configuration connects linkding to a PostgreSQL database managed by CloudNativePG.

The database is exposed internally via the `postgres-rw` service,
which always points to the current primary instance.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: linkding-env
  namespace: linkding
type: Opaque
stringData:
  LD_DB_ENGINE: postgres
  LD_DB_DATABASE: <DB_NAME>
  LD_DB_USER: <DB_USER>
  LD_DB_PASSWORD: <DB_PASSWORD>
  LD_DB_HOST: postgres-rw.cloudnative-pg.svc.cluster.local
  LD_DB_PORT: "5432"
  LD_SUPERUSER_NAME: <APP_ADMIN_USER>
  LD_SUPERUSER_PASSWORD: <APP_ADMIN_PASSWORD>
  LD_SUPERUSER_EMAIL: <APP_ADMIN_EMAIL>
```