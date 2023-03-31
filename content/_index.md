---
title: "Introduction"
weight: 1
---

# Introduction to ConfigSet and cfs

ConfigSet is a platform designed to simplify infrastructure automation by providing a centralized repository of pre-made `cfs` manifests for a variety of tasks. These manifests help users automate their infrastructure setup and management consistently and reliably. Users can interact with ConfigSet in several ways, including manually creating configset manifests and using the `cfs` client application to deploy them to their infrastructure. Users can also load manifests directly from the ConfigSet website or any other http/https location, or retrieve them from S3 buckets.

### ConfigSet supports the following options for interacting with manifests:
* Local Filesystem: A local file on the system or a file path starting with ./ or / is treated as a local file and loaded from the local disk.
* Remote URL: A URL starting with http:// or https:// is treated as a remote URL and loaded from the remote location.
* S3 Bucket: A URL starting with s3:// is treated as an S3 bucket and loaded from the remote location.

This flexibility allows you to use ConfigSet not only as an installation tool but also as a bootstrapping solution for your infrastructure. By restricting access to an S3 bucket, you can ensure that only your infrastructure can retrieve the manifest. This approach allows you to use ConfigSet for bootstrapping your infrastructure and managing your installs and application deployments with the cfs client application. A key feature of `cfs` is its ability to run without any OS dependencies, making it suitable for a wide range of environments, including containers and scenarios where you do not have root access.

`cfs`, short for Config File System, is an open-source configuration management tool that facilitates the management, automation, and deployment of infrastructure. Users can describe their infrastructure requirements with simple, easy-to-understand manifest files. These files define the actions, components, and configurations needed for a specific task.

## Goals of ConfigSet.com

ConfigSet.com aims to make infrastructure automation as easy and accessible as possible for users of all skill levels. By providing a broad range of pre-made manifests, users can quickly find and integrate the right solutions for their needs without starting from scratch.

The main objectives of ConfigSet.com include:

1. Providing a centralized platform for users to discover and utilize community-contributed `cfs` manifests.
2. Encouraging community involvement in the development and sharing of `cfs` manifests for various use cases.
3. Streamlining the process of integrating `cfs` manifests into users' existing infrastructure setups.
4. Providing an easy-to-use interface for navigating and searching for `cfs` manifests based on specific requirements.

