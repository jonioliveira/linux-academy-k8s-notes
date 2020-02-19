kubectl set image deployment/candy-deployment candy-ws=linuxacademycontent/candy-service:3 --record

# check status 
kubectl rollout status deployment/candy-deployment

Get a list of previous revisions.
kubectl rollout history deployment/candy-deployment

Undo the last revision.
kubectl rollout undo deployment/candy-deployment

Check the status of the rollout.
kubectl rollout status deployment/candy-deployment