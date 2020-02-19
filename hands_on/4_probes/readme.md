Learning Objectives

Find the broken pod and save the pod name to the file `/home/cloud_user/debug/broken-pod-name.txt`

Since you don't know what namespace the broken pod is in, a quick way to find the broken pod is to list all pods from all namespaces:

kubectl get pods --all-namespaces

Check the STATUS field to find which pod is broken. Once you have located the broken pod, vi /home/cloud_user/debug/broken-pod-name.txt, enter the name of the broken pod, and save the file.

In the same namespace as the broken pod, find out which pod is using the most CPU and output the name of that pod to the file `/home/cloud_user/debug/high-cpu-pod-name.txt`

Look at the namespace of the broken pod, and then use kubectl top pod to show resource usage for all pods in that namespace.

kubectl top pod -n <namespace>
Identify which pod in that namespace is using the most CPU, then vi /home/cloud_user/debug/high-cpu-pod-name.txt, enter the name of the pod with the highest CPU usage, and then save the file.


Get the broken pod's summary data in the JSON format and output it to the file `/home/cloud_user/debug/broken-pod-summary.json`

You can get the JSON data and output it to the file like this:

kubectl get pod <pod name> -n <namespace> -o json > /home/cloud_user/debug/broken-pod-summary.json

Get the broken pod's container logs and output them to the file `/home/cloud_user/debug/broken-pod-logs.log`

You can get the logs and output them to the file like this:

kubectl logs <pod name> -n <namespace> > /home/cloud_user/debug/broken-pod-logs.log

Fix the problem with the broken pod so that it enters the `Running` state

Describe the broken pod to help identify what is wrong:

kubectl describe pod <pod name> -n <namespace>
Check the Events to see if you can spot what is wrong.

You may notice the pod's liveness probe is failing. If you look closely, you might also notice the path for the liveness probe looks like it may be incorrect.

In order to edit and fix the liveness probe, you will need to delete and recreate the pod. You should save the pod descriptor before deleting it, or you will have no way to recover it!

kubectl get pod <pod name> -n <namespace> -o yaml --export > broken-pod.yml
Delete the broken pod:

kubectl delete pod <pod name> -n <namespace>
Now, edit the descriptor file, and fix the path attribute for the liveness probe: vi broken-pod.yml.

Recreate the broken pod with the fixed probe:

kubectl apply -f broken-pod.yml -n <namespace>
Check to make sure the pod is now running properly:

kubectl get pod <pod name> -n <namespace>