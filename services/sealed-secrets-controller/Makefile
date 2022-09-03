
export BASE = helm
export CHART = sealed-secrets
export NAMESPACE = kube-system
export REPO = bitnami
export URL = https://charts.bitnami.com/bitnami
export VERSION = 1.1.2

include ../Makefile

cli:
	curl -sSL https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.18.2/kubeseal-0.18.2-$(ARCH)-amd64.tar.gz -o /tmp/kubeseal.tar.gz
	tar zxf /tmp/kubeseal.tar.gz kubeseal
	mv kubeseal /usr/local/bin/kubeseal
_PHONY: cli

seal:
_PHONY: seal
