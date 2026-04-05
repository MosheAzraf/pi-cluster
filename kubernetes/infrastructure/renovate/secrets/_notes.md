## renovate-secret example:

```yaml
apiVersion: v1
kind: Secret
metadata:
    name: renovate-secret
    namespace: renovate
type: Opaque
stringData:
    RENOVATE_TOKEN: <token>
```