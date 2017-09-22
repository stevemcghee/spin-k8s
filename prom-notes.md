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






