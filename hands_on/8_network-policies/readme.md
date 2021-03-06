Your company has a set of services, one called inventory-svc and another called customer-data-svc. In the interest of security, both of these services and their corresponding pods have NetworkPolicies designed to restrict network communication to and from them. A new pod has just been deployed to the cluster called web-gateway, and this pod need to be able to access both inventory-svc and customer-data-svc.

Unfortunately, whoever designed the services and their corresponding NetworkPolicies was a little lax in creating documentation. In top of that, they are not currently available to help you understand how to provide access to the services for the new pod.

Examine the existing NetworkPolicies and determine how to alter the web-gateway pod so that it can access the pods associated with both services.

You will not need to add, delete, or edit any NetworkPolicies in order to do this. Simply use the existing ones and modify the web-gateway pod to provide access. All work can be done in the default namespace.

## Commands
**Inventory**
- First, get a list of existing NetworkPolicies:
  - kubectl get networkpolicy

- Examine inventory-policy more closely:
  - kubectl describe networkpolicy inventory-policy

- Note that the policy selects pods with the label app: inventory, and provides incoming and outgoing network access to all pods with the label inventory-access: true.

Modify the web-gateway pod with kubectl edit pod web-gateway.

Add the inventory-access: "true" label to the pod under metdadata.labels.

...
metdadata:
  labels:
    inventory-access: "true"
...

- Test access to the inventory-svc like so:
  - kubectl exec web-gateway -- curl -m 3 inventory-svc

**Customer-Data**

- Examine customer-data-policy more closely:
  - kubectl describe networkpolicy customer-data-policy
- Note that the policy selects pods with the label app: customer-data, and provides incoming and outgoing network access to all pods with the label customer-data-access: true.

Modify the web-gateway pod with kubectl edit pod web-gateway.

Add the customer-data-access: "true" label to the pod under metdadata.labels:

...
metdadata:
  labels:
    inventory-access: "true"
    customer-data-access: "true"
...

- Test access to the customer-data-svc like so:
  - kubectl exec web-gateway -- curl -m 3 customer-data-svc