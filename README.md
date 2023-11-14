# In this demo you will run a simple PHP application:

## what you need to check before preparing your deployment

**Important**: 

Please make sure you have enough resources in your Vcluseter before you start your deployment.

**Best practice :** 
You may need to limit your application ressources by adding what we called ResourceQuota kubernetes kind in your deployment Yaml file.

In this example, I've added a ResourceQuota object that sets resource limits for CPU and memory. Adjust the values based on your application's requirements. You can customize the CPU, memory and ather values according to your application's needs and the available resources in your Kubernetes cluster.

If you need to learn more about the ResourceQuota , please refer to this documentation : https://kubernetes.io/docs/concepts/policy/resource-quotas/

```bash
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: php-app-ingress
spec:
  rules:
  - host: docs-vcluster2-443.m1dns.com  # Set the desired domain or hostname here
    http:
      paths:
      - path: /
        pathType: Prefix # type the path that will be used
        backend:
          service:
            name: php-app-clusterip-service
            port:
              number: 20210
---
apiVersion: v1
kind: ResourceQuota
metadata:
  name: ingress-resource-quota
spec:
  hard:
    cpu: "500m"  # 0.5 CPU cores
    memory: "512Mi"  # 512 Megabytes of memory

```


Before all clone this project on your local machine and move under OC-start file:
```
git clone https://github.com/jkhazri/OC-start.git
cd OC-start
```
1. create the deployment of the PHP app
```
kubectl apply -f deployment-PHP-demo.yaml
```
2. create the service ClusterIP 
```
kubectl apply -f service-PHP-demo.yaml
```
3. create the ingress that will be used to expose your PHP appli to the external world.In our case we used the domain docs-vcluster2-443.m1dns.com , so make sure that the Domain is available and change the PHP-ingress-file.yaml with your domain name.
For that you need to vim or nano the PHP-ingress-file.yaml and change variables (you will see an indication in the yaml file it self)
   
Example :

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: php-app-ingress
spec:
  rules:
  - host: docs-vcluster2-443.m1dns.com  # Set the desired domain or hostname here
    http:
      paths:
      - path: /PHPdemo # change the path that will be used to reach the application .
        pathType: Prefix 
        backend:
          service:
            name: php-app-clusterip-service 
            port:
              number: 20210  # Set the desired port number here (depends on the Vcluster port range)
```
Now the ingress is ready to deploy:
```
kubectl apply -f PHP-ingress-file.yaml
```

 to test the application open your browser and type http://yourDNS/
