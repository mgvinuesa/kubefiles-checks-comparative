# kubefiles-checks-comparative
Project to work with different tools such as kubeval, kubescore...

# Command line 
brew install kube-score
brew install kubeconform
helm plugin install https://github.com/jtyr/kubeconform-helm

helm create example-chart
 -
helm template example-chart/ | kube-score score -

```
manu@AT-5CD2144YCB:/mnt/c/Dev/github/mgvinuesa/kubefiles-checks-comparative$ helm template example-chart/ | kube-score score -
apps/v1/Deployment release-name-example-chart                                 💥
    [CRITICAL] Container Resources
        · example-chart -> CPU limit is not set
            Resource limits are recommended to avoid resource DDOS. Set
            resources.limits.cpu
        · example-chart -> Memory limit is not set
            Resource limits are recommended to avoid resource DDOS. Set
            resources.limits.memory
        · example-chart -> CPU request is not set
            Resource requests are recommended to make sure that the application
            can start and run without crashing. Set resources.requests.cpu
        · example-chart -> Memory request is not set
            Resource requests are recommended to make sure that the application
            can start and run without crashing. Set resources.requests.memory
    [CRITICAL] Container Security Context ReadOnlyRootFilesystem
        · example-chart -> The pod has a container with a writable root filesystem
            Set securityContext.readOnlyRootFilesystem to true
    [CRITICAL] Container Ephemeral Storage Request and Limit
        · example-chart -> Ephemeral Storage limit is not set
            Resource limits are recommended to avoid resource DDOS. Set
            resources.limits.ephemeral-storage
    [CRITICAL] Pod NetworkPolicy
        · The pod does not have a matching NetworkPolicy
            Create a NetworkPolicy that targets this pod to control who/what
            can communicate with this pod. Note, this feature needs to be
            supported by the CNI implementation used in the Kubernetes cluster
            to have an effect.
    [CRITICAL] Container Security Context User Group ID
        · example-chart -> The container is running with a low user ID
            A userid above 10 000 is recommended to avoid conflicts with the
            host. Set securityContext.runAsUser to a value > 10000
        · example-chart -> The container running with a low group ID
            A groupid above 10 000 is recommended to avoid conflicts with the
            host. Set securityContext.runAsGroup to a value > 10000
    [CRITICAL] Pod Probes
        · Container has the same readiness and liveness probe
            Using the same probe for liveness and readiness is very likely
            dangerous. Generally it's better to avoid the livenessProbe than
            re-using the readinessProbe.
            More information: https://github.com/zegl/kube-score/blob/master/README_PROBES.md
    [CRITICAL] Container Image Pull Policy
        · example-chart -> ImagePullPolicy is not set to Always
            It's recommended to always set the ImagePullPolicy to Always, to
            make sure that the imagePullSecrets are always correct, and to
            always get the image you want.
v1/Pod release-name-example-chart-test-connection                             💥
    [CRITICAL] Pod Probes
        · Container is missing a readinessProbe
            A readinessProbe should be used to indicate when the service is
            ready to receive traffic. Without it, the Pod is risking to receive
            traffic before it has booted. It's also used during rollouts, and
            can prevent downtime if a new version of the application is failing.
            More information: https://github.com/zegl/kube-score/blob/master/README_PROBES.md
    [CRITICAL] Container Resources
        · wget -> CPU limit is not set
            Resource limits are recommended to avoid resource DDOS. Set
            resources.limits.cpu
        · wget -> Memory limit is not set
            Resource limits are recommended to avoid resource DDOS. Set
            resources.limits.memory
        · wget -> CPU request is not set
            Resource requests are recommended to make sure that the application
            can start and run without crashing. Set resources.requests.cpu
        · wget -> Memory request is not set
            Resource requests are recommended to make sure that the application
            can start and run without crashing. Set resources.requests.memory
    [CRITICAL] Container Security Context ReadOnlyRootFilesystem
        · wget -> Container has no configured security context
            Set securityContext to run the container in a more secure context.
    [CRITICAL] Container Image Tag
        · wget -> Image with latest tag
            Using a fixed tag is recommended to avoid accidental upgrades
    [CRITICAL] Container Ephemeral Storage Request and Limit
        · wget -> Ephemeral Storage limit is not set
            Resource limits are recommended to avoid resource DDOS. Set
            resources.limits.ephemeral-storage
    [CRITICAL] Pod NetworkPolicy
        · The pod does not have a matching NetworkPolicy
            Create a NetworkPolicy that targets this pod to control who/what
            can communicate with this pod. Note, this feature needs to be
            supported by the CNI implementation used in the Kubernetes cluster
            to have an effect.
    [CRITICAL] Container Security Context User Group ID
        · wget -> Container has no configured security context
            Set securityContext to run the container in a more secure context.
```
helm kubeconform example-chart/
kubeconform -summary -verbose k8/
helm template example-chart/ | kubeconform -summary -verbose

kube-linter lint example-chart/
kube-linter lint k8/
helm template example-chart/ --output-dir /tmp/chart; kube-linter lint /tmp/chart
# Tools

## Kube-score
https://github.com/zegl/kube-score
https://github.com/zegl/kube-score/blob/master/README_CHECKS.md

## Kubeval
https://www.kubeval.com/
Desmantenido!!!!

## Kubeconform
https://github.com/yannh/kubeconform
Basado en kubeval
https://github.com/jtyr/kubeconform-helm


Comentar esto https://github.com/yannh/kubeconform#customresourcedefinition-crd-support

# Kubelinter
https://github.com/stackrox/kube-linter
https://docs.kubelinter.io/
https://github.com/stackrox/kube-linter/blob/main/docs/generated/checks.md
https://github.com/stackrox/kube-linter/issues/48

# Checkov
https://github.com/bridgecrewio/checkov
https://github.com/bridgecrewio/checkov/blob/main/docs/7.Scan%20Examples/Kubernetes.md
https://github.com/bridgecrewio/checkov/blob/main/docs/7.Scan%20Examples/Helm.md

# Kubevious
https://github.com/kubevious/kubevious

# Config-lint
https://github.com/stelligent/config-lint

#Kubeaudit
https://github.com/Shopify/kubeaudit

# Kube-Library y #conftest
testing https://github.com/devopsspiral/KubeLibrary/
https://github.com/open-policy-agent/conftest

# Evaluation
1. Installation
   1. Local 
   2. CI/CD Pipelines
2. Capacity / Checks
3. Integration with K8, Helm, Kustomize
4. Community Support
   1. Insights github
   2. Stars

# Bibliography

https://cloudentity.com/developers/blog/helm_chart_testing_tools/
https://kubevious.io/blog/post/top-kubernetes-yaml-validation-tools
https://thechief.io/c/editorial/7-kubernetes-security-scanners-to-use-in-your-devsecops-pipeline/
https://thechief.io/c/editorial/7-static-analysis-tools-to-secure-and-build-stable-kubernetes-clusters/
