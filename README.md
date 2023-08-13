# KubernetesPractice

## Run curl command in a pod to retrieve all Pods in the `default` namespace through interaction with Kubernetes API server

### Prerequests
* Create a cluster with `default` namespace

### Steps
1. create a pod to run curl command by running below command(yml setting detail sees curl_pod.yml)
    kubectl apply -f curl_pod.yml
2. create a clusterRole and apply it by running below command(yml setting detail sees read_pod_rule.yml)
    kubectl apply -f read_pod_rule.yml
3. create a clusterRoleBinding of the ClusterRole just created by running below command(yml setting detail sees cluster_role_binding.yml)
    kubectl apply -f cluster_role_binding.yml
4. execute a shell inside the curl-pod container by running below command
    kubectl exec -it curl-pod -- /bin/sh
5. run curl command
    curl -k -H "Authorization: Bearer $(cat /var/run/secrets/kubernetes.io/serviceaccount/token)" \
    https://kubernetes.default.svc.cluster.local/api/v1/namespaces/default/pods
6. get all pods inside the `default` namespace