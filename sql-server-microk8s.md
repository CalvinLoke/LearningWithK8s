# SQL-Server Deployment in Microk8s
This document will contain the necessary steps required to deploy an SQL Server in Kubernetes using Microk8s. Hence, it is assumed that you have already installed microk8s.

# Enabling the necessary add-ons
`microk8s enable dns dashboard storage registry`

# Creating the deployment file

```
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: mssql-data
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mssql-deployment
spec:
  replicas: 1
  selector:
     matchLabels:
       app: mssql
  template:
    metadata:
      labels:
        app: mssql
    spec:
      terminationGracePeriodSeconds: 30
      securityContext:
        fsGroup: 10001
      containers:
      - name: mssql
        image: mcr.microsoft.com/mssql/server:2019-latest
        ports:
        - containerPort: 1433
        env:
        - name: MSSQL_PID
          value: "Developer"
        - name: ACCEPT_EULA
          value: "Y"
        - name: SA_PASSWORD
          value: "Password1234"
        volumeMounts:
        - name: mssqldb
          mountPath: /var/opt/mssql
      volumes:
      - name: mssqldb
        persistentVolumeClaim:
          claimName: mssql-data
---
apiVersion: v1
kind: Service
metadata:
  name: mssql-deployment
spec:
  selector:
    app: mssql
  ports:
    - protocol: TCP
      port: 1433
      targetPort: 1433
  type: LoadBalancer
```

Note that this deployment file should not be used in development due to the password being exposed. In development, do change the raw text value of the password to a secret. A detailed guide can be found [here](https://docs.microsoft.com/en-us/sql/linux/tutorial-sql-server-containers-kubernetes?view=sql-server-ver15) under the *Create an SA Password* section. 

Alternatively, you could pull this repository using 

`git clone https://github.com/CalvinLoke/LearningWithK8s`

# Checking if the

