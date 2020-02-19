Our company has a Kubernetes cluster that is running several pods and services. A service called oauth-provider in the gem namespace has stopped working. Our task is to investigate the service and determine what is causing the problem, save some relevant data for future analysis, and then fix the problem.

- The broken service is oauth-provider. It is located in the gem namespace.
- Identify which Kubernetes object is broken and causing the service to fail. Save the name of the object in the file /usr/ckad/broken-object-name.txt.
- Save the object's summary data in JSON format to the file /usr/ckad/broken-object.json.
- Edit the object to fix the problem.
- The oauth-provider service is a NodePort service listening on port 30080, so we can test it using curl localhost:30080.

Note that there may be other objects in the cluster which appear to be broken. Our task is to identify what specifically is causing the oauth-provider service to fail. Ignore any object which doesn't affect the oauth-provider service.

Become the root user so that we can write to the file:
- `sudo -i`

Describe the broken service:
- `kubectl describe service oauth-provider -n gem`
Note that the service's selector selects pods with the label role: oauth.

Get a list of pods with labels in order to locate the pod(s) selected by the service:
- `kubectl get pods --all-name spaces --show-labels`
  
Note that the pod called bowline has the role: oauth label.
Save the name of the broken pod:
- `vi /usr/ckad/broken-object-name.txt`
Put the word **bowline** in there.

Save the JSON summary data for the broken pod to the specified file:
- `kubectl get pod bowline -n gem -o json > /usr/ckad/broken-object.json`

Examine the broken pod more closely:
- `kubectl describe pod bowline -n gem`

Based on the event log and pod status, it appears something may be wrong with the pod image. Look at the pod's container image, which appears to be misspelled. Edit the pod:
- `kubectl edit pod bowline -n gem`

Fix the image name by changing it to nginx:1.15.9.
Verify that the pod is now working:
`kubectl get pod bowline -n gem`

Test the broken service to make sure it is working:
`curl localhost:30080`