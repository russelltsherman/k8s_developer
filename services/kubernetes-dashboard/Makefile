
export BASE = helm
export CHART = kubernetes-dashboard
export NAMESPACE = kubernetes-dashboard
export REPO = kubernetes-dashboard
export URL = https://kubernetes.github.io/dashboard/
export VERSION = 5.10.0

include ../Makefile

postinstall:
	kubectl apply --filename=$(MODULE)/sa-cluster-admin.yaml

seal:
_PHONY: seal
