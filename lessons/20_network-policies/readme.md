#Netowrk Policies
By default, all pods in the cluster can communitcate with any other pods, and reach out to any available IP. 
**Network Policies** allow you to limit what network traffic is allowed to and from pods in your cluster. 

## install package netowrk policies
wget -O canal.yaml https://docs.projectcalico.org/v3.5/getting-started/kubernetes/installation/hosted/canal/canal.yaml

kubectl apply -f canal.yaml

## Use this command to get the cluster IP address of the Nginx pod:
kubectl get pod network-policy-secure-pod -o wide

## Use the secure pod's IP address to test network access from the client pod to the secure Nginx pod:
kubectl exec network-policy-client-pod -- curl <secure pod cluster ip address>

## Get information about NetworkPolicies in the cluster:
kubectl get networkpolicies
kubectl describe networkpolicy my-network-policy

# Notes: 
- podSelector: Determines which pods the NetowrkPolicy applies to
- policyType Sets whether the policy governs incoming traffic (ingress), outgoing traffic (egress), or both.
- ingress: Rules for incoming traffic
- egress: Rules for outgoing traffic
- rules: Both ingress and egress rules are whitelist-based, meaning that any traffic that does not match at least one rule will be blocked.
  - ports: Specifies the protocols and ports that match the rule
  - from/to selectors: Specifies the source(s) and destination(s) of network traffic that matches the rule
