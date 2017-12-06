Notes:


 steven.mcghee@stevebookpro   master  helm install stable/prometheus/
NAME:   handy-elk
LAST DEPLOYED: Fri Sep 22 09:24:12 2017
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1beta1/Deployment
NAME                                     DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
handy-elk-prometheus-alertmanager        1        1        1           0          2s
handy-elk-prometheus-kube-state-metrics  1        1        1           0          2s
handy-elk-prometheus-pushgateway         1        1        1           0          2s
handy-elk-prometheus-server              1        1        1           0          2s

==> v1/ConfigMap
NAME                               DATA  AGE
handy-elk-prometheus-alertmanager  1     3s
handy-elk-prometheus-server        3     3s

==> v1/PersistentVolumeClaim
NAME                               STATUS   VOLUME    CAPACITY  ACCESSMODES  STORAGECLASS  AGE
handy-elk-prometheus-alertmanager  Pending  standard  3s
handy-elk-prometheus-server        Pending  standard  3s

==> v1/Service
NAME                                     CLUSTER-IP     EXTERNAL-IP  PORT(S)   AGE
handy-elk-prometheus-alertmanager        10.51.241.226  <none>       80/TCP    3s
handy-elk-prometheus-kube-state-metrics  None           <none>       80/TCP    2s
handy-elk-prometheus-node-exporter       None           <none>       9100/TCP  2s
handy-elk-prometheus-pushgateway         10.51.251.162  <none>       9091/TCP  2s
handy-elk-prometheus-server              10.51.240.15   <none>       80/TCP    2s

==> v1beta1/DaemonSet
NAME                                DESIRED  CURRENT  READY  UP-TO-DATE  AVAILABLE  NODE-SELECTOR  AGE
handy-elk-prometheus-node-exporter  5        5        4      5           4          <none>         2s


NOTES:
The Prometheus server can be accessed via port 80 on the following DNS name from within your cluster:
handy-elk-prometheus-server.default.svc.cluster.local


Get the Prometheus server URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9090


The Prometheus alertmanager can be accessed via port 80 on the following DNS name from within your cluster:
handy-elk-prometheus-alertmanager.default.svc.cluster.local


Get the Alertmanager URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=alertmanager" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9093


The Prometheus PushGateway can be accessed via port 9091 on the following DNS name from within your cluster:
handy-elk-prometheus-pushgateway.default.svc.cluster.local


Get the PushGateway URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=pushgateway" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9093

For more information on running Prometheus, visit:
https://prometheus.io/



 ⚙ steven.mcghee@stevebookpro   master  helm install stable/grafana 

NAME:   orbiting-gerbil
LAST DEPLOYED: Fri Sep 22 09:27:01 2017
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/PersistentVolumeClaim
NAME                     STATUS   VOLUME    CAPACITY  ACCESSMODES  STORAGECLASS  AGE
orbiting-gerbil-grafana  Pending  standard  1s

==> v1/Service
NAME                     CLUSTER-IP     EXTERNAL-IP  PORT(S)  AGE
orbiting-gerbil-grafana  10.51.247.117  <none>       80/TCP   1s

==> v1beta1/Deployment
NAME                     DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
orbiting-gerbil-grafana  1        1        1           0          1s

==> v1/Secret
NAME                     TYPE    DATA  AGE
orbiting-gerbil-grafana  Opaque  2     1s

==> v1/ConfigMap
NAME                            DATA  AGE
orbiting-gerbil-grafana-config  1     1s
orbiting-gerbil-grafana-dashs   0     1s


NOTES:
1. Get your 'admin' user password by running:

   kubectl get secret --namespace default orbiting-gerbil-grafana -o jsonpath="{.data.grafana-admin-password}" | base64 --decode ; echo

2. The Grafana server can be accessed via port 80 on the following DNS name from within your cluster:

   orbiting-gerbil-grafana.default.svc.cluster.local

   Get the Grafana URL to visit by running these commands in the same shell:

     export POD_NAME=$(kubectl get pods --namespace default -l "app=orbiting-gerbil-grafana,component=grafana" -o jsonpath="{.items[0].metadata.name}")
     kubectl --namespace default port-forward $POD_NAME 3000

3. Login with the password from step 1 and the username: admin

