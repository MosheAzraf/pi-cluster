## grafana-admin-secret example

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: grafana-admin-secret
  namespace: monitoring
type: Opaque
stringData:
  admin-user: <ADMIN_USER>
  admin-password: <ADMIN_PASSWORD>
```