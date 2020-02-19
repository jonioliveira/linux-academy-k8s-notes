Deployments provide a way to declaratively manage a dynamic set of replica pods.
They provide powerfull functionality such as scaling and rolling updates.

A deployment defines a desired state for replica pods, the cluster will constantly work to maintain that desired state, createing, removing and modifying the replica pods accordingly.

- Deployment
  [pod template]
  [selector: app=my-app]
  
  - Pod replica 1
    [label app: my-app]

  - Pod replica 2
    [label app: my-app]

NOTES:
spec.replicas - the number of ther replicas of the pod
spec.selector - the deployment will manage all pods whose labels match this selector
spec.template - A template pod descriptor which will be created