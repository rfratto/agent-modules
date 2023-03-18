# rfratto's Grafana Agent modules

This repository contains a set of [modules][] for Grafana Agent. Each directory
is a different Grafana Agent module with a file called `module.river` and a
`README.md` for documentation on how to use the module.

## Recommended module loader

This repository is intended to be used with the work-in-progress `module.git`
module loader. For example, to use [the `k8sapi` module](./k8sapi):

```river
module.git "k8sapi" {
  repository = "https://github.com/rfratto/agent-modules.git"
  revision   = "main"
  path       = "k8sapi/module.river"

  arguments {
    forward_metrics_to = [prometheus.remote_write.default.receiver]
  }
}

prometheus.remote_write "default" {
  ...
}
```

[modules]: https://grafana.com/docs/agent/next/flow/concepts/modules/
