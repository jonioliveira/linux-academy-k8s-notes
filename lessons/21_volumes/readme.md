# Volumes
The internal storage of a container is ephemeral, meaning that it is design to be highly temporary. Volumes allow you to provide more permanent storage to a pod that exists beyond the life of a container.
 
 ## Notes:
 - EmptyDir: volumes create storage on a node when the pod is assigned to the node. The storage disappears when the pod leaves the node
 - 