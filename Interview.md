### Create yml file from command 
kubectl run redis --image=redis --dry-run=client -o yaml > pod.yml

###  update running pod yml file
kubectl edit pod ```<pod-name>```

###  Create an NGINX Pod
kubectl run --generator=run-pod/v1 nginx --image=nginx

###  Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)
kubectl run --generator=run-pod/v1 nginx --image=nginx --dry-run -o yaml

###  Create a deployment
kubectl create deployment --image=nginx nginx

###  Generate Deployment YAML file (-o yaml). Don't create it(--dry-run)
kubectl create deployment httpd-frontend --image=httpd:2.4-alpine  --dry-run=client -o yaml> n.yaml

###  Generate Deployment YAML file (-o yaml). Don't create it(--dry-run) with 4 Replicas (--replicas=4)
kubectl create deployment --image=nginx nginx --dry-run -o yaml > nginx-deployment.yaml
Save it to a file, make necessary changes to the file (for example, adding more replicas) and then create the deployment.

### Expose Service 
Create a new service to access the web application using the service-definition-1.yaml file
Name: webapp-service; Type: NodePort; targetPort: 8080; port: 8080; nodePort: 30080; selector: simple-webapp

kubectl expose deployment simple-webapp-deployment --name=simple-webapp-service --target-port=8080 --type=NodePort --port=8080 --dry-run=client -o yaml > a.yml

Add line NodePort in a.yml
```
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  name: simple-webapp-service
spec:
  ports:  - port: 8080
    protocol: TCP
    targetPort: 8080
->  nodePort 30080
  selector:
    name: simple-webapp
  type: NodePort
status:
  loadBalancer: {}
```
