
## linkedin-db-secret example:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: linkding-db-secret
  namespace: cloudnative-pg
  labels:
    cnpg.io/reload: "true"
type: kubernetes.io/basic-auth
stringData:
  username: <DB_USER>
  password: <DB_PASSWORD>
```

## postgres-superuser example:
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: postgres-superuser
  namespace: cloudnative-pg
type: kubernetes.io/basic-auth
stringData:
  username: postgres
  password: <SUPERUSER_PASSWORD>
```