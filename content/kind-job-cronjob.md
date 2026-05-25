---
publish: true
aliases:
  - Job
  - CronJob
title: "Kind: Job | Kind: CronJob"
created: 2026-01-29T21:35:20.000+01:00
modified: 2026-02-24T13:18:58.959+01:00
tags:
  - Tech/DevOps/Kubernetes/Kinds
---

# Job

```yaml
# Job to insert sql-dump from s3 into mariaDB

apiVersion: batch/v1
Kind: Job
metadata:
  name: mariadb-backup-insertion
  namespace: kuratli-fiduciary-crm
spec:
  template:
    spec:
      imagePullSecrets:
      - name: ghcr-pull-secret
      containers:
      - name: mariadb-backup-insertion
        image: ghcr.io/fermionhq/s3-sql-dump-to-mariadb:8132948338-1
        env:
        - name: S3_FILE_NAME
          value: "snapshot-20240303T182116.sql.gz"
      restartPolicy: OnFailure
```

# CronJob

```yaml
# CronJob to backup mariaDB with an sql-dump uploaded to s3

apiVersion: batch/v1
Kind: CronJob
metadata:
  name: mariadb-backup
  namespace: kuratli-fiduciary-crm
spec:
  schedule: "0 0 * * *"
  successfulJobsHistoryLimit: 0
  failedJobsHistoryLimit: 0
  jobTemplate:
    spec:
      template:
        spec:
          imagePullSecrets:
          - name: ghcr-pull-secret
          containers:
          - name: mariadb-backup
            image: ghcr.io/fermionhq/mariadb-backup-dump-to-s3:7877541009-1
            env:
            - name: DB_HOST
              value: "mariadb"
          restartPolicy: OnFailure
```

## Remove cronJob job after run

[How to automatically remove completed Kubernetes Jobs created by a CronJob?](https://stackoverflow.com/questions/41385403/how-to-automatically-remove-completed-kubernetes-jobs-created-by-a-cronjob)
