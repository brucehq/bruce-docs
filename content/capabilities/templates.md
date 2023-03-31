---
title: "Templates"
weight: 1
---
The template files use Golang's text/template package, which provides a rich set of functions and actions to perform various operations on the data. In addition to the built-in functions, ConfigSet provides a custom |dump function to pretty-print the variable contents. Here's an overview of some common template functions and actions:

## Variables
You can access environment variables within your template files using the {{.ENV_KEY}} syntax. For example, {{.ENV_HOME}} will be replaced with the value of the ENV_HOME environment variable. If you set an environment variable using an operator, you can access it with a full name like {{.YOUSETME}}. For variables set via an environment properties file, use the current key name without the ENV_ prefix.

### If-Else
You can use if-else statements to conditionally render content based on the value of a variable.

```go
{{if eq .ENV_OS "linux"}}
  This is Linux.
{{else}}
  This is not Linux.
{{end}}
```

Or
```go
{{ if .ENV_KEY }}
  The value of ENV_KEY is: {{ .ENV_KEY }}
{{ else }}
  ENV_KEY is not set.
{{ end }}
```

### Ranges
You can use the range action to iterate over a list of values. For example, you can use it to iterate over a list of environment variables and print their names and values.

```go
{{ range $key, $value := . }}
  {{ $key }} = {{ $value }}
{{ end }}
```

### Functions
You can use functions to perform various operations on the data. For example, you can use the `printf` function to format a string.

```go
{{ printf "Hello, %s!" .ENV_NAME }}
```

### Dump
The `|dump` function prints the variable contents in a human-readable format. For example, you can use it to print the contents of the `ENV` variable.

```go
{{ .ENV | dump }}
```

### With
The `with` action allows you to set a variable to a value for the duration of the action. For example, you can use it to set the `ENV` variable to the value of the `ENV_HOME` environment variable.

```go
{{ with .ENV_HOME }}
  {{ . | dump }}
{{ end }}
```

### Pipelines
You can use pipelines to chain multiple functions. For example, you can use it to print the value of the `ENV_HOME` environment variable in uppercase.

```go
{{ .ENV_HOME | upper | dump }}
```

### Arithmetic Operations
You can use arithmetic operations to perform calculations on the data. For example, you can use it to calculate the sum of two numbers.  Or divide the physical memory by the amount of processors on the machine to get the amount of memory per processor, to assign to your application via a template.

```go
{{ add 1 2 }}
```

```go
{{ div .ENV_PHYSICAL_MEMORY .ENV_PROCESSORS }}
```

### String Functions
You can use string functions to perform various operations on strings. For example, you can use it to convert a string to uppercase.

```go
{{ upper "hello" }}
```

Or to get the length of a string

```go
{{ len "hello" }}
```

Or to get the substring of a string

```go
{{ substr "hello" 1 3 }}
```

### Date and Time Functions
You can use date and time functions to perform various operations on dates and times. For example, you can use it to get the current date and time.

```go
{{ now }}
```

Or to get the current year.

```go
{{ now | year }}
```

Or to set a time in the future in the template with a variable for use with TTL actions as example.

```go
{{ $future := now.AddDate 0 0 1 }}
```

### Comparison Functions
You can use comparison functions to compare values. For example, you can use it to check if two values are equal.

```go
{{ eq 1 2 }}
```

Or to check if a value is greater than another value.

```go
{{ gt 1 2 }}
```

### Boolean Functions
You can use boolean functions to perform various operations on boolean values. For example, you can use it to check if a value is true.

```go
{{ not true }}
```

or to check if a value is false.

```go
{{ not false }}
```