~/src/charts ● 2 jobs                          


 steven.mcghee@stevebookpro   master  helm install cockroachdb 
NAME:   cranky-echidna
LAST DEPLOYED: Mon Oct  2 11:17:04 2017
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/Service
NAME                               CLUSTER-IP    EXTERNAL-IP  PORT(S)             AGE
cranky-echidna-cockroachdb         None          <none>       26257/TCP,8080/TCP  0s
cranky-echidna-cockroachdb-public  10.51.244.30  <none>       26257/TCP,8080/TCP  0s

==> v1beta1/StatefulSet
NAME                        DESIRED  CURRENT  AGE
cranky-echidna-cockroachdb  3        0        0s

==> v1beta1/PodDisruptionBudget
NAME                               MIN-AVAILABLE  MAX-UNAVAILABLE  ALLOWED-DISRUPTIONS  AGE
cranky-echidna-cockroachdb-budget  67%            N/A              0                    0s


NOTES:
CockroachDB can be accessed via port 26257 (or whatever you set the GrpcPort
value to) at the following DNS name from within your cluster:
cranky-echidna-public.default.svc.cluster.local

Because CockroachDB supports the PostgreSQL wire protocol, you can connect to
the cluster using any available PostgreSQL client.

For example, you can open up a SQL shell to the cluster by running:

    kubectl run -it --rm cockroach-client \
        --image=cockroachdb/cockroach \
        --restart=Never \
        --command -- ./cockroach sql --insecure --host cranky-echidna-cockroachdb-public.default



From there, you can interact with the SQL shell as you would any other SQL shell,
confident that any data you write will be safe and available even if parts of
your cluster fail.

Finally, to open up the CockroachDB admin UI, you can port-forward from your
local machine into one of the instances in the cluster:

    kubectl port-forward cranky-echidna-cockroachdb-0 8080

Then you can access the admin UI at http://localhost:8080/ in your web browser.

For more information on using CockroachDB, please see the project's docs at
https://www.cockroachlabs.com/docs/

~/src/charts/stable                                                                                               
 steven.mcghee@stevebookpro   master  helm install mongodb    
NAME:   boisterous-koala
LAST DEPLOYED: Mon Oct  2 11:18:09 2017
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/Secret
NAME                      TYPE    DATA  AGE
boisterous-koala-mongodb  Opaque  2     1s

==> v1/PersistentVolumeClaim
NAME                      STATUS   VOLUME    CAPACITY  ACCESSMODES  STORAGECLASS  AGE
boisterous-koala-mongodb  Pending  standard  1s

==> v1/Service
NAME                      CLUSTER-IP     EXTERNAL-IP  PORT(S)    AGE
boisterous-koala-mongodb  10.51.252.199  <none>       27017/TCP  1s

==> v1beta1/Deployment
NAME                      DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
boisterous-koala-mongodb  1        1        1           0          1s


NOTES:
MongoDB can be accessed via port 27017 on the following DNS name from within your cluster:
boisterous-koala-mongodb.default.svc.cluster.local

To connect to your database run the following command:

   kubectl run boisterous-koala-mongodb-client --rm --tty -i --image bitnami/mongodb --command -- mongo --host boisterous-koala-mongodb
~/src/charts/stable                                                                                               
 steven.mcghee@stevebookpro   master  helm install rabbitmq 
NAME:   nuanced-tortoise
LAST DEPLOYED: Mon Oct  2 11:18:37 2017
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/Secret
NAME                       TYPE    DATA  AGE
nuanced-tortoise-rabbitmq  Opaque  2     1s

==> v1/PersistentVolumeClaim
NAME                       STATUS   VOLUME    CAPACITY  ACCESSMODES  STORAGECLASS  AGE
nuanced-tortoise-rabbitmq  Pending  standard  1s

==> v1/Service
NAME                       CLUSTER-IP    EXTERNAL-IP  PORT(S)                                AGE
nuanced-tortoise-rabbitmq  10.51.243.34  <none>       4369/TCP,5672/TCP,25672/TCP,15672/TCP  1s

==> v1beta1/Deployment
NAME                       DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
nuanced-tortoise-rabbitmq  1        1        1           0          1s


NOTES:

