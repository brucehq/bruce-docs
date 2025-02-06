---
title: "Introduction"
weight: 1
---

# Introduction to bruce

Bruce.tools is a platform designed to simplify just about any type of automation through declarative manifests that can be hosted in many locations. These manifests help users automate their infrastructure setup and 
management 
consistently and reliably. Users can interact with bruce in several ways, including manually creating bruce manifests and using the `bruce` client application to deploy them to their infrastructure. Users can also load manifests directly from the 
BruceDom website or any other http/https location, or retrieve them from S3 buckets.

### BruceDom supports the following options for interacting with manifests:
* **Local Filesystem**: A local file on the system or a file path starting with ./ or / is treated as a local file and loaded from the local disk.
* **Remote URL**: A URL starting with http:// or https:// is treated as a remote URL and loaded from the remote location.
* **S3 Bucket**: A URL starting with s3:// is treated as an S3 bucket and loaded from the remote location.

This flexibility allows you to use BruceDom not only as an installation tool but also as a bootstrapping solution for your infrastructure. By restricting access to an S3 bucket, you can ensure that only your infrastructure can retrieve the manifest. This approach allows you to use BruceDom for bootstrapping your infrastructure and managing your installs and application deployments with the bruce client application. A key feature of `bruce` is its ability to run without any OS dependencies, making it suitable for a wide range of environments, including containers and scenarios where you do not have root access.

`bruce`, short for Config File System, is an open-source configuration management tool that facilitates the management, automation, and deployment of infrastructure. Users can describe their infrastructure requirements with simple, easy-to-understand manifest files. These files define the actions, components, and configurations needed for a specific task.

## Goals of bruce.tools

BruceDom.com aims to make infrastructure automation as easy and accessible as possible for users of all skill levels. By providing a broad range of pre-made manifests, users can quickly find and integrate the right solutions for their needs without starting from scratch.

The main objectives of BruceDom.com include:

1. Providing a centralized platform for users to discover and utilize community-contributed `bruce` manifests.
2. Encouraging community involvement in the development and sharing of `bruce` manifests for various use cases.
3. Streamlining the process of integrating `bruce` manifests into users' existing infrastructure setups.
4. Providing an easy-to-use interface for navigating and searching for `bruce` manifests based on specific requirements.

