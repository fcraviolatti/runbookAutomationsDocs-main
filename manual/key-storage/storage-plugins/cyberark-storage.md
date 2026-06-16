---
title: "CyberArk Key Storage Plugin (Commercial)"
source_url: https://docs.rundeck.com/docs/manual/key-storage/storage-plugins/cyberark-storage.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# CyberArk Key Storage Plugin (Commercial)

CyberArk is a leader in Privileged Access Management solutions providing cloud ready, easy to use security solutions across the complete privileged access surface. A centralized password management system provides visibility and control to protect privileges from attack. CyberArk's solution is built for the Enterprise to enforce strong password business policies and prevent data breaches.

## Prerequisites

In order to securely communicate with CyberArk, Runbook Automation requires keystores for SSL and Client authentication. Instructions store the RootCA certificate, the client certificate and the client private key in key stores and specify them in `rundeck-config.properties`. For more information on creating/using a keystore, see [Java Keystore](https://www.ibm.com/docs/en/cognos-tm1/10.2.2?topic=ictocyoiatwas-add-certificates-jre-keystore).

**Below is an example of how to import a certificate using the command-line:**

<div class="language-bash line-numbers-mode">

``` bash
keytool -import -file "C:\Path\to\certificateFile.crt" -keystore "C:\Path\to\Keystore\Keystorename" -storepass "password"
```

</div>

**Below is an example of how to import another key store, likely containing the private key:**

<div class="language-bash line-numbers-mode">

``` bash
keytool -importkeystore -deststorepass [password] -destkeystore [new-keystore.jks] -srckeystore [keystore-filename.p12] -srcstoretype PKCS12```
```

</div>

> **Keystore Paths**
>
> If a full path is not specified for the new keystore, it will create the keystore in the directory the command was run from. Take note of all the keystore names and passwords as they are created, they will be needed to configure Runbook Automation. Once the certificates and private key are in keystore(s), add them to Runbook Automation using `rundeck-config.properties` or in Key Storage Config, as shown below.

> **Note for Cloud Users**
>
> In order to integrate Runbook Automation (Cloud) with CyberArk, the Enterprise Runner must be used. This is because we do not allow customers to upload their CA Certs and Keystores to our Cloud infrastructure. Please follow the instructions in the [Integration Through Enterprise Runner](#integration-through-enterprise-runner) section.

## Configuration

Key Storage Config (GUI)

rundeck-config.properties

Key Storage Config (GUI)

Use the following steps to configure the CyberArk plugin for key storage:

1.  Navigate to the System Menu (gear icon in the upper right).
2.  Click on **Key Storage**: ![Key Storage Menu](https://docs.rundeck.com/docs/assets/img/key-storage-menu.png)
3.  Navigate to the **Configure** tab.
4.  Click on **Add Storage Plugin +**.
5.  Click on **CyberArk Storage**

- **Key Storage Path**: The path in the Runbook Automation storage tree to apply the plugin. If `keys` is specified, then all keys and directories added to Key Storage will also be added to CyberArk.

- **Remove Path Prefix**: By default, the storage plugin will be invoked using the full path that is requested. If set to true, the path used when invoking the storage plugin would not include the prefix. It is **recommended to set this to true**. If set to false, keys will not be displayed unless an existing directory is specified in Runbook Automation.

- **Mode**: The mode for interacting with CyberArk. See above for descriptions of the various modes.

  - The `REST` mode authenticates with the REST API through the AIM Web Service to list the safes and list the names of the secrets within the safes. The retrieval and usage of individual secrets is accomplished through communication with the Credential Provider, not through the AIM WebService.

    > **Note "legacy" mode**
    >
    > Prior versions of Runbook Automation used `legacy` mode to use the REST API. To support prior versions, `legacy` can still be used in the **Mode** field, and it will behave the same as `REST`.

  - The `CCP` mode will get secrets using the [Central Credential Provider](https://docs.cyberark.com/AAM-CP/13.0/en/Content/CCP/The-Central%20-Credential-Provider.htm) (CCP) web service configuration. To setup Cyberark for this method follow [this documentation](https://docs.cyberark.com/AAM-CP/13.0/en/Content/CCP/Configure_CCPWindows.htm). This mode has a limitation that it is unable to list the keys in safes. When writing Process Automation jobs the job author will need to manually enter the path to the key using the following format: `[provider_path]/[safe]/path/to/secret.pem`

    - `provider_path` is specified in the config. Commonly it is set as `keys` but could be different.
    - `safe` is the Cyberark Safe where the key is stored.
    - `path/to` is the folder path within the safe where the key is stored.
    - `secret.pem` is the unique name of the key in that particular folder.

- **Base URL**: The base URL for the CyberArk account where the secrets should be saved. Use the format: `https://[urltoyourserver]:[port]`.

- **Credential Provider URL**: (Optional) The URL for the Central Credential Provider Web Service. Defaults to the Base URL.

- **Name of CCP WebService**: If using `ccp` mode this can be used to specify the name of the CCP Web Service. Default (if setting is not specified) is `AIMWebService`.

- **CCP AppID**: WebService AppID of the Central Credential Provider used to retrieve accounts and passwords.

- **Credential Safe**: CyberArk Credential Provider Safe for REST API mode.

- **Credential Path**: CyberArk Credential Provider Safe for REST API mode.

- **Credential AppID**: CyberArk Credential Provider AppId for REST API mode.

- **Username**: If using basic authentication, this is the username for an account with access to the secrets that will be used in Runbook Automation.

- **Password**: The password for a user in the account where the secrets are stored.

  > **Less secure authentication**
  >
  > It is **not recommended** to use `basic` authentication with `Username` and `Password`. It is recommended to use the Credential Safe, Path and AppID to retrieve REST credentials from the CCP. :::

- **Client KeyStore**: The path to the key store that contains the client certificate. (Must be of type `JKS`)

- **Client KeyStore Password**: The password for the key store that contains the client certificate.

- **Root CA KeyStore**: The path to the key store containing the RootCA certificate. (Must be of type `JKS`)

- **Root CA KeyStore Password**: The password for the key store containing the RootCA certificate.

- **Private KeyStore**: The path to the key store containing the user's private key. (Must be of type `JKS`)

- **Private KeyStore Password**: The password for the key store containing the user's private key.

- **PrivateKey Password**: Password to access the private key.

- **Root CA Name**: The name that the Root CA Certificate is saved under in the key store.

- **Client Certificate Name**: The name that the Client Certificate is saved under in the key store.

- **Private Key Name**: Alias for the private key in the keystore.

- **Platform ID**: (Optional) Platform ID to use when creating a new secret from Runbook Automation's key storage.

- **Create Username**: (Optional) Default username applied when creating a new password entry in CyberArk. This is only applicable when using Runbook Automation to create new entries in CyberArk.

Below is an example configuration:

![CyberArk Full Config](https://docs.rundeck.com/docs/assets/img/cyberark-config-full.png)  

rundeck-config.properties

For self-hosted Runbook Automation, the configuration for CyberArk can also be set in `rundeck-config.properties`:

<div class="language-text line-numbers-mode">

``` text
rundeck.storage.provider.1.type=cyberark-storage
rundeck.storage.provider.1.path=keys
rundeck.storage.provider.1.removePathPrefix=true
rundeck.storage.provider.1.config.baseURL=https://your.cyberarkserver.com
rundeck.storage.provider.1.config.username=[username]
rundeck.storage.provider.1.config.password=[password]
rundeck.storage.provider.1.config.appId=testappid
rundeck.storage.provider.1.config.platformId=WinServerLocal
rundeck.storage.provider.1.config.createUsername=[createUsername]
rundeck.storage.provider.1.config.clientKeyStore=/path/to/file/cyberArkKeyStore
rundeck.storage.provider.1.config.clientKeyStorePassword=[password]
rundeck.storage.provider.1.config.rootCAKeyStore=/path/to/file/cyberArkKeyStore
rundeck.storage.provider.1.config.rootCAKeyStorePassword=[password]
rundeck.storage.provider.1.config.privateKeyStore=/path/to/file/privateKeyStore
rundeck.storage.provider.1.config.privateKeyStorePassword=[password]
rundeck.storage.provider.1.config.privateKeyPassword=[password]
rundeck.storage.provider.1.config.privateKeyName=client_1-28
rundeck.storage.provider.1.config.rootCAName=rootca
rundeck.storage.provider.1.config.clientCertName=clientcert
```

</div>

- **type**: This specifies the storage plugin to use. For Cyberark, the value should always be `cyberark-storage`.
- **path**: The path in the Runbook Automation storage tree to apply the plugin. If `keys` is specified, then all keys and directories added to Key Storage will also be added to CyberArk.
- **removePathPrefix**: By default, the storage plugin will be invoked using the full path that is requested. If set to true, the path used when invoking the storage plugin would not include the prefix. It is **recommended to set this to true**. If set to false, keys will not be displayed unless an existing directory is specified in Runbook Automation.
- **username**: Username for an account with access to the secrets that will be used in Runbook Automation.
- **password**: The password for a user in the account where the secrets are stored.
- **baseURL**: The base URL for the CyberArk account where the secrets should be saved. Use the format: `https://[urltoyourserver]:[port]`.
- **appId**: The app ID for the application with the safes to use secrets from.
- **platformId**: Platform ID to use when creating a new secret from Runbook Automation's key storage. I.e. WinServerLocal
- **createUsername**: Default user name applied when creating a new password entry in CyberArk.
- **clientKeystore**: The path to the key store that contains the client certificate. (Must be of type `JKS`)
- **clientKeystorePassword**: The password for the key store that contains the client certificate.
- **rootCAKeystore**: The path to the key store containing the RootCA certificate. (Must be of type `JKS`)
- **rootCAKeystorePassword**: The password for the key store containing the RootCA certificate.
- **privateKeyStore**: The path to the key store containing the user's private key. (Must be of type `JKS`)
- **privateKeystorePassword**: The password for the key store containing the user's private key.
- **privateKeyPassword**: Password to access the private key.
- **rootCAName**: The name that the Root CA Certificate is saved under in the key store.
- **clientCertName**: The name that the Client Certificate is saved under in the key store.
- **privateKeyName**: Alias for the private key in the keystore.
- **credentialUrl**: CyberArk Credential Provider URL for REST API mode.
- **credentialAppId**: CyberArk Credential Provider AppId for REST API mode.
- **credentialSafe**: CyberArk Credential Provider Safe for REST API mode.
- **credentialPath**: CyberArk Credential Provider Safe for REST API mode.

For `ccp` mode add the following. (There may be settings above that are not required in this mode.)

<div class="language-text line-numbers-mode">

``` text
rundeck.storage.provider.1.config.mode=ccp
rundeck.storage.provider.1.config.nameOfCCPWebService=NameOfWebService
```

</div>

## Integration Through Enterprise Runner

The [Enterprise Runner](https://docs.rundeck.com/docs/administration/runner/) can be used to integrate with CyberArk. This is useful when CyberArk is hosted in an environment that is not directly accessible from Runbook Automation - whether self-hosted or Cloud.

The following provides examples of how to configure the Enterprise Runner to connect to CyberArk:

YAML Config File

Environment Variables

Docker Compose

YAML Config File

Custom properties for the Runner can be set through a `.yaml` file:

<div class="language-text line-numbers-mode">

``` text
runner:
  rundeck:
      storage:
        cyberark:
          type: "cyberark-storage"
          pathBehavior: "predefined"
          configuration:
            baseURL: "https://services-uswest.skytap.com:14417"
            username: "Administrator"
            password: "myPassword"
            appId: "testappid"
            clientKeyStore: /etc/rundeck/cyberark/clientkeystore
            clientKeyStorePassword: "myClientPass"
            rootCAKeyStore: /etc/rundeck/cyberark/rootkeystore
            rootCAKeyStorePassword: "myRootPass"
            privateKeyStore: /etc/rundeck/cyberark/privatekeystore.jks
            privateKeyStorePassword: "myPrivatePass"
            privateKeyPassword: "myPrivateKeyPass"
            privateKeyName: "client_1-28"
            rootCAName: "rootcert"
            clientCertName: "clientcert"
```

</div>

Save this file in the directory where the Runner `.jar` is located and then invoke the Runner with the following command:

<div class="language-text line-numbers-mode">

``` text
java -Dmicronaut.config.files=runner-props.yaml -jar runner-{{unique-runner-id}}.jar
```

</div>

> **CCP Mode**
>
> CCP Mode requires the explicit configuration of the availability check path that is used to determine if the CyberArk service is available.
>
> <div class="language-text line-numbers-mode">
>
> ``` text
>     runner:
>       rundeck:
>           storage:
>             cyberark:
>               availabilityCheckPath: WinServerLocal-account-Administrator
>               <...>
>               configuration:
>                 mode: ccp
>                 <...>
> ```
>
> </div>

Environment Variables

These custom properties can be set as environment variables on the system where the Runner will be invoked:

<div class="language-text line-numbers-mode">

``` text
export RUNNER_RUNDECK_STORAGE_CYBERARK_TYPE="cyberark-storage"
export RUNNER_RUNDECK_STORAGE_CYBERARK_PATH_BEHAVIOR="predefined"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_BASE_URL="https://services-uswest.skytap.com:14417"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_USERNAME="Administrator"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_PASSWORD="myPassword"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_APP_ID="testappid"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_CLIENT_KEY_STORE="/etc/rundeck/cyberark/clientkeystore"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_CLIENT_KEY_STORE_PASSWORD="myClientPass"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_ROOT_CA_KEY_STORE="/etc/rundeck/cyberark/rootkeystore"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_ROOT_CA_KEY_STORE_PASSWORD="myrootpass"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_PRIVATE_KEY_STORE="/etc/rundeck/cyberark/privatekeystore.jks"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_PRIVATE_KEY_STORE_PASSWORD="myPrivatePass"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_PRIVATE_KEY_PASSWORD="MyPrivateKeyPass"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_PRIVATE_KEY_NAME="client_1-28"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_ROOT_CA_NAME="rootcert"
export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_CLIENT_CERT_NAME="clientcert"
```

</div>

When using environment variables, the Runner can be invoked with just:

<div class="language-text line-numbers-mode">

``` text
java -jar runner-{{unique-runner-id}}.jar
```

</div>

> **CCP Mode**
>
> CCP Mode requires the explicit configuration of the availability check path that is used to determine if the CyberArk service is available.
>
> <div class="language-text line-numbers-mode">
>
> ``` text
> export RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_MODE="ccp"
> export RUNNER_RUNDECK_STORAGE_CYBERARK_AVAILABILITY_CHECK_PATH="WinServerLocal-account-Administrator"
> ```
>
> </div>

Docker Compose

Here is an example `docker-compose` for the Runner with the configuration properties:

<div class="language-text line-numbers-mode">

``` text
version: '3'
services:
    runner:
      image: ${RUNNER_IMAGE}
      environment:
         RUNNER_RUNDECK_STORAGE_CYBERARK_TYPE="cyberark-storage"
         RUNNER_RUNDECK_STORAGE_CYBERARK_PATH_BEHAVIOR="predefined"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_BASE_URL="https://services-uswest.skytap.com:14417"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_USERNAME="Administrator"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_PASSWORD="myPassword"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_APP_ID="testappid"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_CLIENT_KEY_STORE="/etc/rundeck/cyberark/clientkeystore"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_CLIENT_KEY_STORE_PASSWORD="myClientPass"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_ROOT_CA_KEY_STORE="/etc/rundeck/cyberark/rootkeystore"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_ROOT_CA_KEY_STORE_PASSWORD="myrootpass"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_PRIVATE_KEY_STORE="/etc/rundeck/cyberark/privatekeystore.jks"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_PRIVATE_KEY_STORE_PASSWORD="myPrivatePass"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_PRIVATE_KEY_PASSWORD="MyPrivateKeyPass"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_PRIVATE_KEY_NAME="client_1-28"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_ROOT_CA_NAME="rootcert"
         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_CLIENT_CERT_NAME="clientcert"
```

</div>

> **CCP Mode**
>
> CCP Mode requires the explicit configuration of the availability check path that is used to determine if the CyberArk service is available.
>
> <div class="language-text line-numbers-mode">
>
> ``` text
>       environment:
>         RUNNER_RUNDECK_STORAGE_CYBERARK_CONFIGURATION_MODE="ccp"
>         RUNNER_RUNDECK_STORAGE_CYBERARK_AVAILABILITY_CHECK_PATH="WinServerLocal-account-Administrator"
> ```
>
> </div>
