# 4. implement kustomize for greater customization of helm charts

Date: 2022-09-05

## Status

Accepted

## Context

helm charts are very handy for getting an application up and running very quickly
however the capability to customize a helm chart varies by chart producer.

we find, increasingly, the need to change charts in ways that the chart author did not anticipate.
yet we wish to avoid creating and maintaining forks of official helm charts to suite our purposes.
manually editing charts can be tedius and error prone.

## Decision

Implement [Kustomize](https://kustomize.io) to facilitate easier kustomization of any aspect of a helm chart.

## Consequences

Kustomize allows for editing absolutely anything and everything from a helm release.
