<!-- This is an auto-generated file. DO NOT EDIT -->
# hello

* Needs: 
* Image: python:alpine3.6

# desc

1. `hello-executor-plugin-configmap.yaml` is created by `argo executor-plugin build .` 
  
only need create `server.py` and `plugin.yaml`, then exec `argo executor-plugin build .` will generate `hello-executor-plugin-configmap.yaml`

2. k8s 1.24 will not generate token auto, manual create by generate-token. need create for default sa in argo namespace. cannot work if create for argo sa

3. `plugin.yaml` `securityContext.runAsNonRoot: false, runAsUser: 0` run as root, demo use `runAsNonRoot: true`。but falied for
`Permission denied: '/var/run/argo/token'`

Install:

    kubectl apply -f hello-executor-plugin-configmap.yaml

Debugging:

    kubectl -n argo logs ${agentPodName} -c hello-executor-plugin   # -c for show pod.container's log

Uninstall:
	
    kubectl delete cm hello-executor-plugin 
