kubectl apply -f candy-service-config.yml
kubectl apply -f db-password-secret.yml
kubectl apply -f candy-service-pod.yml
kubectl get pod candy-service