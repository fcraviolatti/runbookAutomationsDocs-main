---
title: "Document Format Reference"
source_url: https://docs.rundeck.com/docs/manual/document-format-reference/
product: Runbook Automation Self-Hosted
version: 5.20.1
fetched: 2026-06-12
---

# Document Format Reference

## Overview

Rundeck uses structured document formats for defining Jobs, Resources (Nodes), and Access Control policies. These formats allow you to:

- **Define Jobs as Code**: Create and manage Job definitions in version control
- **Import/Export Jobs**: Share Jobs between projects or Rundeck instances
- **Manage Resources**: Define node inventories programmatically
- **Configure Access Control**: Define security policies in a structured, reviewable format
- **Automate via API**: Programmatically create and update Rundeck configurations

This section provides detailed specifications for each document format, including schema definitions, examples, and version information.

## When to Use These Formats

**Job Definitions:**

- Exporting Jobs from the GUI for backup or version control
- Creating Jobs using the [rd CLI tool](https://rundeck.github.io/rundeck-cli/) or API
- Bulk importing Jobs into projects
- Defining Jobs in CI/CD pipelines

**Resource Model Sources:**

- Defining custom node inventories
- Creating static node definitions
- Building resource model source plugins

**ACL Policies:**

- Defining role-based access controls
- Managing security policies as code
- Controlling access to Projects, Jobs, Nodes, and System functions

## Available Format References

### Job Definitions

Jobs can be defined in XML, YAML, or JSON formats. All three formats support the same features and can be converted between each other.

- **[JOB-XML](https://docs.rundeck.com/docs/manual/document-format-reference/job-v20.html)** - XML format for Job definitions (v2.0)
- **[JOB-YAML](https://docs.rundeck.com/docs/manual/document-format-reference/job-yaml-v12.html)** - YAML format for Job definitions (v1.2)
- **[JOB-JSON](https://docs.rundeck.com/docs/manual/document-format-reference/job-json-v44.html)** - JSON format for Job definitions (v4.4)

**Choose YAML when:**

- Working with configuration as code
- Prioritizing human readability
- Using version control systems
- Most common choice for Job definitions

**Choose XML when:**

- Integrating with XML-based tools
- Working with legacy Job definitions
- Original Rundeck format

**Choose JSON when:**

- Working with REST APIs
- Programmatic Job generation
- Integration with JSON-based tooling

### Resource Model (Node Definitions)

Resources (Nodes) can be defined in JSON, XML, or YAML formats for use with Resource Model Source plugins.

- **[RESOURCE-JSON](https://docs.rundeck.com/docs/manual/document-format-reference/resource-json-v10.html)** - JSON format for node definitions (v1.0)
- **[RESOURCE-XML](https://docs.rundeck.com/docs/manual/document-format-reference/resource-v13.html)** - XML format for node definitions (v1.3)
- **[RESOURCE-YAML](https://docs.rundeck.com/docs/manual/document-format-reference/resource-yaml-v13.html)** - YAML format for node definitions (v1.3)

These formats are used when:

- Creating custom Resource Model Source plugins
- Defining static node inventories
- Importing node data from external systems

### Access Control Policies

- **[ACLPOLICY](https://docs.rundeck.com/docs/manual/document-format-reference/aclpolicy-v10.html)** - YAML format for ACL policy definitions (v1.0)

ACL policies define authorization rules for:

- Project access
- Job execution and modification
- Node access
- System-level operations

## Related Documentation

- [Jobs](https://docs.rundeck.com/docs/manual/jobs/creating-jobs.html) - Creating and managing Jobs
- [Resource Model Sources](https://docs.rundeck.com/manual/projects/resource-model-sources/) - Node inventory configuration
- [Access Control](https://docs.rundeck.com/docs/administration/security/authorization.html) - Authorization and ACL policies
- [API Documentation](https://docs.rundeck.com/api/) - Using document formats with the Rundeck API
- [rd CLI Tool](https://rundeck.github.io/rundeck-cli/) - Command-line interface for Rundeck
