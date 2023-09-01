# rfratto's Grafana Agent Flow modules

This repository contains a set of [modules][] for Grafana Agent Flow. Each
directory is a different Grafana Agent Flow module with a file called
`module.river` and a `README.md` for documentation on how to use the module.

## Recommended module loader

This repository is intended to be used with the work-in-progress `module.git`
module loader. For example, to use [the `k8s_api` module](./k8s_api):

```river
module.git "k8s_api" {
  repository = "https://github.com/rfratto/agent-modules.git"
  revision   = "main"
  path       = "k8s_api/module.river"

  arguments {
    forward_metrics_to = [prometheus.remote_write.default.receiver]
  }
}

prometheus.remote_write "default" {
  ...
}
```

[modules]: https://grafana.com/docs/agent/next/flow/concepts/modules/
