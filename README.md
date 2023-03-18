# rfratto's Grafana Agent Flow modules

This repository contains a set of [modules][] for Grafana Agent Flow. Each
directory is a different Grafana Agent Flow module with a file called
`module.river` and a `README.md` for documentation on how to use the module.

Modules are an upcoming feature in Grafana Agent Flow scheduled for the v0.33
release.

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

To use `module.git`, see
[grafana/agent#3302](https://github.com/grafana/agent/pull/3302).

[modules]: https://grafana.com/docs/agent/next/flow/concepts/modules/
