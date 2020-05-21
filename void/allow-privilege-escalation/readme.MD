Tested.

To work within the constraint you have to:

Set resource limits for CPU and MEM:

resources:
  limits:
    cpu: "1"
    memory: "500Mi"

And set:

securityContext:
  allowPrivilegeEscalation: false
  
