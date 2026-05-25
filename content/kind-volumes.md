---
publish: true
aliases:
  - Volume
  - PVC
  - PV
  - PersistanceVolumeClaim
  - PersistanceVolume
title: "Kind: Ingress"
created: 2026-01-29T21:35:20.000+01:00
modified: 2026-02-24T13:18:58.959+01:00
tags:
  - Tech/DevOps/Kubernetes/Kinds
---

Um ein beständiges Volume in Kubernetes einem Container anzuhängen, damit die Daten auch bei Beendigung/Absturz des Containers vorhanden sind, kann ein Volume erstellt werden. DigitalOcean übernimmt das ganze erstellen, mounten, …. Dafür soll am besten ein Statefull-Set erstellt werden und ein Volume angefügt werden. Falls das volume nicht existiert wird ein neues damit angelegt. Beachte dass der Volumenamen über den ganzen Cluster unique sein muss.

Beachte dass beim ersten Pod hochfahren ggf. ein Fehler kommen kann das dass Volume nicht existiert. Es kann 2-3 Restarts in Anspruch nehmen bis das Volume korrekt erstellt und eingebunden wurde. Es kann überprüft werden ob das Volume erstellt wurde indem: DigitalOcean-Dashboard öffnen → Volumes Block Storage oder DigitalOcean-Dashboard öffnen → Kubernetes → Cluster auswählen → Resources → Volumes.

### Löschen

Im Daten auf einem Volume zu löschen muss man am besten das ganze Volume löschen. Achtung nicht in DigitalOcean direkt löschen, sondern in Kubernetes zuerst das Stateful-Set und danach kann das `Persistent Volume Claims` gelöscht werden. Sobald dieses gelöscht wird, wird es auch in DigitalOcean gelöscht. Danach kann einfach das Stateful-Set neu angelegt werden.

ggf. muss dann der Backend-Pod neu gestartet werden, da dieser die Schemas anlegt.

### DB erstellen

Öffne das Terminal der DB, logge dich bei der Datenbank ein und erstelle die Datenbank.

1. `mariadb -h localhost -u root -p`
2. Password eingeben
3. `SHOW DATABASES;`
4. `CREATE <your-db-name>;`

# Example

```yaml
apiVersion: apps/v1
Kind: StatefulSet
metadata:
  name: mariadb
  namespace: kuratli-fiduciary-crm
spec:
  serviceName: mariadb
  replicas: 1
  template:
    spec:
      containers:
      - name: mariadb
        image: mariadb
        volumeMounts:
        - mountPath: "/data"
          name: csi-pvc-kuratli-fiduciary-crm-mariadb
  volumeClaimTemplates:
  - metadata:
      name: csi-pvc-kuratli-fiduciary-crm-mariadb
    spec:
      accessModes:
      - ReadWriteOnce
      resources:
        requests:
          storage: 1Gi
      storageClassName: do-block-storage
```

[How to Add Volumes to Kubernetes Clusters | DigitalOcean Documentation](https://docs.digitalocean.com/products/kubernetes/how-to/add-volumes/)
