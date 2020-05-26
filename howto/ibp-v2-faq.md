---

copyright:
  years: 2019, 2020
lastupdated: "2020-05-26"

keywords: FAQs, can I, upgrade, what version, peer ledger database, supported languages, why do I, regions

subcollection: blockchain-sw-213

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:note: .note}
{:important: .important}
{:tip: .tip}
{:faq: data-hd-content-type='faq'}
{:pre: .pre}


# FAQs
{: #ibp-v2-faq}

<div style="background-color: #f4f4f4; padding-left: 20px; border-bottom: 2px solid #0f62fe; padding-top: 12px; padding-bottom: 4px; margin-bottom: 16px;">
  <p style="line-height: 10px;">
    <strong>Running a different version of IBM Blockchain Platform?</strong> Switch to version
    <a href="https://cloud.ibm.com/docs/blockchain-sw?topic=blockchain-sw-ibp-v2-faq">2.1.2</a>
    </p>
</div>


**General**   

- [What is the value of using {{site.data.keyword.blockchainfull_notm}} Platform over native Hyperledger Fabric?](#ibp-v2-faq-v2-IBP-Overview-1-7)
- [Where can a customer deploy the {{site.data.keyword.blockchainfull_notm}} Platform and how will {{site.data.keyword.IBM_notm}} support those deployment environments?](#ibp-v2-faq-sw-support)
- [Does {{site.data.keyword.blockchainfull_notm}} Platform v2.1.x run on OpenShift on {{site.data.keyword.cloud_notm}}?](#ibp-v2-faq-saas-ocp)
- [How can I find what version of the {{site.data.keyword.blockchainfull_notm}} Platform that I am running?](#ibp-v2-faq-version)
- [What version of Hyperledger Fabric is being used with {{site.data.keyword.blockchainfull_notm}} Platform?](#ibp-v2-faq-v2-Hyperledger-Fabric-3-1)
- [What database do the peers use for their ledger?](#ibp-v2-faq-v2-IBP-Overview-1-3)
- [What languages are supported for smart contracts?](#ibp-v2-faq-v2-IBP-Overview-1-4)
- [Do you support using certificates from non-IBM Certificate Authorities (CAs)?](#ibp-v2-faq-v2-external-certs)
- [I am currently using Hyperledger Fabric v1.4 and want to move to {{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}} or Multicloud. Can I continue to use Raft?](#ibp-v2-faq-migrate-raft)
- [Is it possible to deploy blockchain nodes to multiple clouds from a single blockchain console?](#ibp-v2-faq-multicloud)
- [How can I find the examples and tutorials within the VSCode extension?](#ibp-v2-faq-vscode-tutorials)
- [Can the {{site.data.keyword.blockchainfull_notm}} Platform monitor the health of a client application?](#ibp-v2-faq-mon-client-app)
- [Is there a best practice for monitoring my blockchain resources?](#ibp-v2-faq-mon-res)
- [If service discovery is on, will an endorsement request be routed to any peer on the network?](#ibp-v2-faq-service-discovery)
- [What is the recommended way to manage private keys?](#ibp-v2-faq-hsm)
- [What ports are used by the {{site.data.keyword.blockchainfull_notm}} Platform?](#ibp-v2-ports)
- [Do ordering service Raft nodes use Transport Layer Security (TLS) for communication?](#ibp-v2-faq-raft-tls)
- [Can {{site.data.keyword.blockchainfull_notm}} Platform components interoperate with Hyperledger Fabric components on the same network? And vice versa? And what is the support policy for networks that include both {{site.data.keyword.blockchainfull_notm}} Platform components and open source components?](#ibp-v2-faq-interoperability)
- [What types of off-chain databases are supported with the {{site.data.keyword.blockchainfull_notm}} Platform?](#ibp-v2-faq-offchain-db)



## What is the value of using {{site.data.keyword.blockchainfull_notm}} Platform over native Hyperledger Fabric?
{: #ibp-v2-faq-v2-IBP-Overview-1-7}
{: faq}

Hyperledger Fabric is a powerful, versatile, pluggable, open source, distributed ledger technology capable of addressing a wide variety of use cases across many industries. {{site.data.keyword.blockchainfull_notm}} Platform is built on top of Fabric and includes integrated tools that provide end to end features for developers and network operators to develop, test, operate, monitor, and govern Hyperledger Fabric components by using an intuitive console UI. Quickly deploy an instance and use the streamlined console UI to [build a network](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-build-network), easily [install and instantiate smart contracts](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-smart-contracts), [govern your components](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-govern-components), and [govern your channel](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-govern). Interested in APIs? See the [{{site.data.keyword.blockchainfull_notm}} Platform API reference](https://cloud.ibm.com/apidocs/blockchain){: external}. With the {{site.data.keyword.blockchainfull_notm}} Platform, it is easy to extend a basic network, work with multicloud solutions, and receive {{site.data.keyword.IBM_notm}} worldwide support when needed. Finally, the {{site.data.keyword.blockchainfull_notm}} Platform provides additional security benefits that are essential for running an enterprise-grade production network.


## Where can a customer deploy the {{site.data.keyword.blockchainfull_notm}} Platform and how will {{site.data.keyword.IBM_notm}} support those deployment environments?
{: #ibp-v2-faq-sw-support}

For an updated list of all the {{site.data.keyword.blockchainfull_notm}} Platform deployment options check out the [Supported Platforms](/docs/blockchain-sw-213?topic=blockchain-sw-213-console-ocp-about#console-ocp-about-prerequisites).

It is important to note that the {{site.data.keyword.blockchainfull_notm}} support only spans across Hyperledger Fabric based component issues for customers who have purchased the Blockchain Platform. Some examples include assistance in Fabric upgrades, chaincode instantiation, adding peers to channels, etc.

On the other hand, {{site.data.keyword.blockchainfull_notm}} will not provide deployment support for environments outside of the supported platform. This means the customer is free to deploy into an environment of their choice from the list above, and should have the same {{site.data.keyword.blockchainfull_notm}} Platform experience as they would when they deploy into the {{site.data.keyword.cloud_notm}}. But it will be up to the customer to configure the network and address their own infrastructure related issues. Examples of these types of issues include failed deployment to a Kubernetes service, infrastructure capacity, custom firewall settings, etc.

## Does {{site.data.keyword.blockchainfull_notm}} Platform v2.1.x run on OpenShift on {{site.data.keyword.cloud_notm}}?
{: #ibp-v2-faq-saas-ocp}
{: faq}

Yes. The {{site.data.keyword.blockchainfull_notm}} Platform can be purchased and deployed in three ways on OpenShift:
- [{{site.data.keyword.blockchainfull_notm}} Platform for {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/catalog/services/blockchain-platform){: external} is deployed and runs on [IBM Cloud](https://cloud.ibm.com/kubernetes/catalog/openshiftcluster){: external}.
- {{site.data.keyword.blockchainfull_notm}} Platform is also available as a software offering that can be deployed on Red Hat OpenShift and can run in all environments where OpenShift Container Platform (OCP) is supported. Read more about running OpenShift Container Platform [here](/docs/blockchain-sw-213?topic=blockchain-sw-213-console-ocp-about).
- Finally, experienced Hyperledger Fabric customers also have the option to download and use the peer, CA, orderer, and smart contract container [images](/docs/blockchain-sw-213?topic=blockchain-sw-213-blockchain-images).


## How can I find what version of the {{site.data.keyword.blockchainfull_notm}} Platform that I am running?
{: #ibp-v2-faq-version}
{: faq}
{: support}

View the Support page by clicking the question mark icon <img src="../images/support-link.png" alt="Support link icon" width="30" style="width:30px; border-style: none"/> in the upper right corner of the page. The {{site.data.keyword.blockchainfull_notm}} Platform version is visible under the page heading.

## What version of Hyperledger Fabric is being used with {{site.data.keyword.blockchainfull_notm}} Platform?
{: #ibp-v2-faq-v2-Hyperledger-Fabric-3-1}
{: faq}

{{site.data.keyword.blockchainfull_notm}} Platform v2.1.3 uses Hyperledger Fabric v1.4.6 while {{site.data.keyword.blockchainfull_notm}} Platform v2.1.0 and 2.1.1 use Hyperledger Fabric 1.4.3.

## What database do the peers use for their ledger?
{: #ibp-v2-faq-v2-IBP-Overview-1-3}
{: faq}
{: support}

You have the choice of either CouchDB or LevelDB when you configure your peer database. Because data is modeled differently in a Couch database than in a Level database, the peers in a channel must all use the same database type. See [LevelDB versus CouchDB](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-adv-deployment#ibp-console-adv-deployment-level-couch) to decide what is best for your business needs.

## What languages are supported for smart contracts?
{: #ibp-v2-faq-v2-IBP-Overview-1-4}
{: faq}
{: support}

The {{site.data.keyword.blockchainfull_notm}} Platform supports smart contracts that are written in  Node.js, Golang, or JavaScript, and Java. The new Hyperledger Fabric programming model currently supports JavaScript, TypeScript, Java, and Go. If you are interested in preserving your existing application code, or by using Fabric SDKs for *Go*, you can still connect to your {{site.data.keyword.blockchainfull_notm}} Platform network by using the lower-level Fabric SDK APIs.

## Do you support using certificates from non-IBM Certificate Authorities?
{: #ibp-v2-faq-v2-external-certs}
{: faq}

Yes, you can bring your own certificates if they are issued by a CA that is X.509 compliant. The CA should sign by using ECDSA and the defaults should be set to use P256 curve. See this topic about [Using certificates from an external CA with your peer or ordering node](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-adv-deployment#ibp-console-adv-deployment-third-party-ca).

## I am currently using Hyperledger Fabric v1.4.x and want to move to {{site.data.keyword.blockchainfull_notm}} Platform v2.1.x. Can I continue to use Raft?
{: #ibp-v2-faq-migrate-raft}
{: faq}

Yes. The {{site.data.keyword.blockchainfull_notm}} Platform v2.1.x uses Raft consensus. All of the applications and smart contracts that you are using on Fabric 1.4.x are able to work on your {{site.data.keyword.blockchainfull_notm}} Platform network. However, no mechanism exists to migrate your ledger data from one network to another. Instead, you can reinstall your smart contract packages on your {{site.data.keyword.blockchainfull_notm}} Platform network. See also [Can IBM Blockchain Platform components interoperate with Hyperledger Fabric components on the same network?](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-v2-faq#ibp-v2-faq-interoperability).

## Is it possible to deploy blockchain nodes to multiple clouds from a single blockchain console?
{: #ibp-v2-faq-multicloud}
{: faq}

You cannot currently deploy blockchain nodes to multiple hosted cloud providers. However, you can use your console to operate a distributed multicloud network by importing nodes deployed by using consoles on other clouds.

## How can I find the examples and tutorials within the VSCode extension?
{: #ibp-v2-faq-vscode-tutorials}
{: faq}

The {{site.data.keyword.blockchainfull_notm}} Platform extension provides guided tutorials within VS Code to help you get started. You can find these tutorials on the extension home page when the extension is first installed. However, you can return to the tutorials and the home page by going to the extensions tab. For more information, see [Guided tutorials in VS Code](/docs/blockchain-sw-213?topic=blockchain-sw-213-develop-vscode#develop-vscode-guided-tutorials).

## Can the {{site.data.keyword.blockchainfull_notm}} Platform monitor the health of a client application?
{: #ibp-v2-faq-mon-client-app}
{: faq}

The {{site.data.keyword.blockchainfull_notm}} Platform console does not monitor the health of blockchain client applications, but {{site.data.keyword.cloud_notm}} does offer tooling such as [{{site.data.keyword.la_full_notm}}](/catalog/services/ibm-log-analysis-with-logdna){: external} and [{{site.data.keyword.mon_full_notm}}](/catalog/services/ibm-cloud-monitoring-with-sysdig){: external} that can be used for their health monitoring.

## Is there a best practice for monitoring my blockchain resources?
{: #ibp-v2-faq-mon-res}
{: faq}
{: support}

You are responsible for the health monitoring and resource allocation of the blockchain nodes in your Kubernetes cluster. While requests against the nodes are being actively processed, you should be monitoring for spikes in resource consumption to avoid problems.  You can configure a monitoring tool, such as [Sysdig](https://sysdig.com/platform/){: external} with alert notifications for the nodes in your cluster.

You should be aware that JavaScript and TypeScript smart contracts require more resources than contracts written in Go. Therefore, when you are allocating resources to your peer node, it is important to allocate sufficient resources and monitor the peer containers to ensure adequate resources are available to the peer when smart contracts are instantiated on a channel and during transaction processing.
{: tip}

## If service discovery is on, will an endorsement request be routed to any peer on the network?
{: #ibp-v2-faq-service-discovery}
{: faq}

Yes, if you have the endorsement policy set to “ANY”. However, you do have the opportunity to bind the policy directly to an organization's peers. The service discovery information provided by the peer supplies two pieces of information, `Layouts` and `EndorsersByGroup`. With these two pieces of data, the SDK has the ability to send requests to peers in different organizations that meet the endorsement policy requirements. The node.js SDK provides default code that uses the `Layouts` and `EndoresersByGroup` and sends the requests to the appropriate peers to meet the endorsement policy requirements. This existing logic can be customized to meet the business needs.

## What is the recommended way to manage private keys?
{: #ibp-v2-faq-hsm}
{: faq}

Because private keys are not stored by the platform, users are responsible for downloading and securing their private key. Therefore, when a higher level of security is required for private keys, an HSM is recommended. An HSM is a hardware appliance that performs cryptographic operations and provides the capability to ensure that the cryptographic keys never leave the HSM. Hyperledger Fabric supports HSM devices that implement the PKCS #11 standard. PKCS #11 is a cryptographic standard for secure operations, generation, and storage of keys. See [Configuring a node to use a Hardware Security Module (HSM)](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-adv-deployment#ibp-console-adv-deployment-cfg-hsm) to learn more.

## What ports are used by the {{site.data.keyword.blockchainfull_notm}} Platform?
{: #ibp-v2-ports}
{: faq}

See the port information in the [Security topic](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-security#ibp-security-ibp-ports).

## Do ordering service Raft nodes use Transport Layer Security (TLS) for communication?
{: #ibp-v2-faq-raft-tls}
{: faq}

Yes. The Raft ordering service nodes are configured to use TLS communication. TLS is embedded in the trust model of Hyperledger Fabric. By default, server-side TLS is enabled for all communications using TLS certificates. TLS is used to encrypt the communication between your nodes and as well as between your nodes and your applications. TLS prevents man-in-the-middle and session hijacking attacks. All {{site.data.keyword.blockchainfull_notm}} Platform components use TLS to communicate with each other.

## Can {{site.data.keyword.blockchainfull_notm}} Platform components interoperate with Hyperledger Fabric components on the same network? And vice versa? And what is the support policy for networks that include both {{site.data.keyword.blockchainfull_notm}} Platform components and open source components?
{: #ibp-v2-faq-interoperability}

Yes. Hyperledger Fabric networks consist of many distributed members owning one or more nodes. There are multiple deployment options:

* {{site.data.keyword.blockchainfull_notm}} Platform for IBM Cloud with console
* {{site.data.keyword.blockchainfull_notm}} Platform v2.1.x (Full Platform)  
* {{site.data.keyword.blockchainfull_notm}} Images
* Open source Hyperledger Fabric images or a non-IBM product

Containers deployed from any of the above sources can be connected on a single channel and transact. You can join IBM Blockchain Platform peers to any network running Hyperledger Fabric components. Similarly, you can invite Fabric peers to join channels hosted on an ordering service deployed on the IBM Blockchain Platform. Note that you will need to use Hyperledger Fabric APIs or the CLI. For more information about what is supported, see [Support for IBM Blockchain Platform v2.1.x](https://www.ibm.com/support/pages/support-ibm-blockchain-platform-v21x){: external}.

## What types of off-chain databases are supported with the {{site.data.keyword.blockchainfull_notm}} Platform?
{: #ibp-v2-faq-offchain-db}
{: faq}

As a best practice it is recommended that you do not query the entire blockchain ledger for the purpose of aggregation or reporting. If you want to build a dashboard or collect large amounts of data as part of your application, you can query an off chain database that replicates the data from your blockchain network. This allows you to understand the data on the blockchain without degrading the performance of your network or disrupting transactions.

You can use block or chaincode events from your application to write transaction data to an off-chain database or analytics engine. For each block received, the block listener application would iterate through the block transactions and build a data store by using the key/value writes from each valid transaction's read-write set. The [Peer channel-based event services](https://hyperledger-fabric.readthedocs.io/en/release-1.4/peer_event_services.html#peer-channel-based-event-services) provide replayable events to ensure the integrity of downstream data stores. For an example of how you can use an event listener to write data to an external database, see the [Off chain data sample](https://github.com/hyperledger/fabric-samples/tree/release-1.4/off_chain_data) in the Fabric samples.

Blockchain solutions can use any RDBMS or NoSQL DB such as IBM Cloudant for offchain data storage. Hyplerledger Fabric does not govern, interact with, or manage off-chain databases. In most cases, the off-chain database is used for reference data and non-transactional data. {{site.data.keyword.IBM_notm}} has successfully built blockchain products and solution accelerators with Hyperledger Fabric and NoSQL databases such as OrientDB. Additionally, {{site.data.keyword.IBM_notm}} offers an add-on solution, [Blockchain Document Store](/docs/blockchain-document-store?topic=blockchain-document-store-service-overview)(BDS), to coordinate document flow in a blockchain solution, both for on-chain and off-chain document storage.



