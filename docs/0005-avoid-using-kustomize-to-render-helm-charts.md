# 5. avoid using kustomize to render helm charts

Date: 2022-09-05

## Status

Accepted

## Context

Kustomize has the ability to download and render helm charts natively
however, some oddities are produced when using this approach.

1. the manifest created includes resources intended for testing
1. applications in argo-cd can be helm, or kustomize, you must customize argocd to enable support to enable helm within a kustomize application.
1. config duplication is produced to support both kustomize helm chart handling and our make targets.

## Decision

Decouple helm from kustomize.
Use helm to render manifests which destribe our typical installation
Use kustomize to implement changes to the manifest rendered by helm

## Consequences

This will facilitate:
1. DRY configuration values
1. deduplication of chart overrides
1. no need to customize argo-cd to support our applications
