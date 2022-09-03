
export BASE = helm
export CHART = keycloak
export NAMESPACE = keycloak
export REPO = bitnami
export URL = https://charts.bitnami.com/bitnami
export VERSION = 9.7.3

include ../Makefile

seal:
	@kubectl create secret generic keycloak \
		--from-literal=admin-password="$(POSTGRES_PASSWORD)" \
		--from-literal=password="$(POSTGRES_PASSWORD)" \
		--namespace $(NAMESPACE) --output yaml --dry-run=client | \
		kubeseal --cert="$(K8S_CTX_CERT)" --format=yaml > "envs/$(K8S_CTX)/secret.yaml"
_PHONY: seal
