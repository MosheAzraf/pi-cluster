## pgadmin-secret example:

```yaml
apiVersion: v1
kind: Secret
metadata:
    name: pgadmin-env
    namespace: pgadmin
type: Opaque
stringData:
    PGADMIN_DEFAULT_EMAIL: <email>
    PGADMIN_DEFAULT_PASSWORD: <password>
```