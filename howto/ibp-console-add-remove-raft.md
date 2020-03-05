---

copyright:
  years: 2020
lastupdated: "2020-03-05"

keywords: network components, Kubernetes, channel update, channels, governance, channel configuration, orderer, ordering node, ordering service, raft, tutorial

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

# Adding and removing ordering service nodes
{: #ibp-console-add-remove-orderer}

<div style="background-color: #f4f4f4; padding-left: 20px; border-bottom: 2px solid #0f62fe; padding-top: 12px; padding-bottom: 4px; margin-bottom: 16px; font-family: 'IBM Plex Sans', 'Helvetica Neue', Arial, sans-serif;">
  <p style="line-height: 10px;">
    <strong>Running a different version of IBM Blockchain Platform?</strong> Switch to version
    <a href="https://cloud.ibm.com/docs/blockchain-sw?topic=blockchain-sw-ibp-console-add-remove-orderer.">2.1.2</a>
    </p>
</div>


In this tutorial, we'll talk about the process for creating ordering nodes to add to an existing ordering service and to existing channels. This will cover not just the instructions for adding nodes using the same organization that created the ordering service and as a separate ordering organization that is added as an ordering service admin.

Because ordering service nodes can only belong to a single ordering service, if you create an ordering service node from the main **Nodes** panel, you will not be able to add it to an existing ordering service. If you want to add a node to an existing ordering service, the node must be created specifically for that purpose using the process described below. Also, be aware that **adding nodes to an ordering service does not automatically add them to any existing channel**. That is a separate process that must take place after the node has been added to the ordering service. For more information, see [Adding and removing ordering service consenters](/docs/blockchain?topic=blockchain-ibp-console-add-remove-orderer#ibp-console-add-remove-orderer-consenters).
{:important}

## Number of ordering nodes
{: #ibp-console-add-remove-orderer-suggested-ordering-node-configurations}

While it's technically possible to build a configuration of any number of ordering nodes (no configuration is explicitly restricted), some numbers provide a better balance between cost and performance than others. The reason for this lies in satisfying the needs of high availability (HA) and in understanding the Raft concept of the "quorum", the minimum number of nodes that must be available (out of the total number) for the ordering service to process transactions.

In Raft, a **majority of the total number of nodes** is needed to form a quorum. In other words, if you have one node, you need that node available to have a quorum, because the majority of one is one. Similarly, if you have two nodes, you will need both available, since the majority of two is two (for this reason, a configuration of two nodes is discouraged; there is no advantage to a two node configuration). In a similar vein, the majority of three is two, the majority of four is three, the majority of five is three, and so on.

While satisfying the quorum will make sure the ordering service is functioning, production networks also have to think about deployment configurations that are highly available (in other words, configurations in which the loss of a certain number of nodes can be tolerated by the system). Typically, this means tolerating two nodes failing: one node going down during a normal maintenance cycle, and another going down for any other reason (such as a power outage or error).

This is why, by default, the console offers two options: one node or five nodes. Recall that the majority of five is three. This means that in a five node configuration, the loss of two nodes can be tolerated. If your configuration features four nodes, only one node can be down for any reason before **another** node going down means a quorum has been lost and the ordering service will stop processing transactions.

For this reason, it is considered a best practice to have an odd number of nodes in an ordering service. There is nothing wrong with an even number of nodes, but they add costs without making the ordering service more highly available.

Because the number of nodes need for a quorum is updated automatically when nodes are added to the consenter set, it is a best practice to make sure that all of the nodes in the consenter set are servicing the channel before attempting to add a new node. This is because the consenter set is updated before the node has finished provisioning. For example, if you have three nodes servicing a channel, you will have a quorum as long as two nodes are up. When attempting to add a new node, the consenter set will index to three nodes being needed (out of four). In a case where only two nodes are up out of three when a new node is added, and the new node fails to provision for any reason, you will only have two nodes available out of the three that are needed.
{:tip}

## Creating and adding a node to the ordering service
{: #ibp-console-add-remove-orderer-add-orderer}

Adding a node to the ordering service is, at a high level, a three step process.

1. Create the node to be added to an existing ordering service.
2. Add the node to the ordering system channel. While this might seem logically similar to creating the node, it involves a different step. For more information, see [Adding the node to the ordering system channel](#ibp-console-add-remove-orderer-consenter-system-channel).
3. [Add the node to any application channels](#ibp-console-add-remove-orderer-consenters-add) where you want it to become a consenter.

If you have already created an ordering service, you can reuse the CA, MSP, node identity, and admin identity you created as part of that process when creating the new node and can skip down to the [Create the node](#ibp-console-add-remove-orderer-add-orderer-create) section below. If you are creating the node using a separate console and separate organization, proceed to [Create the node using a separate org and console](#ibp-console-add-remove-orderer-add-orderer-create).

### Create the node using a separate org and console
{: #ibp-console-add-remove-orderer-add-orderer-create}

If an organization other than the organization that created the ordering service wishes to create a new node, they will need to complete several steps. For the purpose of this tutorial, assume a user has followed the [Build a network tutorial](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-build-network) in their console and has created a peer, ordering service, and an application channel. **As a separate user with a separate console, you wish to add a node to that ordering service, which is called `Ordering Service`**.

1. Create a CA and an MSP. This process is identical to the process described in [Creating your ordering service organization CA](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-build-network#ibp-console-build-network-create-orderer-ca) from the Build a network tutorial. However, use the following values:

**Task: Create a CA and register users**

  | **Field** | **Description** | **Enroll ID** | **Secret** |
  | ------------------------- |-----------|-----------|-----------|-----------|
  | **Create CA** | Ordering Service2 CA | admin | adminpw |
  | **Register users** | Ordering Service2 admin | OS2admin | OS2adminpw |
  |  | Ordering Service node identity |  OS2 | OS2pw |
  {: caption="Table 1. Create a CA and register users" caption-side="bottom"}

If you are using a separate console, it is possible to specify exactly the same values for these fields as was specified in the Build a network tutorial. Only the `mspid` from the fields below must be different than `osmsp`, as two different MSPs cannot have the same ID in the same console (the MSP you create here will be exported to the other console in a future step). However, we have given different values in this tutorial in case users are running this tutorial inside the same console.
{:tip}

After your CA has been created and your identities have been registered, create the MSP representing your organization and an admin representing that organization using the following values:

**Task: Create the ordering service organization MSP definition**

  |  | **Display name** | **MSP ID** | **Enroll ID**  | **Secret** |
  | ------------------------- |-----------|-----------|-----------|-----------|
  | **Create Organization** | Ordering Service2 MSP | os2msp |||
  | **Root CA** | Ordering Service2 CA ||||
  | **Org Admin Cert** | |  | OS2admin | OS2adminpw |
  | **Identity** | Ordering Service2 MSP Admin |||||
  {: caption="Table 11. Create the ordering service organization MSP definition" caption-side="bottom"}

#### You: export your MSP and import the ordering service
{: #ibp-console-add-remove-orderer-add-orderer-export-MSP}

Now that you have created your MSP, you need to export it to the console where the ordering service was created. You should have downloaded a copy of your MSP to your local machine when it was created, but if you have not yet done so, download the MSP now. Then send the JSON to the user of the other console.

Until your organization is an administrator of the ordering service, you cannot add a new node to it.

#### Other console: import the ordering service
{: #ibp-console-add-remove-orderer-add-orderer-import-ordering-service}

The user of the other console must take your MSP and add it to its console by clicking on the **Organizations** tab and then the **Import MSP definition** tab. This MSP can then be added as an ordering service administrator by clicking on the tile representing the ordering service and then the **Add ordering service administrator** tab.

After the MSP has been added as an ordering service administrator, the user of the console where the ordering service was created must export the ordering service back to your console (the console where the new node is being added from). To export a node, navigate to the node and click on the download button. Then send the JSON file to the user of the other console.

After you have imported the ordering service, you will be able to create the new node for it.

### Create the node
{: #ibp-console-add-remove-orderer-add-orderer-create}

While it is not possible to ensure that the ordering service is available (that is, that a quorum of nodes are up and that a leader has been elected) without [Viewing your node logs](/docs/blockchain?topic=blockchain-ibp-console-manage-console#ibp-console-manage-console-node-logs), it is a best practice to minimally ensure the likelihood that a quorum exists by ensure that the pods where the nodes have been deployed are available. This can be done by checking to make sure the relevant pods are active in the Kubernetes dashboard or by issuing `kubectl get pods -n <namespace>` and checking on the pods. If you do not have access to the cluster where all of the ordering nodes were created, contact the administrator of the relevant clusters. **If a quorum of nodes is not available, it will not be possible to add another node to the ordering service**.
{:tip}

To add a node, click on the tile representing the node in the **Nodes** panel. Then click on the **Ordering nodes** panel and the **Add another node** tile. This will open a series of panels similar to the process for creating an ordering service. You will need to:

* **Give the node a display name**. A best practice will be to give the node a display name that matches the pattern used for the other nodes in the ordering service. By default, nodes are given the name `<name of ordering service>_1`, `<name of ordering service>_2`, and so on.
* **Select a CA**. This should be the CA used to create your MSP.
* **Enter an enroll ID and secret**. Again, if you created an enroll ID and secret for your existing ordering nodes, you may use the same enroll ID and secret here.
* **Select an MSP**. If you are adding to an ordering service you created in your console, reuse the MSP you used when creating that ordering service. If the new node is being added to an ordering service created elsewhere, use the MSP you exported to that console.
* **Allocate resources**. If the original set of ordering nodes was created using a custom allocation, it is a best practice to mimic that allocation when adding new nodes.
* **Associate identity**. You will only have to associate an identity if you are using a different MSP from the MSP that was originally used when creating the ordering service.

**Task: Create an ordering service**

  |  | **Display name** | **MSP ID** | **Enroll ID** | **Secret** |
  | ------------------------- |-----------|-----------|-----------|-----------|
  | **Add another node** | Ordering Service_2 ||||
  | **CA** | Ordering Service2 CA ||||
  | **Ordering Service Identity** | |  | OS2 | OS2pw |
  | **Organization MSP** | | os2msp |||
  | **Administrator certificate** | Ordering Service2 MSP ||||
  | **Associate identity** | Ordering Service2 MSP Admin   |||||
  {: caption="Table 2. Create an ordering service" caption-side="bottom"}

After reviewing the **Summary** page, click **Add another node**. This will submit the creation request.

To complete the process of adding the node, you need to add it to the consenter set of the system channel. For information about how to do that, proceed to the next section.

### Adding the node to the ordering system channel
{: #ibp-console-add-remove-orderer-consenter-system-channel}

After the ordering node has been successfully added, a new tile with the name of the node will appear on the **Ordering nodes** page. It will say it "Requires attention". This state reflects the fact that, while the node creation process has been successful, the node is not yet part of the consenter set of the system channel. The node must be added to the system channel before it can be added to any of the application channels.

Recall that the "consenter set" refers to the ordering service nodes actively participating in the ordering process on a channel, while the "system channel", which is managed by the ordering service, is the foundation of a network and forms the template for application channels.
{:tip}

To add the node you created to the system channel, click on the node. You will see a **Add node to ordering service** button. Click this button. After the node has been added to the ordering service, the node should now be part of the system channel.

Note that **it will take a few minutes for the new node to sync with ordering service in the system channel**. During this time, you may see a message that your ordering service is down. This is normal --- the ordering service must come down while the new node is syncing.

After the node has successfully been created and added to the system channel, export a JSON representing the node back to the console where the ordering service was created.

Note that **if you want to add this node to any existing application channels, you will have to add them to consenter set of each of those channels** separately. For information about how to do that, see [Adding an ordering node to the consenter set](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-add-remove-orderer#ibp-console-add-remove-orderer-consenters-add) of a channel.

### Adding the node to an application channel
{: #ibp-console-add-remove-orderer-consenters-add}

To add a consenter to an application channel, navigate to the channel and click the edit button. After specifying your org MSP and admin identity, click on the **Ordering service consenters** panel. Then select the node from the drop down list and click **Add**. Note that you will only be able to add one node at a time.

**It will take a few minutes for the new node to sync with the consenter set of the application channel**. During this time, the ordering service may be down. After the node has been successfully added to the application channel, you will see it in the **Ordering nodes** tab.

## Removing ordering service nodes
{: #ibp-console-add-remove-orderer-consenters-remove}

If a user wants to delete an ordering node, it must first remove the node from all channels where it is a consenter. This is because the console does not distinguish between a deleted node and an unavailable node, and will keep an ordering node as part of its consenter set until it is removed.

As a result, when you delete a node, a check is performed to see if it is a consenter on any channels. If it is, you will not be able to delete the node until it has been removed as a consenter from all channels. After removing the node as a consenter from all channels, you will be able to delete the node by clicking the trash can icon. Note that this action will have to be taken in the console where the node was created.

