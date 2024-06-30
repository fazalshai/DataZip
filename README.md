Commands that we require 

C:\Windows\System32>cd c:\minikube
----------------------------------------------------
c:\minikube>dir
 Volume in drive C is Windows-SSD
 Volume Serial Number is 2E0D-ED14
-----------------------------------------------------------------
 Directory of c:\minikube

30-Jun-24  03:26 PM    <DIR>          .
30-Jun-24  03:26 PM             1,252 clickhouse.yaml
30-Jun-24  11:55 AM                 0 kubectl
29-Jun-24  11:57 AM        98,241,024 minikube.exe
30-Jun-24  03:27 PM             1,539 superset.yaml
               4 File(s)     98,243,815 bytes
               1 Dir(s)  10,479,996,928 bytes free
--------------------------------------------------------------------

c:\minikube>kubectl apply -f superset.yaml
deployment.apps/superset created
service/superset-web unchanged

--------------------------------------------------------------------

c:\minikube>kubectl apply -f clickhouse.yaml
statefulset.apps/clickhouse created

--------------------------------------------------------------------

c:\minikube>kubectl get pods
NAME                            READY   STATUS    RESTARTS        AGE
clickhouse-0                    1/1     Running   1 (54s ago)     2m2s
superset-6c58c564b6-qz2tz       1/1     Running   1 (57s ago)     2m11s
superset-web-67b578c466-p4dlv   1/1     Running   16 (131m ago)   3h30m
-------------------------------------------------------------------------

c:\minikube>kubectl get svc
NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
clickhouse     ClusterIP   10.103.56.180   <none>        9000/TCP         3h6m
kubernetes     ClusterIP   10.96.0.1       <none>        443/TCP          5h15m
superset-web   NodePort    10.105.25.171   <none>        8088:30000/TCP   3h30m
-----------------------------------------------------------------------------

c:\minikube>minikube status     #status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
------------------------------------------------------------------------

c:\minikube>kubectl exec -it superset-6c58c564b6-qz2tz -- /bin/bash

superset@superset-6c58c564b6-qz2tz:/app$ superset fab create-admin
logging was configured successfully
2024-06-30 10:25:58,983:INFO:superset.utils.logging_configurator:logging was configured successfully
2024-06-30 10:25:59,002:INFO:root:Configured event logger of type <class 'superset.utils.log.DBEventLogger'>
/usr/local/lib/python3.10/site-packages/flask_limiter/extension.py:293: UserWarning: Using the in-memory storage for tracking rate limits as no storage was explicitly specified. This is not recommended for production use. See: https://flask-limiter.readthedocs.io#configuring-a-storage-backend for documentation about configuring the storage backend.
  warnings.warn(
Username [admin]: admin
User first name [admin]: admin
User last name [user]: admin
Email [admin@fab.org]:
Password:
Repeat for confirmation:
Recognized Database Authentications.
Admin User admin created.
superset@superset-6c58c564b6-qz2tz:/app$ superset db upgrade
logging was configured successfully
2024-06-30 10:26:43,566:INFO:superset.utils.logging_configurator:logging was configured successfully
2024-06-30 10:26:43,632:INFO:root:Configured event logger of type <class 'superset.utils.log.DBEventLogger'>
/usr/local/lib/python3.10/site-packages/flask_limiter/extension.py:293: UserWarning: Using the in-memory storage for tracking rate limits as no storage was explicitly specified. This is not recommended for production use. See: https://flask-limiter.readthedocs.io#configuring-a-storage-backend for documentation about configuring the storage backend.
-------------------------------------------------------------------------------------------------------------------------------------
c:\minikube>minikube service superset-web --url #to open in browser
http://127.0.0.1:27848
! Because you are using a Docker driver on windows, the terminal needs to be open to run it.

