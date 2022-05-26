### s2i-cli-tools

Utilizing the openshift-client `(oc)` image that is readily available within the cluster as a base image so that we can easily layer in additional cli tools that we may need. In this case, we are adding the `jq` package because it simplifies json parsing.

#### Directory Layout
| directory | purpose |
|:---------:|:--------|
|containerfiles| location of containerfile that gets included in build config.|
|manifests| openshift manifests for imagestream and buildconfig|
|cli-tools| Helm Chart for automated deployments of the buildconfig and imagestream|

#### Usage (manual installation)
The `oc` image is using `ubi8/ubi` as its base image - to add anything additional update 
the containerfile. 

To make the imagestream available to the entire cluster, you will need to create it in the `openshift` namespace. In order to do so, the user will need to have the `cluster-admin` role-binding.

`oc create -f cli-tools-is.yaml`

Create the buildconfig in whichever application project. The buildconfig will point to the configured git repository and apply the instructions from the dockerfile. 

`oc create -f cli-tools-bc.yaml`

Create an application in argocd, or install the chart locally in the cluster

`helm install cli-tools ./cli-tools`
