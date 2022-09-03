
export BASE = helm
export CHART = pgadmin4
export NAMESPACE = pgadmin
export REPO = runix
export URL = https://helm.runix.net
export VERSION = 1.11.0

include ../Makefile

seal:
	@kubectl create secret generic pgadmin4 \
		--from-literal=password="$(DEFAULT_PASSWORD)" \
		--from-literal=servers.json="{\"Servers\": {\"firstServer\":{\"Group\":\"Servers\",\"Host\":\"postgresql.postgresql.svc.cluster.local\",\"MaintenanceDB\":\"postgres\",\"Name\":\"Local Kubernetes Server\",\"Port\":5432,\"SSLMode\":\"prefer\",\"Shared\":true,\"Username\":\"postgres\"}}}" \
		--namespace $(NAMESPACE) --output yaml --dry-run=client | \
		kubeseal --cert="$(K8S_CTX_CERT)" --format=yaml > "envs/$(K8S_CTX)/secret.yaml"
_PHONY: seal
