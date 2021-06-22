# Keycloak and PostgreSQL with JDBC_PING
Similarly to other templates, the keycloak-postgres-jdbc-ping.yml template creates a volume for PostgreSQL and boots up Keycloak connected to it. Traefik is used like load balancer to redirect all request to diferent container instances. The most important change is the JGroups Discovery protocol that is used in this configuration, which is JDBC_PING. JDBC_PING reuses the same database instance as all Keycloak servers in the cluster.

Run the example with the following command:

```shell
docker-compose -f keycloak-postgres.yml up --scale keycloak=2
```



Once the cluster is started, open http://localhost:8080/auth and login as user 'admin' with password 'Pa55w0rd'.

Note - Sometimes, it is necessary to adjust the JDBC_PING initialization SQL (see the manual). In such cases, make sure you specify proper initialize_sql string into JGROUPS_DISCOVERY_PROPERTIES property. For more information, please refer to JGroups codebase.