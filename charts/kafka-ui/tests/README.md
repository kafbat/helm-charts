# Chart unit tests

These suites use [`helm-unittest`](https://github.com/helm-unittest/helm-unittest)
to render the chart's templates and assert on the resulting manifests. They run
in milliseconds, need no Kubernetes cluster, and catch template regressions
(missing fields, broken conditionals, failed `fail`/`required` guards) before a
change is ever applied.

## Running locally

Install the plugin once:

```bash
helm plugin install https://github.com/helm-unittest/helm-unittest
```

Then run the suites from the repository root:

```bash
helm unittest charts/kafka-ui
```

## Layout

One suite per template, named `<template>_test.yaml`:

| Suite | Template under test | Highlights |
|-------|---------------------|------------|
| `ingress_test.yaml`    | `ingress.yaml`    | API version selection, TLS, ingressClassName, templated host |
| `service_test.yaml`    | `service.yaml`    | type/port, NodePort/LoadBalancer specifics, selector labels |
| `deployment_test.yaml` | `deployment.yaml` | replicas vs. autoscaling, image reference, probes, env wiring |
| `notes_test.yaml`      | `NOTES.txt`       | ClusterIP port-forward fallback |

## Adding tests for a new feature

When you add or change a template, add or update the matching `*_test.yaml`
suite in the same PR. A good suite covers:

1. **Does not render when disabled** — the feature's `enabled: false` path.
2. **Renders correctly when enabled** — kind, apiVersion, name, namespace.
3. **Each configurable knob** — one assertion per value that changes output.
4. **Guards** — every `fail`/`required` is exercised with `failedTemplate`
   so a misconfiguration is a red test, not a red CI render.

### Notes for templates that `include` siblings

`deployment.yaml` builds checksum annotations by `include`-ing `configmap.yaml`,
`configmap_fromValues.yaml` and `secret.yaml`. Those templates must be listed
under `templates:` so the includes resolve, and each test uses a
`documentSelector` with `skipEmptyTemplates: true` to assert against the
Deployment document while ignoring the (often empty) configmap/secret renders.

### Notes for `NOTES.txt`

`NOTES.txt` is plain text, not a manifest, so use the raw assertions
(`matchRegexRaw`, `equalRaw`) which operate on the rendered text directly
instead of a YAML `path`.
