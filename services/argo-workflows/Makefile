
export BASE = helm
export CHART = argo-workflows
export NAMESPACE = argo-workflows
export REPO = argo
export URL = https://argoproj.github.io/argo-helm
export VERSION = 0.17.1

include ../Makefile

cli:
	curl -sLO https://github.com/argoproj/argo-workflows/releases/download/v3.3.9/argo-$(ARCH)-amd64.gz
	gunzip argo-darwin-amd64.gz
	chmod +x argo-darwin-amd64
	mv ./argo-darwin-amd64 ~/bin/argo
_PHONY: cli

seal:
_PHONY: seal
