---
hide:
  - toc
---

# Capítulo 3: Aplicação OCI PIZZA

# 3.3 Oracle NoSQL Cloud Simulator

https://docs.oracle.com/en/cloud/paas/nosql-cloud/donsq/#GUID-3E11C056-B144-4EEA-8224-37F4C3CB83F6

https://github.com/oracle/docker-images/tree/main/NoSQL

```bash linenums="1"
$ cd nosql
$ tar zxvf oracle-nosql-cloud-simulator-5.11.6.tar.gz
$ cd oracle-nosql-cloud-simulator-5.11.6/
$ sh runCloudSim -storePort 6000 -root ./ocipizza
Oracle NoSQL Cloud Simulator is ready
```

```bash linenums="1"
$ python3 -m venv venv

```