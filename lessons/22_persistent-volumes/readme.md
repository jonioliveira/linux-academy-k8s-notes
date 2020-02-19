# State Persistence
Kubernetes is designe to manage stateless containers. Pods and containers can be easily deleted and/or replaced. When a container is removed, data stored inside the container's internal disk is lost.

State persistance refers to maintaining data outside and potencially beyond the life of a container.

This usually means storing data in some kind of persistent data store that can be accessed by containers.

Kubernetes allow us to implement persistent storage using PersistentVolumes and PersistentVolumesClaims.

**PersistentVolume** or **PV** - Represents a storage resource.
**PersistentVolumeClaim** or **PVC** - Abstraction layer between user (pod) and the PV
PVCs will automatically bind themselves to a PV that fas compatible StorageClass and accessModes.

- Pod:
  - PersistentVolumeClaim:
    [storageClass: fast]
    [accessModes: RWO]
    - PersistentVolume (will be choosed by PVC because of the same storageClass and acess mode)
      [storageClass: fast]
      [accessModes: RWO]
      - storage
  
    - PersistentVolume
      [storageClass: fast]
      [accessModes: RWO]
      - storage

## Notes (Persistent Volume):
-  storageClassNames: Defines different categories of storage+
-  capacity: storage amount for the PV
-  accessModes: Determines what read/write modes can be used to mount the volume
-  hostPath: Uses the node's local filesystem for storage

## Notes (Persistent Volume Claim:
- storageClassNames: Defines what StorageClass to use
- accessMode: Determines what read/write modes the claim needs
- resources.requests.storage: Defines how much storage the Claim needs

## Notes (Check status):
- kubectl get pvc
- kubectl get pv