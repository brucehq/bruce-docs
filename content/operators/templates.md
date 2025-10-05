---
title: "Templates Operator"
weight: 12
---
The Templates operator renders a remote or inline template to a local file, injecting environment variables and optional per-step variables.

## Syntax

```yaml
- template: <LOCAL_DESTINATION_PATH>
  source: <REMOTE_LOCATION_OR_URL>
  vars:
    - type: <value|command>
      input: <INPUT>
      variable: <VARIABLE_NAME>
  onlyIf: <sub-command>
  notIf: <sub-command>
  exitIf: <sub-command>
```
* `template`: Local destination path written by this operator.
* `source`: Remote template source. Supports `file://`, `http(s)://`, and `s3://` URLs.
* `vars`: Optional list of variables to add/override when rendering the template.
* `type`:
  * `value`: Use the literal `input` value (supports OS handler mapping; see below).
  * `command`: Execute `input` as a command and use its stdout.
* `input`: The value or command to evaluate for the variable.
* `variable`: The variable name made available to the template (merged on top of existing environment variables).
* `onlyIf`: [See detailed docs here](/operators/sub-commands)
* `notIf`: [See detailed docs here](/operators/sub-commands)
* `exitIf`: [See detailed docs here](/operators/sub-commands)

Note: Fields `perms`, `owner`, and `group` exist in the configuration model but are not currently applied by the implementation. Files are created with default mode `0664`, and ownership is unchanged.

## Example:

```yaml
- template: /etc/nginx/nginx.conf
  source: https://raw.githubusercontent.com/brucedom/bruce/main/examples/nginx/templates/etc/nginx/nginx.conf
  vars:
  - type: value
    input: nginx|apt=www-data
    variable: NGINX_USER
```
In this example, the Templates operator downloads the Nginx configuration file from the provided URL and saves it to `/etc/nginx/nginx.conf`. It injects the variable `NGINX_USER` using OS handler mapping: `nginx|apt=www-data` means use `nginx` by default, but if the package handler is `apt`, use `www-data`. See `GetValueForOSHandler()` in `bruce/operators/operators.go`.

## Example 2:

```yaml
- template: /etc/nginx/nginx.conf
  source: https://raw.githubusercontent.com/brucedom/bruce/main/examples/nginx/templates/etc/nginx/nginx.conf
  vars:
  - type: value
    input: nginx|apt=www-data
    variable: NGINX_USER
  notIf: ls /etc/systemd/system/nginx.service
```
In the above example, the Templates operator only executes if the /etc/systemd/system/nginx.service file does not exist.

## Example 3:

```yaml
- template: /etc/nginx/nginx.conf
  source: https://raw.githubusercontent.com/brucedom/bruce/main/examples/nginx/templates/etc/nginx/nginx.conf
  vars:
  - type: value
    input: nginx|apt=www-data
    variable: NGINX_USER
  onlyIf: ls /tmp/output.txt
```
In the above example, the Templates operator only executes if the /tmp/output.txt file exists.

## Variable sources and Templating

- Environment variables are always injected into the template render context.
- `vars` entries override or add to those values.
- Two custom template functions are available:
  - `contains substr value`: returns true if `value` contains `substr`.
  - `dump .`: pretty-prints a value for debugging.

## Example 4: Using a command-based variable

```yaml
- template: /etc/example.conf
  source: https://example.com/templates/example.conf.tmpl
  vars:
    - type: command
      input: hostname -f
      variable: HOST_FQDN
```
The `HOST_FQDN` variable will contain the output of `hostname -f`.