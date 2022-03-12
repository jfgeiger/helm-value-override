# Prerequisite

* The Kubernetes namespace `helm-value-override` does not exist yet.

# Run

```
helm install --namespace helm-value-override --create-namespace \
    helm-value-override helm-value-override \
    -f helm-value-override/values.default.yaml
```

The log of the busybox-Pod shows `1a (coming from values.default.yaml) , 2a (coming from values.default.yaml)`.

```
helm upgrade --namespace helm-value-override \
    helm-value-override helm-value-override \
    -f helm-value-override/values.default.yaml \
    -f helm-value-override/values.override.yaml
```

The log of the busybox-Pod shows `1b (coming from values.override.yaml) , 2a (coming from values.default.yaml)` - the first value gets overridden by `values.override.yaml`.

```
helm upgrade --namespace helm-value-override \
    helm-value-override helm-value-override \
    -f helm-value-override/values.default.yaml \
    -f helm-value-override/values.override.yaml \
    -f helm-value-override/values.default.yaml
```

The log of the busybox-Pod shows `1a (coming from values.default.yaml) , 2a (coming from values.default.yaml)` - the first value gets overridden twice.

# Cleanup

```
helm uninstall --namespace helm-value-override helm-value-override
kubectl delete namespace helm-value-override
```