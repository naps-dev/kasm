# Kasm Workspaces Helm Chart

This is a proof-of-concept Helm chart for running Kasm workspaces in the cluster. It runs using port forwarding in our k8s cluster, but more work probably needs to be done with networking to get a good reliable connection between the front-end and the server.

**Must be run with priveleged context**
This container requires root privileges to run successfully. An exception must be made in OPA Gatekeeper to allow this container to run.

Exception should be made for default/kasm-workspaces in the CRD K8sPSPPrivilegedContainer2 under constratins.gatekeeper.sh

### Note on Health Checks
The health checks for this helm chart are setup to initially check for readiness on port 3000, which is the install endpoint.  After 5 minutes elapses since the start of the deployment, the liviness probe will check the health check endpoint of the api. As soon as the pod is deployed you must go to the 3000 endpoint to handle the initial configuration of kasm-workspaces. Once configured, the application will be live on port 443 and the health check will be reachable.
