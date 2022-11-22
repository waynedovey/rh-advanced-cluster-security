---
slug: step2
id: 2kb1eyjtbdsi
type: challenge
title: Cluster Management
notes:
- type: text
  contents: |-
    In the next learning module, we cover enabling ACS and the following Concepts:

    * Create the ACS Managed Cluster instances from the ACS Hub
    * Deploy the required import secrets and Kube config
    * Provision the Import files to the managed clusters
    * Verify the import and start managing the clusters

    Let's begin!
tabs:
- title: Work Terminal 1
  type: terminal
  hostname: container
- title: Visual Editor
  type: code
  hostname: container
  path: /root
- title: ACS Console
  type: website
  url: https://central-acs.crc-lgph7-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
- title: OCP Web Console
  type: website
  url: https://console-openshift-console.crc-lgph7-master-0.crc.${_SANDBOX_ID}.instruqt.io
  new_window: true
difficulty: advanced
timelimit: 6000
---
Login to the ACS Console with

admin/admin

![perspective-toggle](../assets/acs-login-console.png)

Login to the ACS Cluster

```
oc login -u admin -p admin https://api.crc.testing:6443 --insecure-skip-tls-verify=true
```

###TODO ADD the TOKEN##


Export the ACS Central Route

```
ROX_CENTRAL_ADDRESS=$(oc get route -n acs | awk '{print $2}' | grep -v HOST | head -n 1)
```

Start the management of Spoke1

```
export CLUSTER_NAME=spoke1
```

Enable the RHACS Helm Charts

```
helm repo add rhacs https://mirror.openshift.com/pub/rhacs/charts/
```

Create the Init Bundle for Spoke1

```
roxctl -e "$ROX_CENTRAL_ADDRESS:443" --token-file=TOKEN.txt central init-bundles generate ${CLUSTER_NAME} --output ${CLUSTER_NAME}_init_bundle.yaml --insecure-skip-tls-verify=true
```

Login to the Spoke1 cluster

```
oc login --token=superSecur3T0ken --server=http://${CLUSTER_NAME}:8001
```

Install the ACS service on Spoke1

```
helm install -n stackrox --create-namespace stackrox-secured-cluster-services rhacs/secured-cluster-services -f ${CLUSTER_NAME}_init_bundle.yaml --set clusterName=$CLUSTER_NAME --set centralEndpoint=$ROX_CENTRAL_ADDRESS:443 --set imagePullSecrets.allowNone=true
```


Start the management of Spoke2

```
export CLUSTER_NAME=spoke2
```

Create the Init Bundle for Spoke2

```
roxctl -e "$ROX_CENTRAL_ADDRESS:443" --token-file=TOKEN.txt central init-bundles generate ${CLUSTER_NAME} --output ${CLUSTER_NAME}_init_bundle.yaml --insecure-skip-tls-verify=true
```

Login to the Spoke2 cluster

```
oc login --token=superSecur3T0ken --server=http://${CLUSTER_NAME}:8001
```

Install the ACS service on Spoke2

```
helm install -n stackrox --create-namespace stackrox-secured-cluster-services rhacs/secured-cluster-services -f ${CLUSTER_NAME}_init_bundle.yaml --set clusterName=$CLUSTER_NAME --set centralEndpoint=$ROX_CENTRAL_ADDRESS:443 --set imagePullSecrets.allowNone=true
```

Completed, move onto the next assignment.
