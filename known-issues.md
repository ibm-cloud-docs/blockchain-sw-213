---

copyright:
  years: 2019, 2020
lastupdated: "2020-11-02"

keywords: catalina, chrome, external CA, TLS, orderer, error

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

# Known issues
{: #sw-known-issues}

This page describes known issues that you might encounter when you use {{site.data.keyword.blockchainfull_notm}} Platform v2.1.3.
{:shortdesc}

<div style="background-color: #6fdc8c; padding-left: 20px; padding-right: 20px; border-bottom: 4px solid #0f62fe; padding-top: 12px; padding-bottom: 4px; margin-bottom: 16px;">
  <p style="line-height: 20px;">
    <strong>Important: You are not looking at the latest product documentation.  Make sure you are reading the documentation that matches the version of the software that you are using. Switch to product version </strong>
    <a href="/docs/blockchain-sw?topic=blockchain-sw-sw-known-issues">2.1.2</a>,
    <a href="/docs/blockchain-sw-25?topic=blockchain-sw-25-sw-known-issues">2.5 </a>,
    <a href="/docs/blockchain-sw-251?topic=blockchain-sw-251-sw-known-issues">2.5.1 (latest)</a>
    </p>
</div>


## Certificate Authority patch install fails
{: #sw-known-issues-ca-upgrade}

After upgrading from {{site.data.keyword.blockchainfull_notm}} Platform v2.1.2 to v2.1.3, installing the patch on a CA node fails. To resolve this problem see the [Troubleshooting](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-v2-troubleshooting#ibp-v2-troubleshooting-ca-upgrade-fails) topic.


## Chrome browser on Mac OS Catalina
{: #sw-known-issues-catalina}

The console will not work in the Chrome browser on Mac OS Catalina when the {{site.data.keyword.blockchainfull_notm}} Platform v2.1.0 or v2.1.1 is deployed with the default configuration that uses self-signed certificates. There are three ways to resolve this problem:

1.  Use a different [supported browser](/docs/blockchain-sw-213?topic=blockchain-sw-213-deploy-ocp#deploy-ocp-browsers) with Catalina.
2. Use your own [TLS certificates when deploying on OpenShift Container Platform](/docs/blockchain-sw-213?topic=blockchain-sw-213-deploy-ocp#use-your-own-tls-certificates-optional-) or [TLS certificates when deploying on Kubernetes or {{site.data.keyword.cloud_notm}} Private](/docs/blockchain-sw-213?topic=blockchain-sw-213-deploy-k8#use-your-own-tls-certificates-optional-).
3. Run the following commands to generate a new key and certificate pair for the console that will fix the problem.
   1. Run the following command to get the pod that corresponds to the console:
      ```
      kubectl get po
      ```
      {: codeblock}
   2. Exec into the pod by running the command:
      ```
      kubectl get po <pod-name> -c optools bash
      ```
      {: codeblock}
   3. Delete the console key and certificate by running the command:
      ```
      rm -f /certs/tls.key rm -f /certs/tls.crt
      ```
      {: codeblock}
   4. Delete the console pod which causes it to restart by running the command:
      ```
      kubectl delete po <pod-name>
      ```
      {: codeblock}
    When the pod restart completes, you should now be able to log in to your console URL from a Chrome Browser.
