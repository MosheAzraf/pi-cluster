## homepage-secret example

This secret was originally used to provide credentials for widgets
(e.g. AdGuard, OMV, Grafana) in order to display extended data.

In the current setup, this is optional and not required.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: homepage-secrets
  namespace: homepage
type: Opaque
stringData:
  # AdGuard Home
  HOMEPAGE_VAR_ADGUARD_USERNAME: <USERNAME>
  HOMEPAGE_VAR_ADGUARD_PASSWORD: <PASSWORD>

  # OpenMediaVault
  HOMEPAGE_VAR_OMV_USERNAME: <USERNAME>
  HOMEPAGE_VAR_OMV_PASSWORD: <PASSWORD>

  # Grafana
  HOMEPAGE_VAR_GRAFANA_USERNAME: <USERNAME>
  HOMEPAGE_VAR_GRAFANA_PASSWORD: <PASSWORD>
```