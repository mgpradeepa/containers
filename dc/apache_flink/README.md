To use the flink job manager and task manager ver the iceberg, this setup is used

As this setup is used with iceberg based deployment, minio, nessie, is also installed along

We need to create a nessie keyspace in cassandra so that the catalog data is stored in cassandra making this setup a ducklake implementation.
```
CREATE KEYSPACE nessie WITH replication = {'class': SimpleStrategy 'replication_factor' : 1};
```