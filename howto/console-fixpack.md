---

copyright:
  years: 2019, 2020
lastupdated: "2020-04-10"

keywords: Kubernetes, IBM Blockchain Platform console, deploy, resource requirements, storage, parameters

subcollection: blockchain-sw-213

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:note: .note}
{:important: .important}
{:tip: .tip}
{:pre: .pre}

# Installing the {{site.data.keyword.blockchainfull_notn}} Platform v2.1.3 Fix Pack
{: #install-fixpack}

<div style="background-color: #f4f4f4; padding-left: 20px; border-bottom: 2px solid #0f62fe; padding-top: 12px; padding-bottom: 4px; margin-bottom: 16px;">
  <p style="line-height: 10px;">
    <strong>Running a different version of IBM Blockchain Platform?</strong> Switch to version
    <a href="https://cloud.ibm.com/docs/blockchain-sw?topic=blockchain-sw-install-fixpack">2.1.2</a>
    </p>
</div>


Users who installed the {{site.data.keyword.blockchainfull_notn}} Platform v2.1.3 before April 16, 2020 should apply the v2.1.3 Fix Pack. The Fix Pack contains important bug fixes and should be applied to your network as soon as possible. If you installed the {{site.data.keyword.blockchainfull_notn}} Platform v2.1.3 after April 16, 2020, the bug fixes in the Fix Pack will have been incorporated into the platform, and it is not necessary to apply the Fix Pack.
{:shortdesc}

You can install the Fix Pack by updating the {{site.data.keyword.blockchainfull_notn}} Platform deployment on your Kubernetes cluster to pull the latest images from the {{site.data.keyword.IBM_notm}} Entitlement registry. The Fix Pack is applied by using the following steps:

1. [Apply fix to the {{site.data.keyword.blockchainfull_notm}} Platform operator](#install-fixpack-operator)
2. [Apply fix to the {{site.data.keyword.blockchainfull_notm}} console](#install-fixpack-console)
3. [Apply fix to your blockchain nodes](#install-fixpack-nodes)

You will need to apply the Fix Pack for each network that you deployed. Complete the steps for installing Fix Pack for each network that runs on a separate namespace. If you experience any problems, see the instructions for [rolling back the Fix Pack](#upgrade-k8-rollback). You can install the Fix Pack without disrupting a running network. However, you cannot use the console to deploy new nodes, install or instantiate smart contracts, or create new channels during the process.

## Before you begin

To upgrade your network, you need to [retrieve your entitlement key](/docs/blockchain-sw-213?topic=blockchain-sw-213-deploy-k8#deploy-k8-entitlement-key) from the My {{site.data.keyword.IBM_notm}} Dashboard, and [create a Kubernetes secret](/docs/blockchain-sw-213?topic=blockchain-sw-213-deploy-k8#deploy-k8-docker-registry-secret) to store the key on your namespace. If the Entitlement key secret was removed from your cluster, or if your key is expired, then you need to download another key and create a new secret.

## Step one: Apply fix to the {{site.data.keyword.blockchainfull_notm}} operator
{: #install-fixpack-operator}

You can apply the Fix Pack to the {{site.data.keyword.blockchainfull_notm}} operator by fetching the operator deployment spec from your cluster.

Log in to your cluster by using the kubectl CLI. Run the following command to get the name of the names of your Kubernetes namespaces `kubectl get namespace`. You will need to reference the namespace of the {{site.data.keyword.blockchainfull_notm}} network that you apply the fix to in future commands.

Run the following command to download the operator deployment spec to your local file system. Replace `<namespace>` with the name of our namespace:
```
kubectl get deployment ibp-operator -n <namespace> -o yaml > operator.yaml
```
{:codeblock}

Open `operator.yaml` in a text editor and save a new copy of the file as `operator-fixpack.yaml`. You need to update the `image:` field with the operator image that contains the bug fixes. You can find the name and tag of the latest operator image below:
```
cp.icr.io/cp/ibp-operator:2.1.3-20200416-amd64
```
{:codeblock}

Save the file on your local system. You can then issue the following command to apply the fix to the {{site.data.keyword.blockchainfull_notm}} operator:
```
kubectl apply -f operator-fixpack.yaml
```
{:codeblock}

You can use the `kubectl get deployment ibp-operator -o yaml` command to confirm that the fix was applied.

After you apply the `operator-fixpack.yaml` operator spec to your namespace, the operator will restart and pull the latest image. The upgrade takes about a minute. While the operator is restarting, you can still access your console UI. However, you cannot use the console to install and instantiate chaincode, or use the console or the APIs to create or remove a node.

You can check that the fix was applied successfully by running `kubectl get deployment ibp-operator`. If the upgrade is successful, then you can see the following tables with four ones displayed for your operator and your console.
```
NAME           READY     UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1       1            1           1m
```

If you experience a problem while you are upgrading the operator, go to this [troubleshooting topic](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-v2-troubleshooting#ibp-v2-troubleshooting-deployment-cr) for a list of commonly encountered problems. You can run the command to apply the original operator file, `kubectl apply -f operator.yaml` to restore your original operator deployment.

## Step two: Apply fix to the {{site.data.keyword.blockchainfull_notm}} console
{: #install-fixpack-console}

After you the new images to the {{site.data.keyword.blockchainfull_notm}} operator, you need to apply the Fix Pack to your console. The console will download the latest images used by the console, in addition to the new images for your blockchain nodes.

You can apply the fix to your console by removing artifacts that were created when the V2.1.2 console was deployed. Removing these artifacts will allow your console to pull the latest images and configuration of the Fix Pack from your operator.

First you need to fetch the configmap that was created by console.
```
kubectl get configmap -n <namespace>
```
Find the configmap of your console from the list of results. You will be able to see the word console in the configmap name. You can the use the following command to delete the console configmap. Replace `<console-configmap>` with the console configmap name from the previous command.
```
kubectl delete configmap -n <namespace> <console-configmap>
```

You then need to fetch the console deployment:
```
kubectl get deployment -n <namespace>
```
Find the deployment of your console from the list of results. The deployment is often called `ibpconsole`. You can use the following command to delete the console deployment. Replace `<console-configmap>` with the name of the console deployment from the previous command.
```
kubectl delete deployment -n <namespace> <console-deployment>
```

After you delete the console deployment and configmap, the console will download the new images and configuration of the v2.1.3 Fix Pack. You can pull the updated deployment and configmap to confirm that the console picked up the images of the Fix Map.
```
kubectl get deployment -n <namespace> ibpconsole -o yaml
kubectl get configmap -n <namespace> ibpconsole-configmap -o yaml
```

The new images will have the tags fdfdfd


You can check that the upgrade is complete by running `kubectl get deployment ibp-operator`. If the upgrade is successful, then you can see the following tables with four ones displayed for your operator and your console.
```
NAME           READY     UP-TO-DATE   AVAILABLE   AGE
ibp-operator   1/1       1            1           1m
```

## Step three: Apply fix to your blockchain nodes
{: #install-fixpack-nodes}

After you apply the fix to your console, you need to use your console UI to update the nodes of your blockchain network. Browse to the console UI open the nodes overview tab. To apply a patch to a node, open the node tile and click the **Install patch** button. You cannot patch nodes that you imported to the console.

Apply patches to nodes one at a time. Your nodes are unavailable to process requests or transactions while the patch is being applied. Therefore, to avoid any disruption of service, you need to ensure that another node of the same type is available to process requests whenever possible. Installing patches on a node takes about a minute to complete and when the update is complete, the node is ready to process requests.
{:important}


### Roll back the Fix Pack
{: #install-fixpack-rollback}

When you apply the Fix Pack to your operator, it saves the secrets, deployment spec, and network information of your console before it restarts and attempts to apply the fixes to the console. If the Fix Pack fails for any reason, {{site.data.keyword.IBM_notm}} Support can roll back your upgrade and restore your previous deployment by using the information on your cluster. If you need to roll back your upgrade, you can submit a support case from the [mysupport](https://www.ibm.com/support/pages/support-ibm-blockchain-platform-v21x){: external} page.

You can roll back an upgrade after you use the console to operate your network. However, after you use the console to upgrade your blockchain nodes, you can no longer roll back your console to a previous version of the platform.
