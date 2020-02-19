kubectl logs counter
Multicontainer: 
kubectl logs <pod name> -c <container name>
save to a file
kubectl logs counter > counter.log