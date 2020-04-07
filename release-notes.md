---

copyright:
  years: 2019, 2020
lastupdated: "2020-04-06"


keywords: release note, latest changes, Hyperledger Fabric

subcollection: blockchain-sw-213

---

{:note: .note}
{:important: .important}
{:tip: .tip}
{:shortdesc: .shortdesc}
{:pre: .pre}
{:external: target="_blank" .external}

# Release notes
{: #release-notes-saas-20}

<div style="background-color: #f4f4f4; padding-left: 20px; border-bottom: 2px solid #0f62fe; padding-top: 12px; padding-bottom: 4px; margin-bottom: 16px;">
  <p style="line-height: 10px;">
    <strong>Running a different version of IBM Blockchain Platform?</strong> Switch to version
    <a href="https://cloud.ibm.com/docs/blockchain-sw?topic=blockchain-sw-release-notes-saas-20">2.1.2</a>
    </p>
</div>


Use these release notes that are grouped by date to learn about the latest changes to {{site.data.keyword.blockchainfull}} Platform v2.1
{:shortdesc}


## 24 March 2020
{: #03-24-2020}







**Support for OpenShift Container Platform v4.2 on LinuxONE on s390x**

Enables IBM Z environments to participate fully in a multicloud architecture. Existing IBM Z applications running on Linux on IBM Z and z/OS can be extended to create a comprehensive multi-organizatioal blockchain network. 

**Hyperledger Fabric v1.4.6**

All new nodes are deployed using Hyperledger Fabric v1.4.6. If you have an existing blockchain network, you should review the topic on [Capabilities](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-govern#ibp-console-govern-capabilities) to understand how this new Fabric version can impact your network.

**Hardware Security Module (HSM) support for node identities**   

Full cryptographic HSM support is now available for HSMs that implement the PKCS #11 standard. Using an HSM provides on-demand encryption, key management, and key storage. When you deploy a CA, peer, or ordering node, you now have the option to store the private key for the node identity in an HSM. See [Configuring a node to use a HSM](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-adv-deployment#ibp-console-adv-deployment-cfg-hsm) for more details.

**Support for adding and removing ordering nodes from an existing ordering service**  

Previously, an ordering service could only contain one or five ordering nodes and they all were contributed from the same organization. Now, the ordering service can be deployed across multiple organizations in a blockchain network, enabling individual organizations to add and remove individual ordering nodes as required. Multi-organizational transaction ordering improves the decentralized nature of a blockchain network.  Learn more about the process in the new [Adding and removing Raft ordering service nodes tutorial](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-add-remove-orderer#ibp-console-add-remove-orderer).

**Ability to override default CA, peer, ordering node configuration**  

Hyperledger Fabric includes many configuration options for a CA, peer, or ordering node. A subset of those options for the [CA](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-adv-deployment#ibp-console-adv-deployment-ca-customization), [peer](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-adv-deployment#ibp-console-adv-deployment-peer-create-json) and [ordering node](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-adv-deployment#ibp-console-adv-deployment-orderer-create-json) can now be overridden by using the console or the [APIs](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-v2-apis#ibp-v2-apis-custom).

**Full Java smart contract development support**

In addition to smart contracts written in JavaScript, TypeScript, and Go programming languages, it is now possible to install and instantiate Java smart contracts from the console. Moreover, Java can be freely mixed and matched with other application and smart contract programming languages, including JavaScript, TypeScript, and Go. This heterogeneous programming language support enables an organization to capitalize on the full range of its development skills.

In order to use Java chaincode, developers should be aware that:

- Java 11 is required to execute Java smart contracts.
- Gradle v4.x and Maven v3.x are used to build Java smart contracts.
- Custom Gradle versions can be used by using a Gradle wrapper.
- Java smart contracts require the fabric-chaincode-shim at v1.4.6 or later, as this version is the first version that includes support for Java 11.
- For an example of a Java smart contract, see the [FabCar Java smart contract](https://github.com/hyperledger/fabric-samples/tree/release-1.4/chaincode/fabcar/java){: external} from Fabric v1.4.

**v2 APIs available**

New {{site.data.keyword.blockchainfull_notm}} Platform console APIs using the route `/v2/` are now available. Use of the earlier `/v1/` APIs continues to be supported. See [{{site.data.keyword.blockchainfull_notm}} Platform APIs](https://cloud.ibm.com/apidocs/blockchain) for more information.



## 17 December 2019
{: #12-17-2019}

### Release of {{site.data.keyword.blockchainfull_notm}} Platform v2.1.2
{: #12-17-2019-212}

#### Hyperledger Fabric v1.4.4
{: #12-17-2019-hlf144}

All new nodes are deployed using Hyperledger Fabric v1.4.4.

#### Support for OpenShift Container Platform (OCP) 4.1 and 4.2
{: #12-17-2019-ocp4.x}

In addition to supporting deployment on OCP 3.11, you can now also deploy the platform on OpenShift Container Platform 4.1 and 4.2.

#### Simplified component creation flows
{: #12-17-2019-flow}

Peer, CA, and ordering service creation has been streamlined. Now, when you create a node, you can select a checkbox to configure advanced deployment options.

#### Zone selection for ordering nodes
{: #12-17-2019-oszone}

If your Kubernetes cluster is configured across multiple zones, you now have the ability to select which zone an ordering node is deployed to.

#### Add peer to a channel from Channels tab
{: #12-17-2019-add-peer}

In addition to joining a channel from the peer node panel, a peer can now be joined to a channel directly from the Channels tab.

#### Anchor peer during join
{: #12-17-2019-add-anchor-peer}

When a peer is joined to a channel, you can now designate that peer as an anchor peer which bootstraps automatic communication between organizations. Anchor peers on your channel are a requirement if your client application uses Service Discovery or if your smart contract uses private data collections.

#### Export/Import all
{: #12-17-2019-export-import}

Allows for the bulk export and import of nodes, MSPs, and identities, rather than having to export and import these components one at a time. See this topic on [Exporting and importing in bulk](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-import-nodes#ibp-console-import-bulk-export-import) for more information.

#### Support for Fabric Node OU features
{: #12-17-2019-nodeOU}

In addition to the existing `client` and `peer` Node OU types that are available when you deploy a peer or ordering node, you now have two additional Node OU types to choose from: `admin` and `orderer`. Follow the [Build a network tutorial](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-build-network) for examples of which type to use when you deploy your nodes.

## 8 November 2019
{: #11-08-2019}


### Release of {{site.data.keyword.blockchainfull_notm}} Platform v2.1.1


#### {{site.data.keyword.blockchainfull_notm}} Platform images
{: #11-08-2019-images}


A purchase of {{site.data.keyword.blockchainfull_notm}} Platform v2.1.1 now includes an entitlement to peer, CA, ordering service, and smart contract container images that are signed and supported by {{site.data.keyword.IBM_notm}}. The images are based on the open source Fabric code base and contain a number of enhancements for stability and serviceability.

## 24 September 2019
{: #09-24-2019}

### Release of {{site.data.keyword.blockchainfull_notm}} Platform v2.1.0
{: #09-24-2019-210}

{{site.data.keyword.blockchainfull_notm}} Platform v2.1.0 allows you to deploy the platform on the Red Hat OpenShift Container Platform. {{site.data.keyword.blockchainfull_notm}} Platform v2.1.0 can be installed on any x86_64 architecture where Red Hat OpenShift Container Platform 3.11 runs and includes the console UI.
