# How to regenerate various sourcegraph.com tokens

## `SRC_SESSION_COOKIE_KEY`

This can be regenerated by running:

```shell
> openssl rand -hex 16
```

Note: Existing users will be signed out, but they will be able to sign in again without any issues.

## EXECUTOR_FRONTEND_PASSWORD (PRECISE_CODE_INTEL_INTERNAL_PROXY_AUTH_TOKEN)

```shell
> openssl rand -base64 128
```

Needs to be updated in three places:

- https://github.com/sourcegraph/infrastructure/blob/main/code-intel/terraform.tfvars
- https://github.com/sourcegraph/deploy-sourcegraph-dot-com/blob/release/base/frontend/sourcegraph-frontend.Deployment.yaml
- https://github.com/sourcegraph/deploy-sourcegraph-dot-com/blob/release/base/executor-queue/executor-queue.Deployment.yaml

Follow the [instructions](https://github.com/sourcegraph/infrastructure/blob/main/code-intel/README.md) for deploying the
terraform changes. The dot-com k8s changes are deployed as usual.