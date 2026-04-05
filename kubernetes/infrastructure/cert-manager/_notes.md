## Notes

The internal CA was bootstrapped using a temporary ClusterIssuer (internal-ca-bootstrap),
which is no longer present in the cluster.

The root certificate already exists and is used by the main ClusterIssuer (internal-ca).

example:

```yaml
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata:
  name: internal-ca-bootstrap
spec:
  selfSigned: {}
```

