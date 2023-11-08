# In this demo you will run a simple PHP application:

Before all clone this project on your local machine 
```
git clone https://github.com/jkhazri/OC-start.git
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
example :
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

 to test the application open your browser and type http://yourDNS/PHPdemo

