---
title: "More Details on Operators"
weight: 4
---
This section explains the extended capabilities of operators that are available in bruce, and how to use them.  For instance each of the operators has additional capabilities that can be used to customize the behavior of the operator.  For example loading a template is not just a basic text file that is loaded from a specific location but contains variables that can be replaced with values from the environment or from the command line.  Commands that can iterate and change the output of the text file based on variables etc.  There are also global capabilities / operator commands like the properties file allowing you to pre-set or pre-load a set of variables that can be used in the template files, as well as throughout all of your operators as environment varialbes.  An example of this would setting a key as `SOMEKEY=FOO` and then using it with the copy operator to define which src file to grab.

Example:
```yaml
- copy: s3://somebucket/somefile.{{.SOMEKEY}}.bin
  dest: /usr/bin/somefile
  perm: 0775
```

Templates have a very large amount of capabilities and we'll look at some of the more common ones, including the built in functions which add additional functionality beyond text/template, but please be sure to check the text/template documentation for golang found at: https://golang.org/pkg/text/template/ for more information on the capabilities of the templates.  