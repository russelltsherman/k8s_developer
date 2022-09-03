
export BASE = helm
export CHART = argo-cd
export MODULE = .
export NAMESPACE = argocd
export REPO = argo
export URL = https://argoproj.github.io/argo-helm
export VERSION = 5.4.1

include ../Makefile

cli:
	curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-$(ARCH)-amd64
	chmod +x /usr/local/bin/argocd
_PHONY: cli

seal:
	@kubectl create secret generic argocd-github-creds \
		--from-literal=password="$(GITHUB_TOKEN)" \
		--from-literal=type=git \
		--from-literal=url="$(GITHUB_REPO_URL)" \
		--from-literal=username="$(GITHUB_USERNAME)" \
		--namespace $(NAMESPACE) --output yaml --dry-run=client | \
		kubeseal --cert="$(K8S_CTX_CERT)" --format=yaml > "envs/$(K8S_CTX)/github-creds.yaml"
_PHONY: seal
