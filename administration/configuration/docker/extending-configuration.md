---
title: "Extending Docker Configuration"
source_url: https://docs.rundeck.com/docs/administration/configuration/docker/extending-configuration.html
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Extending Docker Configuration

[Remco](https://github.com/HeavyHorst/remco) is used to generate the Rundeck configuration files from templates. It supports different key/value sources such as vault, etcd, and dynamodb. All configuration backends are combined into a unified keyspace. This allows storing parts of the configuration space in different backends. The default configuration uses environment variables.

Extending the configuration involves building a derived image with additional template files.

## Configuration Layout

<div class="language-text line-numbers-mode">

``` text
.
âââ Dockerfile
âââ remco
   âââ config.toml
   âââ resources.d
   â   âââ artifact-repositories-private.yaml.toml
   â   âââ framework.properties.toml
   â   âââ grails-config.properties.toml
   âââ templates
       âââ artifact-repositories-private.yaml
       âââ framework.properties
       âââ grails-config.properties
       âââ jaas-loginmodule.conf
       âââ log4j2.properties
```

</div>

The above is an abridged layout of the remco configuration files in the Rundeck image source directory. The three primary components for the configuration system are:

- `config.toml` Where the config backends and resource includes are configured
- `remco/resources.d` Directory that includes the resources files declaring the templates
- `remco/templates` Directory where the templates are stored

### Template Resources

<div class="language-text line-numbers-mode">

``` text
[[template]]
    src         = "${REMCO_TEMPLATE_DIR}/framework.properties"
    dst         = "${RUNDECK_HOME}/etc/framework.properties"
    mode        = "0644"
```

</div>

The template resource files declare:

- `src` The source template file
- `dst` Where the template will be rendered on disk
- `mode` The file mode for the created file

### Config Merging

<div class="language-text line-numbers-mode">

``` text
[[template]]
    src         = "${REMCO_TEMPLATE_DIR}/rundeck-config-features.properties"
    dst         = "${REMCO_TMP_DIR}/rundeck-config/rundeck-config-features.properties"
    mode        = "0644"
```

</div>

In the above example the destination is the special temporary directory `${REMCO_TMP_DIR}/rundeck-config/`. All files in this directory will be merged into `rundeck-config.properties` before Rundeck starts.

### Special Destination Directories

All template files rendered into special destination directories are merged into common Rundeck configuration files before Rundeck starts. The special template destination directories are:

- `${REMCO_TMP_DIR}/rundeck-config/` -\> `rundeck-config.properties`
- `${REMCO_TMP_DIR}/framework/` -\> `framework.properties`

## Extending Configuration

Extending the configuration by building a new Docker image derived from the Rundeck image is a snap. The following example is taken from the [Docker Zoo Config Exhibit](https://github.com/rundeck/docker-zoo/tree/master/config).

Starting with the following layout:

<div class="language-text line-numbers-mode">

``` text
.
âââ docker-compose.yml
âââ Dockerfile
âââ README.md
âââ remco
    âââ resources.d
    â   âââ plugin-http-tours-framework.properties.toml
    âââ templates
        âââ plugin-http-tours-framework.properties
```

</div>

The `plugin-http-tours-framework.properties.toml` file contents are:

<div class="language-text line-numbers-mode">

``` text
[[template]]
    src         = "${REMCO_TEMPLATE_DIR}/plugin-http-tours-framework.properties"
    dst         = "${REMCO_TMP_DIR}/framework/plugin-http-tours-framework.properties"
    mode        = "0644"
```

</div>

This file declares the input template source and an output destination to the special directory `${REMCO_TMP_DIR}/framework/`. This contents of the rendered template will be merged into `framework.properties` at startup.

The template contents are as follows:

<div class="language-text line-numbers-mode">

``` text
{% if exists("/rundeck/tour/endpoint") %}

framework.plugin.TourLoader.httptours.tourEndpoint={{ getv("/rundeck/tour/endpoint") }}
framework.plugin.TourLoader.httptours.tourManifestName={{ getv("/rundeck/tour/manifest","tour-manifest.json") }}
framework.plugin.TourLoader.httptours.toursSubpath={{ getv("/rundeck/tour/subpath","tours") }}

{% endif %}
```

</div>

This template adds configuration for a new plugin.

The following line from the Dockerfile includes the new remco configurations in the derived Docker image:

<div class="language-text line-numbers-mode">

``` text
COPY --chown=rundeck:root remco /etc/remco
```

</div>
