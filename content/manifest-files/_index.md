---
title: "Manifest Files"
weight: 2
---

Manifest files are the core building blocks of cfs. They are used to describe the desired state of your infrastructure and define the actions, components, and configurations required for a specific task. Manifest files are written in a simple, easy-to-understand language that is both human-readable and machine-parseable.

## Structure of a Manifest File

A manifest file is a text file that contains a series of components, each of which represents an action or configuration to be applied to your infrastructure. Components are organized into a logical sequence, and each component is defined by an operator, which dictates its behavior.

The general structure of a manifest file is as follows:

```yaml
operator1:
key1: value1
key2: value2
...
operator2:
key1: value1
key2: value2
```


In this structure, `operator1`, `operator2`, etc., represent the different operators that can be used within a manifest file. Each operator is followed by a set of key-value pairs that define its properties and behavior.

## Available Operators

cfs provides a wide range of operators that cater to various use cases. Some of the most common operators include:

- Tarball: Download and extract a tarball to a specified directory.
- Command: Execute a command on the system.
- Copy: Make a copy of a file or directory.
- Cron: Set up a cron task.
- Github: Download a GitHub release.
- PackageRepo: Set up a package repository, such as apt or yum.
- Packages: Install a package based on the system type.
- Services: Set up a service to start and ensure the application runs with the service.
- Signals: Send a signal to a specific process.
- Templates: Load a template and write it to the local filesystem.

Each operator has its own set of properties and behavior, which will be discussed in detail in the following sections.

In the next section, we will explore each operator in more detail and provide examples of their usage in a cfs manifest file.
