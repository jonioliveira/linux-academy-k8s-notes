update deployment
note: --record flag informs about the update so that it can be rolled back later
kubectl set image deployment/rolling-deployment nginx=nginx:1.7.9 --record

rollout

kubectl rollout history deployment/rolling-deployment

kubectl rollout history deployment/rolling-deployment --revision=2


Notes:
MaxSurge: max number of replicas
MaxUnvailabel: max number of unvailable replicas