** Please be patient while the chart is being deployed **

  Credentials:

    echo Username      : user
    echo Password      : $(kubectl get secret --namespace default nuanced-tortoise-rabbitmq -o jsonpath="{.data.rabbitmq-password}" | base64 --decode)
    echo ErLang Cookie : $(kubectl get secret --namespace default nuanced-tortoise-rabbitmq -o jsonpath="{.data.rabbitmq-erlang-cookie}" | base64 --decode)

  RabbitMQ can be accessed within the cluster on port 5672 at nuanced-tortoise-rabbitmq.default.svc.cluster.local

  To access for outside the cluster execute the following commands:

    export POD_NAME=$(kubectl get pods --namespace default -l "app=nuanced-tortoise-rabbitmq" -o jsonpath="{.items[0].metadata.name}")
    kubectl port-forward $POD_NAME 5672:5672 15672:15672

  To Access the RabbitMQ AMQP port:

    echo amqp://127.0.0.1:5672/

  To Access the RabbitMQ Management interface:

    echo URL : http://127.0.0.1:15672

~/src/charts/stable                                                                                               
 steven.mcghee@stevebookpro   master  helm install --name artifactory --set artifactory.image.repository=docker.bintray.io/jfrog/artifactory-oss stable/artifactory
NAME:   artifactory
LAST DEPLOYED: Mon Oct  2 11:20:17 2017
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/Secret
NAME                     TYPE    DATA  AGE
artifactory-artifactory  Opaque  1     1s

==> v1/PersistentVolumeClaim
NAME                                 STATUS   VOLUME    CAPACITY  ACCESSMODES  STORAGECLASS  AGE
artifactory-artifactory-artifactory  Pending  standard  1s
artifactory-artifactory-nginx        Pending  standard  1s
artifactory-artifactory-postgresql   Pending  standard  1s

==> v1/Service
NAME         CLUSTER-IP     EXTERNAL-IP  PORT(S)                     AGE
artifactory  10.51.254.204  <none>       8081/TCP                    1s
nginx        10.51.248.163  <pending>    80:30112/TCP,443:32440/TCP  1s
postgresql   10.51.251.172  <none>       5432/TCP                    1s

==> v1beta1/Deployment
NAME                                 DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
artifactory-artifactory-artifactory  1        1        1           0          1s
artifactory-artifactory-nginx        1        1        1           0          1s
artifactory-artifactory-postgresql   1        1        1           0          1s


NOTES:
Congratulations. You have just deployed JFrog Artifactory Pro!

1. Get the Artifactory URL by running these commands:

   NOTE: It may take a few minutes for the LoadBalancer IP to be available.
         You can watch the status of the service by running 'kubectl get svc -w nginx'
   export SERVICE_IP=$(kubectl get svc --namespace default nginx -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
   echo http://$SERVICE_IP/

2. Open Artifactory in your browser
   Default credential for Artifactory:
   user: admin
   password: password

~/src/charts/stable                 



NAME:   irreverant-penguin
LAST DEPLOYED: Mon Oct  2 11:56:39 2017
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1beta1/Deployment
NAME                      DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
irreverant-penguin-redis  1        1        1           0          1s

==> v1/Secret
NAME                      TYPE    DATA  AGE
irreverant-penguin-redis  Opaque  1     1s

==> v1/PersistentVolumeClaim
NAME                      STATUS   VOLUME    CAPACITY  ACCESSMODES  STORAGECLASS  AGE
irreverant-penguin-redis  Pending  standard  1s

==> v1/Service
NAME                      CLUSTER-IP    EXTERNAL-IP  PORT(S)   AGE
irreverant-penguin-redis  10.51.243.42  <none>       6379/TCP  1s


NOTES:
Redis can be accessed via port 6379 on the following DNS name from within your cluster:
irreverant-penguin-redis.default.svc.cluster.local
To get your password run:

    REDIS_PASSWORD=$(kubectl get secret --namespace default irreverant-penguin-redis -o jsonpath="{.data.redis-password}" | base64 --decode)

To connect to your Redis server:

1. Run a Redis pod that you can use as a client:

   kubectl run irreverant-penguin-redis-client --rm --tty -i \
    --env REDIS_PASSWORD=$REDIS_PASSWORD
   --image bitnami/redis:3.2.9-r2 -- bash

2. Connect using the Redis CLI:

  redis-cli -h irreverant-penguin-redis -a $REDIS_PASSWORD



