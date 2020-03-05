---

copyright:
  years: 2019, 2020
lastupdated: "2020-03-05"

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

<div style="background-color: #f4f4f4; padding-left: 20px; border-bottom: 2px solid #0f62fe; padding-top: 12px; padding-bottom: 4px; margin-bottom: 16px; font-family: 'IBM Plex Sans', 'Helvetica Neue', Arial, sans-serif;">
  <p style="line-height: 10px;">
    <strong>Running a different version of IBM Blockchain Platform?</strong> Switch to version
    <a href="https://cloud.ibm.com/docs/blockchain-sw?topic=blockchain-sw-sw-known-issues.">2.1.2</a>
    </p>
</div>


## Chrome browser on Mac OS Catalina
{: #sw-known-issues-catalina}

The console will not work in the Chrome browser on Mac OS Catalina when the {{site.data.keyword.blockchainfull_notm}} Platform v2.1.0 or v2.1.1 is deployed with the default configuration that uses self-signed certificates. There are three ways to resolve this problem:

1.  Use a different [supported browser](/docs/blockchain-sw-213?topic=blockchain-sw-213-deploy-ocp#deploy-ocp-browsers) with Catalina.
2. Use your own [TLS certificates when deploying on OpenShift Container Platform](/docs/blockchain-sw-213?topic=blockchain-sw-213-deploy-ocp#use-your-own-tls-certificates-optional-) or [TLS certificates when deploying on Kubernetes or {{site.data.keyword.cloud_notm}} Private](/docs/blockchain-sw-213?topic=blockchain-sw-213-deploy-k8#use-your-own-tls-certificates-optional-).
3. Run the following commands to generate a new key and certificate pair for the console that will fix the problem.
   1. Run the following command to get the pod that corresponds to the ibp console:
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
    When the pod restart completes, you should now be able to login to your console URL from a Chrome Browser.

## Exporting an ordering node shows error for missing TLS certs
{: #sw-known-issues-orderer-tls-cert-error}

When attempting to export an ordering node, you might see the following error: `Some ordering service TLS certificates could not be retrieved at this time and will not be included in the exported information.`

You can safely ignore this error, as the certificates the console is trying to pull are only needed for a feature that is not currently enabled.

## Unable to create peer or ordering node using external CA certificates
{: #sw-known-issues-external-CA-cant-create}

Currently, it is not possible to create a peer or ordering nodes using certificates entered into the console as described in [Component governance](/docs/blockchain-sw-213?topic=blockchain-sw-213-ibp-console-govern-components#ibp-console-govern-third-party-ca).

It is still possible to create components using the normal register and enroll flows in the console.
