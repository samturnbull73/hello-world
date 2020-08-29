## Create yml file from command 
kubectl run redis --image=redis --dry-run=client -o yaml > pod.yml

## update running pod yml file
kubectl edit pod ```<pod-name>```
