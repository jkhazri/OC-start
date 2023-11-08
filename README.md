# In this demo you will run a simple PHP application:

# 1-create the deployment of the PHP app

```
kubectl apply -f deployment-PHP-demo.yaml
```

# 2-create the service ClusterIP 

```
kubectl apply -f service-PHP-demo.yaml
```

# 3-create the ingress that will be used to expose your PHP appli to the external world.

```
kubectl apply -f PHP-ingress-file.yaml
```
# In our case we used the domain docs-vcluster2-443.m1dns.com , so make sure that the Domain is available 

