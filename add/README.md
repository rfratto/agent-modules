# add

The `add` module is an example module which can add two numbers.

> **NOTE**: Do not use `add` in production; it is intended only to demonstrate
> the usage of modules. You should always just use the `+` operator directly.

> **NOTE**: `add` must be used with a module loader which can pass arguments
> to loaded modules, such as `module.git`.

## Usage

```river
module.git "add" {
  repository = "https://github.com/rfratto/agent-modules.git"
  revision   = "main"
  path       = "add/module.river"

  arguments {
    a = NUMBER
    b = NUMBER
  }
}
```

## Module arguments

The following arguments are supported when passing arguments to the module
loader:

| Name | Type | Description | Default | Required
| ---- | ---- | ----------- | ------- | --------
| `a` | `number` | The first number to add. | | yes
| `b` | `number` | The second number to add. | | yes

## Module exports

The following fields are exported by the module:

| Name | Type | Description
| ---- | ---- | -----------
| `sum` | `number` | The sum of the two arguments.

## Example

This example demonstrates how you can add two numbers using a module, and use
the sum as part of the scrape interval for
[the `prometheus.scrape` component][prometheus.scrape].

```river
module.git "add" {
  repository = "https://github.com/rfratto/agent-modules.git"
  revision   = "main"
  path       = "add/module.river"

  arguments {
    a = 45
    b = 15
  }
}

prometheus.scrape "default" {
  targets = []

  scrape_interval = module.git.add.export.sum + "s"
}
```

[prometheus.scrape]: https://grafana.com/docs/agent/latest/flow/reference/components/prometheus.scrape
