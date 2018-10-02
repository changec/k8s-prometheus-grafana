# prometheus+grafana+node_exporter

1. docker pull images  
    + <code>docker pull prom/node-exporter</code>  
    + <code>docker pull prom/prometheus:v2.0.0</code>  
    + <code>docker pull grafana/grafana:4.2.0</code>  

2. create node-exporter  
    + <code>kubectl create -f node-exporter.yaml</code>  

3. create prometheus  
    + <code>kubectl create -f prometheus/</code>  
    
4. create grafana  
    + <code>kubectl create -f grafana/</code>  

5. check k8s' svc
    + <code>kubectl get svc -n kube-system</code>
  ```bash
  ubuntu@iiiedu-ais-1:~/k8s-prometheus-grafana$ kubectl get svc -n kube-system
  NAME                   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
  grafana                NodePort    10.105.158.43    <none>        3000:32413/TCP   50m
  kube-dns               ClusterIP   10.96.0.10       <none>        53/UDP,53/TCP    92d
  kubernetes-dashboard   NodePort    10.109.159.131   <none>        443:30771/TCP    92d
  node-exporter          NodePort    10.105.214.200   <none>        9100:31672/TCP   5d
  prometheus             NodePort    10.101.1.108     <none>        9090:30003/TCP   5d  
  ```
6. node-exporter url  
    + http://\<k8s-ip\>:31672/metrics  
7. prometheus url
    + http://\<k8s-ip\>:30003/targets
8. grafana url
    + http://\<k8s-ip\>:32413
9. edit grafana data source
    + login admin/admin
    + config name:prometheus
    + config type:Prometheus
    + http setting:http://prometheus:9090
    + click save & test
    + import dashboard:315
