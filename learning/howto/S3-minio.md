---
title: "Configure S3 or Minio for Storing Execution Logs"
source_url: https://docs.rundeck.com/docs/learning/howto/S3-minio.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Configure S3 or Minio for Storing Execution Logs

Rundeck execution logs are a set of files generated after each job execution. By default, Rundeck stores them on the local filesystem. Another way to store these logs is on a dedicated file storage service like [AWS S3](https://aws.amazon.com/s3/).  
  
By delegating this storage to AWS S3 itâ€™s possible to leverage [features](https://aws.amazon.com/s3/features/) like S3 replication, security management, data persistence, and saving space on the local filesystem.  
  

> **Warning**
>
> Other S3-compatible bucket system like [Minio](https://min.io/) may work with the S3 plugin, but compatibility is not guaranteed. Minio in this example is used for example purposes and does not imply support.

In PagerDuty Runbook Automation (formerly â€œRundeck Enterpriseâ€?) [cluster](https://docs.rundeck.com/administration/cluster/#cluster-overview), S3-compatible storage should be the default configuration to ensure access to logs from any cluster member.  
  
This article explains how to configure Rundeck so that these execution logs are stored on services such as Amazon S3 or Minio.

## Steps to configure S3 execution logs on Rundeck OSS / Runbook Automation for Global Config

1.  Stop the Rundeck service  

    <div class="language-text line-numbers-mode">

    ``` text
    systemctl stop rundeckd
    ```

    </div>

2.  S3 Log Storage Plugin  

    Rundeck Community

    PagerDuty Runbook Automation

    Rundeck Community

    Add the S3 log storage [plugin](https://github.com/rundeck-plugins/rundeck-s3-log-plugin) on the `libext` directory (at `$RDECK_BASE/libext` directory).  

    <div class="language-text line-numbers-mode">

    ``` text
    wget https://github.com/rundeck-plugins/rundeck-s3-log-plugin/releases/download/v1.0.12/rundeck-s3-log-plugin-1.0.12.jar -P $RDECK_BASE/libext
    ```

    </div>

    PagerDuty Runbook Automation

    Runbook Automation includes its own plugin for this out of the box  

3.  To enable the S3 / Minio log storage plugin, add the following line on the `rundeck-config.properties` file  

    Rundeck Community

    PagerDuty Runbook Automation

    Rundeck Community

    <div class="language-text line-numbers-mode">

    ``` text
    rundeck.execution.logs.fileStoragePlugin=org.rundeck.amazon-s3
    ```

    </div>

    PagerDuty Runbook Automation

    <div class="language-text line-numbers-mode">

    ``` text
    rundeck.execution.logs.fileStoragePlugin=com.rundeck.rundeckpro.amazon-s3
    ```

    </div>

4.  Then open the `framework.properties` file and add the S3 / Minio bucket info as follow:

Rundeck Community

PagerDuty Runbook Automation

Rundeck Community

<div class="language-text line-numbers-mode">

``` text
framework.plugin.ExecutionFileStorage.org.rundeck.amazon-s3.endpoint=http://192.168.1.14:9000
framework.plugin.ExecutionFileStorage.org.rundeck.amazon-s3.AWSAccessKeyId=your_s3_or_minio_access_key
framework.plugin.ExecutionFileStorage.org.rundeck.amazon-s3.AWSSecretKey=your_s3_or_minio_access_key
framework.plugin.ExecutionFileStorage.org.rundeck.amazon-s3.bucket=test-rundeck-logs
framework.plugin.ExecutionFileStorage.org.rundeck.amazon-s3.path=logs/${job.project}/${job.execid}.log
framework.plugin.ExecutionFileStorage.com.rundeck.amazon-s3.region=your_instance_region
```

</div>

PagerDuty Runbook Automation

<div class="language-text line-numbers-mode">

``` text
framework.plugin.ExecutionFileStorage.com.rundeck.rundeckpro.amazon-s3.endpoint=http://192.168.1.14:9000
framework.plugin.ExecutionFileStorage.com.rundeck.rundeckpro.amazon-s3.AWSAccessKeyId=your_s3_or_minio_access_key
framework.plugin.ExecutionFileStorage.com.rundeck.rundeckpro.amazon-s3.AWSSecretKey=your_s3_or_minio_access_key
framework.plugin.ExecutionFileStorage.com.rundeck.rundeckpro.amazon-s3.bucket=test-rundeck-logs
framework.plugin.ExecutionFileStorage.com.rundeck.rundeckpro.amazon-s3.path=logs/${job.project}/${job.execid}.log
framework.plugin.ExecutionFileStorage.com.rundeck.rundeckpro.amazon-s3.region=your_instance_region
```

</div>

**Definitions:**

- `endpoint`: A custom S3 compatible endpoint to use, such as `https://my-host.com/s3`
- `pathStyle`: Optional, boolean, `default=False`, set to `True` if you need to define the bucket in your S3 like endpoint URL. e.g: `https://<s3_like_end_point_url\>/<your_bucket_name\>`
- `AWSAccessKeyId`: AWS access key, required if using `AWSSecretKey`.
- `AWSSecretKey`: AWS secret key, required if using `AWSAccessKeyId`.
- `AWSCredentialsFile`: Properties file which contains `accessKey` and `secretKey` entries. The alternative to specifying the `AWSAccessKeyId` and `AWSSecretKey`
- `bucket`: The name of the S3 bucket to use. This is the shorthand name, eg `test-rundeck-logs`
- `region`: The Region your Instance is located, eg `us-east-1`

## Test basic setup

1.  Start the Rundeck service.  
2.  Create a new project.  
3.  Create a new job and then execute it, now the execution log is stored in the S3/Minio bucket.  
    ![ ](https://docs.rundeck.com/docs/assets/img/minio1.png)  
4.  From Rundeck click on the Gear Icon and then to the Log Storage option, now you can see the Log Storage Activity.  
    ![ ](https://docs.rundeck.com/docs/assets/img/minio2.png)  

## PagerDuty Runbook Automation (formerly â€œRundeck Enterpriseâ€?) System Configuration

1.  As admin rights users click on the Gear Icon and then click on â€œSystem Configurationâ€?.  
    ![ ](https://docs.rundeck.com/docs/assets/img/minio3.png)  
2.  Then click on the â€œ+ Add Configâ€? button.  
    ![ ](https://docs.rundeck.com/docs/assets/img/minio4.png)  
3.  Add the following property `rundeck.execution.logs.fileStoragePlugin` with the following value `com.rundeck.rundeckpro.amazon-s3`.  
    ![ ](https://docs.rundeck.com/docs/assets/img/minio5.png)  
4.  Add the following custom properties:  
    ![ ](https://docs.rundeck.com/docs/assets/img/minio6.png)  
5.  Restart the PagerDuty Runbook Automation service.  

## Steps to configure S3 execution logs on Rundeck OSS / Runbook Automation for individual projects

1.  As admin rights users click on `Project Settings` then `Edit Configuration` and then Edit `Configuration File`  
    ![ ](https://docs.rundeck.com/docs/assets/img/minio3.png)  
2.  Then add these lines with your information:

<div class="language-text line-numbers-mode">

``` text
project.plugin.ExecutionFileStorage.com.rundeck.rundeckpro.amazon-s3.AWSAccessKeyId=your_aws_access_key
project.plugin.ExecutionFileStorage.com.rundeck.rundeckpro.amazon-s3.AWSSecretKey=your_aws_secret_key
project.plugin.ExecutionFileStorage.com.rundeck.rundeckpro.amazon-s3.bucket=your_s3_bucket_name
project.plugin.ExecutionFileStorage.com.rundeck.rundeckpro.amazon-s3.path=logs/${job.project}/${job.execid}.log
project.plugin.ExecutionFileStorage.com.rundeck.rundeckpro.amazon-s3.region=your_instance_region
```

</div>

1.  Then click Save button.
2.  Restart the PagerDuty Runbook Automation service.  

## Docker Config

Rundeck Community

PagerDuty Runbook Automation

Rundeck Community

The S3 Log Storage Plugin isnâ€™t bundled out of the box with Rundeck. To use it on a Docker image it is necessary to extend the image using Remco. [Remco](https://github.com/HeavyHorst/remco) is used to generate the Rundeck configuration files from templates. This allows storing parts of the configuration space in different backends. The default configuration uses environment variables.

The Remco documentation is available [here](https://docs.rundeck.com/docs/administration/configuration/docker/extending-configuration.html#extending-docker-configuration).

This is the example file structure of a custom Rundeck image with the S3 Log Storage Plugin.  

![ ](https://docs.rundeck.com/docs/assets/img/minio8.png)  

The` Dockerfile` file content (inside docker project base directory)  

<div class="language-text line-numbers-mode">

``` text
FROM rundeck/rundeck:4.5.0

# root user tasks
USER root

# install python
RUN apt-get -y update && \
   apt-get -y install python3-pip && \
   pip install --upgrade pip

# rundeck user tasks
USER rundeck

ADD --chown=rundeck:root https://github.com/rundeck-plugins/rundeck-s3-log-plugin/releases/download/v1.0.13/rundeck-s3-log-plugin-1.0.13.jar libext/
COPY --chown=rundeck:root remco /etc/remco
COPY --chown=rundeck:root plugins/* ./libext/
```

</div>

The` docker-compose.yml` file content (inside docker project base directory):

<div class="language-text line-numbers-mode">

``` text
version: '3'
services:
 rundeck:
   build:
     context: .
     args:
       IMAGE: rundeck/rundeck:4.5.0
   ports:
   - 4440:4440
   environment:
     RUNDECK_GRAILS_URL: 'http://localhost:4440'
     RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_NAME: org.rundeck.amazon-s3
     RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_ENDPOINT: http://minio:9000/
     RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_BUCKET: rundeck
     RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_REGION: us-east-1
     RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_PATHSTYLE: "true"
     RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_ACCESSKEY: minioadmin
     RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_SECRETKEY: minioadmin
 minio:
   image: minio/minio:latest
   ports:
     - 9000:9000
     - 9001:9001
   entrypoint: sh
   command: -c 'mkdir /rundeck && /opt/bin/minio server /rundeck --console-address ":9001"'
   environment:
       MINIO_ACCESS_KEY: minioadmin
       MINIO_SECRET_KEY: minioadmin
 createbuckets:
    image: minio/mc:latest
    depends_on:
      - minio
    entrypoint: >
      /bin/sh -c "
      /usr/bin/mc config host add myminio http://minio:9000 minioadmin minioadmin;
      /usr/bin/mc mb myminio/rundeck;
      /usr/bin/mc policy download myminio/rundeck;
      exit
      "
```

</div>

The` custom-framework.properties.toml` file content (inside `myrundeck/remco/resources.d/`directory):

<div class="language-text line-numbers-mode">

``` text
[[template]]
    src         = "${REMCO_TEMPLATE_DIR}/custom-framework.properties"
    dst         = "${REMCO_TMP_DIR}/framework/custom-framework.properties"
    mode        = "0644"
```

</div>

The` plugin-rundeck-config.properties.toml` file (inside `myrundeck/remco/resources.d/`directory):

<div class="language-text line-numbers-mode">

``` text
[[template]]
    src         = "${REMCO_TEMPLATE_DIR}/plugin-rundeck-config.properties"
    dst         = "${REMCO_TMP_DIR}/rundeck-config/plugin-rundeck-config.properties"
    mode        = "0644"
```

</div>

The` custom-framework.properties` file (inside `myrundeck/remco/templates/`directory)

<div class="language-text line-numbers-mode">

``` text
framework.plugin.ExecutionFileStorage.org.rundeck.amazon-s3.path=logs/${job.project}/${job.execid}.log
framework.plugin.ExecutionFileStorage.org.rundeck.amazon-s3.AWSAccessKeyId={{ getv("/rundeck/plugin/executionfilestorage/s3/accesskey") }}
framework.plugin.ExecutionFileStorage.org.rundeck.amazon-s3.AWSSecretKey={{ getv("/rundeck/plugin/executionfilestorage/s3/secretkey") }}
framework.plugin.ExecutionFileStorage.org.rundeck.amazon-s3.endpoint={{  getv("/rundeck/plugin/executionfilestorage/s3/endpoint") }}
framework.plugin.ExecutionFileStorage.org.rundeck.amazon-s3.pathStyle={{ getv("/rundeck/plugin/executionfilestorage/s3/pathstyle") }}
```

</div>

`Plugin-rundeck-config.properties `(inside `myrundeck/remco/templates/` directory):

<div class="language-text line-numbers-mode">

``` text
rundeck.execution.logs.fileStorage.storageRetryDelay=5
rundeck.execution.logs.fileStorage.retrievalRetryDelay=5
rundeck.execution.logs.fileStorage.checkpoint.time.minimum=5s
rundeck.execution.logs.fileStorage.checkpoint.time.interval=5s
rundeck.feature.pagedjoblist.enabled=true
```

</div>

1.  With all environment set, build the image doing: `docker-compose build`
2.  After that, run the project using the following command: `docker-compose up`
3.  Enter the Rundeck instance in the following URL: `http://localhost:4000`, user: `admin`, password: `admin`.
4.  Create a new Project.
5.  Go to the â€œCommandsâ€? Section and dispatch any command against the local node.
6.  Check the Minio web interface ([`http://localhost:9001`](http://localhost:9001)`, `user:` minioadmin, `password:` minioadmin`), now all Rundeck executions are stored on the â€œrundeckâ€? bucket.  

![ ](https://docs.rundeck.com/docs/assets/img/minio9.png)  

PagerDuty Runbook Automation

The following env vars are included on the Runbook Automation Docker image by default and are needed to enable S3/Minio log storage on the Docker container:

<div class="language-text line-numbers-mode">

``` text
RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_NAME
```

</div>

(With the following value: `com.rundeck.rundeckpro.amazon-s3`)

<div class="language-text line-numbers-mode">

``` text
RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_BUCKET
RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_REGION 
RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_PATH 
RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_AWSACCESSKEYID
RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_AWSSECRETKEY
```

</div>

Full Docker example:

1.  Run this `docker-compose.yml` example with `docker-compose up` command:  
    <div class="language-text line-numbers-mode">

    ``` text
    version: '3'
    services:
      rundeck:
          image: rundeckpro/enterprise:4.3.1
          environment:
            RUNDECK_GRAILS_URL: 'http://localhost:4440'
            RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_NAME: com.rundeck.rundeckpro.amazon-s3
            RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_BUCKET: rundeck
            RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_REGION: us-east-1
            RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_AWSACCESSKEYID: minioadmin
            RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_AWSSECRETKEY: minioadmin
            RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_ENDPOINT: http://minio:9000
            RUNDECK_PLUGIN_EXECUTIONFILESTORAGE_S3_PATHSTYLE: "true"
          ports:
            - 4440:4440
      minio:
        image: minio/minio:latest
        ports:
          - 9000:9000
          - 9001:9001
        entrypoint: sh
        command: -c 'mkdir /rundeck && /opt/bin/minio server /rundeck --console-address ":9001"'
        environment:
            MINIO_ACCESS_KEY: minioadmin
            MINIO_SECRET_KEY: minioadmin
      createbuckets:
         image: minio/mc:latest
         depends_on:
           - minio
         entrypoint: >
           /bin/sh -c "
           /usr/bin/mc config host add myminio http://minio:9000 minioadmin minioadmin;
           /usr/bin/mc mb myminio/rundeck;
           /usr/bin/mc policy download myminio/rundeck;
           exit
           "
    ```

    </div>
2.  Enter the Rundeck instance in another browser tab: `http://localhost:4440`, user: `admin`, password: `admin`.  
3.  Create a new Project.  
4.  Go to the â€œCommandsâ€? Section and dispatch any command against the local node.  
5.  Check the Minio web interface in another browser tab ([`http://localhost:9001`](http://localhost:9001)`, `user:` minioadmin, `password:` minioadmin`), now, all Rundeck executions are stored on the â€œrundeckâ€? bucket.  

![ ](https://docs.rundeck.com/docs/assets/img/minio10.png)  

## Resources

- [S3/Minio Log Storage configuration](https://docs.rundeck.com/docs/administration/cluster/logstore/s3.html#s3-log-storage-plugin) (Rundeck documentation).
- [S3 Log Storage Plugin GitHub space](https://github.com/rundeck-plugins/rundeck-s3-log-plugin).
- [Extending Rundeck Docker Image](https://docs.rundeck.com/docs/administration/configuration/docker/extending-configuration.html#extending-configuration) (Rundeck Documentation).
