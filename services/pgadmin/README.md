# pgadmin

pgAdmin is the most popular and feature rich Open Source administration and development platform for PostgreSQL.

## References

[PGAdmin Documentation](https://www.pgadmin.org/)

## Usage

1. Retrieve the admin user password

```sh
kubectl get secret pgadmin4 -n pgadmin -o jsonpath="{.data.password}" | base64 -d; echo
```

## Issues

enabling oauth causes saved server config to behave unexpectedly
https://github.com/rowanruseler/helm-charts/issues/115
