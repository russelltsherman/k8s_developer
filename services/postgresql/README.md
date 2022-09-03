# postgresql

PostgreSQL: The World's Most Advanced Open Source Relational Database

## References

[PostgreSQL Documentation](https://www.postgresql.org/)

## Usage

1. Retrieve the postgres user password

```sh
kubectl get secret postgresql -n postgresql -o jsonpath="{.data.postgres-password}" | base64 -d; echo
```

To connect to your database run the following command:

    POSTGRES_PASSWORD=$(kubectl get secret postgresql -n postgresql -o jsonpath="{.data.postgres-password}" | base64 -d; echo)
    kubectl run postgresql-client --rm --tty -i --restart='Never' --namespace postgresql --image docker.io/bitnami/postgresql:14.4.0-debian-11-r0 --env="PGPASSWORD=$POSTGRES_PASSWORD" \
      --command -- psql --host postgresql -U postgres -d postgres -p 5432

    > NOTE: If you access the container using bash, make sure that you execute "/opt/bitnami/scripts/postgresql/entrypoint.sh /bin/bash" in order to avoid the error "psql: local user with ID 1001} does not exist"

To connect to your database from outside the cluster execute the following commands:

    kubectl port-forward --namespace postgresql svc/postgresql 5432:5432 &
    PGPASSWORD="$POSTGRES_PASSWORD" psql --host 127.0.0.1 -U postgres -d postgres -p 5432
