---

copyright:
  years: 2018, 2020
lastupdated: "2020-11-02"

keywords: IBM Blockchain Platform console, deploy, resource requirements, storage, parameters, delete, remove

subcollection: blockchain-sw-213

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:note: .note}
{:important: .important}
{:tip: .tip}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
 

# Removing your deployment
{: #Removing-k8}

<div style="background-color: #6fdc8c; padding-left: 20px; padding-right: 20px; border-bottom: 4px solid #0f62fe; padding-top: 12px; padding-bottom: 4px; margin-bottom: 16px;">
  <p style="line-height: 20px;">
    <strong>Important: You are not looking at the latest product documentation.  Make sure you are reading the documentation that matches the version of the software that you are using. Switch to product version </strong>
    <a href="/docs/blockchain-sw?topic=blockchain-sw-Removing-k8">2.1.2</a>, 2.1.3,
    <a href="/docs/blockchain-sw-25?topic=blockchain-sw-25-Removing-k8">2.5</a>,
    <a href="/docs/blockchain-sw-251?topic=blockchain-sw-251-Removing-k8">2.5.1</a>,
      <a href="/docs/blockchain-sw-252?topic=blockchain-sw-252-Removing-k8">2.5.2 (latest)</a>
    </p>
</div>


The {{site.data.keyword.blockchainfull}} Platform operator automatically restarts your blockchain nodes or your console if they stop or crash. As a result, you cannot manually remove your blockchain components by manually deleting their pods. Use the following steps to remove the {{site.data.keyword.blockchainfull_notm}} Platform from your cluster. You must follow these steps for each Kubernetes namespace that you create.

If your organization is participating in an active blockchain network, you should remove your organization from the network before you remove your deployment. See [Removing an organization](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-organizations#console-organizations-remove) for more details.
{: important}

## Step one: Use the console to delete your blockchain nodes

You can use your console to remove your blockchain node and any accompanying artifacts from your cluster. These artifacts include your ledger data in persistent storage and the keys that are stored in Kubernetes secrets. Log in to your console and go to the node overview page. Click **Delete** under the node name and enter the node name on the slider to permanently remove the node from the cluster. Note that you can delete a node only by using the console that created the node. You cannot use your console to delete nodes that are deployed on other clusters. You can also delete nodes by using the {{site.data.keyword.blockchainfull_notm}} Platform APIs.

If you cannot use your console or the APIs to remove your nodes, you can manually remove all of the nodes from your cluster by using the kubectl CLI. Navigate to your namespace:
```
kubectl config set-context --current --namespace=<NAMESPACE>
```
{:codeblock}

Then run the following commands to delete all of your blockchain nodes:
```
kubectl delete ibpca --all
kubectl delete ibppeer --all
kubectl delete ibporderer --all
```
{:codeblock}

## Step two: Delete the {{site.data.keyword.blockchainfull_notm}} Platform operator

You can use the kubectl CLI to remove the {{site.data.keyword.blockchainfull_notm}} Platform operator. When the operator is no longer running on your cluster, you can delete the console and any remaining nodes without them being restarted.

1. Log in to your cluster by using the kubectl CLI.

2. Use the CLI to set the context to the namespace that you created for your blockchain network:

  ```
  kubectl config set-context --current --namespace=<NAMESPACE>
  ```
  {:codeblock}

3. You can remove the operator deployment using the kubectl CLI:

  ```
  kubectl delete deployment ibp-operator
  ```
  {:codeblock}

## Step Three: Delete the {{site.data.keyword.blockchainfull_notm}} Platform console

After you remove the operator, you can then delete the console without it being restarted. When you are logged in to your cluster and are operating from your project, you can delete the console by issuing the following command:

```
kubectl delete ibpconsole --all
```
{:codeblock}

## Step Four: Remove policies and secrets

If you are done working with the {{site.data.keyword.blockchainfull_notm}} Platform on your Kubernetes cluster, you can delete your namespace.

```
kubectl delete namespaces <NAMESPACE>
```
{:codeblock}

This command deletes any remaining blockchain nodes that are running on the project, in addition to your console and the {{site.data.keyword.blockchainfull_notm}} Platform operator.
{:important}

Deleting the namespace removes the {{site.data.keyword.blockchainfull_notm}} Platform Security Context Constraint, clusterRole, and ClusterRoleBinding that you applied. It also deletes the secrets that you created. You cannot undo this action. As a result, deleting your project is not recommended unless you are not going to deploy another instance of the platform.
