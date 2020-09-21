---

copyright:
  years: 2017, 2020
lastupdated: "2020-09-21"

keywords: IBM Blockchain Platform, release, new features

subcollection: blockchain-sw-213

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:note: .note}
{:important: .important}
{:tip: .tip}
{:external: target="_blank" .external}

# What's new
{: #whats-new}

<div style="background-color: #6fdc8c; padding-left: 20px; padding-right: 20px; border-bottom: 4px solid #0f62fe; padding-top: 12px; padding-bottom: 4px; margin-bottom: 16px;">
  <p style="line-height: 20px;">
    <strong>Important: You are not looking at the latest product documentation.  Make sure you are reading the documentation that matches the version of the software that you are using. Switch to product version </strong>
    <a href="https://cloud.ibm.com/docs/blockchain-sw?topic=blockchain-sw-whats-new">2.1.2</a>,
    <a href="https://cloud.ibm.com/docs/blockchain-sw-25?topic=blockchain-sw-25-whats-new">2.5 (latest)</a>
    </p>
</div>

## June 18, 2020
{: #whats-new-06-18-2020}

{{site.data.keyword.blockchainfull}} Platform 2.5 is now available.

{{site.data.keyword.blockchainfull_notm}} Platform 2.5 provides tighter integration with Red Hat solutions, including additional deployment options on Red Hat OpenShift 4.3 and support for Ansible Playbooks and Red Hat CodeReady Workspaces. To learn more about the new features see the []{{site.data.keyword.blockchainfull_notm}} Platform 2.5 documentation](/docs/blockchain-sw-25?topic=blockchain-sw-25-whats-new){: external}.

If you have an existing {{site.data.keyword.blockchainfull_notm}} Platform v2.1.x deployment and are interested in upgrading to {{site.data.keyword.blockchainfull_notm}} Platform 2.5, see the following topics in the {{site.data.keyword.blockchainfull_notm}} Platform 2.5 documentation:
- [Upgrading your console and components on the OpenShift Container Platform](/docs/blockchain-sw-25?topic=blockchain-sw-25-upgrade-ocp)
- [Upgrading your console and components on Kubernetes](/docs/blockchain-sw-25?topic=blockchain-sw-25-upgrade-k8)
- [Upgrading the {{site.data.keyword.blockchainfull_notm}} images](/docs/blockchain-sw-25?topic=blockchain-sw-25-blockchain-images#blockchain-images-upgrade)  

This update also helps organizations accelerate deployment through support of Ansible, an open source tool that automates provisioning, configuration management, and application deployment. Available in both {{site.data.keyword.blockchainfull_notm}} Platform v2.1.3 and 2.5, **Ansible Content Collections** are packages of modules, plug-ins, and other Ansible content that automate these processes. The platform has published a set of Ansible Content Collections to help organizations deploy blockchain components and networks with greater speed. See [Getting started with Ansible playbooks on the {{site.data.keyword.blockchainfull_notm}} Platform](/docs/blockchain-sw-213?topic=blockchain-sw-213-ansible) to learn more.

## March 24, 2020
{: #whats-new-03-24-2020}


{{site.data.keyword.blockchainfull}} Platform v2.1.3 is now available.


The following enhancements are included in this latest release:
- Red Hat OpenShift on LinuxONE (s390x)
- Support for Hyperledger Fabric v1.4.6
- Hardware Security Module (HSM) support for node identities
- Support for adding and removing ordering nodes from an existing ordering service
- Ability to override default CA, peer, ordering node configuration
- Full Java smart contract development support


If you have an existing {{site.data.keyword.blockchainfull_notm}} Platform v2.1.0, v2.1.1, or v2.1.2 deployment and are interested in upgrading to {{site.data.keyword.blockchainfull_notm}} Platform v2.1.3, see the following topics:
- [Upgrading your console and components on the OpenShift Container Platform](/docs/blockchain-sw-213?topic=blockchain-sw-213-upgrade-ocp)
- [Upgrading your console and components on Kubernetes or {{site.data.keyword.cloud_notm}} Private 3.2.1](/docs/blockchain-sw-213?topic=blockchain-sw-213-upgrade-k8)
- [Upgrading the {{site.data.keyword.blockchainfull_notm}} images](/docs/blockchain-sw-213?topic=blockchain-sw-213-blockchain-images#blockchain-images-upgrade)


See the [Release notes](/docs/blockchain-sw-213?topic=blockchain-sw-213-release-notes-saas-20#03-24-2020) for more details on the new features that are included in this release.

We've streamlined the documentation. If you are an existing customer, you might notice that a new `Tutorials` section was added in the table of contents under `Learn`. We've aggregated all of the tutorials in a single location under the Tutorials heading to make them easier to find.



## December 17, 2019
{: #whats-new-12-17-2019}

{{site.data.keyword.blockchainfull}} Platform v2.1.2 can now be deployed on the OpenShift Container Platform 4.1 and 4.2. You can find a table of deployment options by going to [Supported platforms](/docs/blockchain-sw-213?topic=blockchain-sw-213-console-ocp-about#console-ocp-about-prerequisites). {{site.data.keyword.blockchainfull_notm}} Platform v2.1.2 also provides improvements to the {{site.data.keyword.blockchainfull_notm}} Platform console. See the [Release notes](/docs/blockchain-sw-213?topic=blockchain-sw-213-release-notes-saas-20#12-17-2019) for a full list of new features that are included with this release.

If you have an existing {{site.data.keyword.blockchainfull_notm}} Platform v2.1.0 or v2.1.1 deployment and are interested in upgrading to {{site.data.keyword.blockchainfull_notm}} Platform v2.1.2, see the following topics:
- [Upgrading your console and components on the OpenShift Container Platform](/docs/blockchain-sw-213?topic=blockchain-sw-213-upgrade-ocp)
- [Upgrading your console and components on Kubernetes or {{site.data.keyword.cloud_notm}} Private 3.2.1](/docs/blockchain-sw-213?topic=blockchain-sw-213-upgrade-k8)
- [Upgrading the {{site.data.keyword.blockchainfull_notm}} images](/docs/blockchain-sw-213?topic=blockchain-sw-213-blockchain-images#blockchain-images-upgrade)


## November 08, 2019
{: #whats-new-11-08-2019}


{{site.data.keyword.blockchainfull_notm}} Platform v2.1.1 now provides users the ability to deploy the blockchain components on any Kubernetes v1.11 - v1.16 container platform on x86_64 hardware. Your entitlement includes the peer, CA, ordering node, and smart contract container images as well as the award-winning flexible management console for deploying and managing your blockchain network. Use the console or IBM Blockchain Platform APIs to build a consortium of organizations to easily transact on the same network, regardless of each client's cloud preference. Clients can build, operate, and grow their blockchain networks with an offering that can be used from development to production.

If you are an experienced Hyperledger Fabric customer and prefer to deploy and manage the containers yourself, you can download and use the container images without the management console. For more information, see [Using the IBM Blockchain images](/docs/blockchain-sw-213?topic=blockchain-sw-213-blockchain-images).

If you are an existing {{site.data.keyword.blockchainfull_notm}} Platform 2.1.0 customer, there is no upgrade needed to the {{site.data.keyword.blockchainfull_notm}} Platform v2.1.1.

{: note}


## September 24, 2019
{: #whats-new-9-24-2019}

{{site.data.keyword.blockchainfull_notm}} Platform utilizes Hyperledger Fabric v1.4.3 and provides a new flexible management platform on Red Hat OpenShift Container Platform 3.11 an open source platform that allows developers to quickly develop, build, deploy, and manage Linux containerized services and applications in a cloud environment. {{site.data.keyword.blockchainfull_notm}} Platform v2.1.0 is now available to be installed on any x86_64 architecture where Red Hat OpenShift Container Platform 3.11 runs and includes an award winning console UI for creating and managing your blockchain network.
