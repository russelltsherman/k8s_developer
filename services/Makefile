export K8S_CTX ?= $(shell kubectl config current-context)
export K8S_CTX_CERT ?= $(KEYTDIR)/$(K8S_CTX).pem

.DEFAULT_GOAL := bootstrap

bootstrap: deps kustomization manifest values
_PHONY: bootstrap

## add service repo to helm
deps:
	@if [ "$(BASE)" != "helm" ]; then exit 0; fi
	@if [ "$(BASE)" == "helm" ]; then helm repo add ${REPO} ${URL}; fi
_PHONY: deps

## install application to selected context
deploy:
	-kubectl create ns $(NAMESPACE)
	@while ! kubectl kustomize ./envs/$(K8S_CTX) | kubectl apply -f - --namespace $(NAMESPACE); do echo "Retrying to apply resources"; sleep 30; done
_PHONY: deploy

## delete application from selected context
destroy:
	kubectl kustomize ./envs/$(K8S_CTX) | kubectl delete -f - --namespace $(NAMESPACE)
_PHONY: destroy

## generate manifest for current context
generate:
	kustomize build ./envs/$(K8S_CTX)
_PHONY: generate

## iterate services and call default make target
init:
	@# find . -type d -maxdepth 1 -exec make -C {} \;
	@for f in $(shell ls -d */); do echo "Initializing $$f ..."; make -C $$f; done
_PHONY: init

## generate base kustomization declaration
kustomization:
	@if [ "$(BASE)" != "helm" ]; then echo "apiVersion: kustomize.config.k8s.io/v1beta1 \nkind: Kustomization\nnamespace: $(NAMESPACE) \nresources: \n  - $(BASE) \n" > ./base/kustomization.yaml; fi
	@if [ "$(BASE)" == "helm" ]; then echo "apiVersion: kustomize.config.k8s.io/v1beta1 \nkind: Kustomization\nnamespace: $(NAMESPACE) \nresources: \n  - $(CHART)-$(VERSION).yaml \n" > ./base/kustomization.yaml; fi
_PHONY: kustomization

## fetch/render base manifests
manifest:
	@if [ "$(BASE)" != "helm" ]; then curl -s $(BASE) --output ./base/.base-manifest.yaml; fi
	@if [ "$(BASE)" == "helm" ]; then touch base/overrides.yaml; helm template $(CHART) --include-crds --namespace=$(NAMESPACE) --name-template=$(CHART) --repo $(URL) --values=base/overrides.yaml > ./base/$(CHART)-$(VERSION).yaml; fi
_PHONY: manifest

## search helm repo for chart
search:
	@if [ "$(BASE)" != "helm" ]; then exit 1; fi
	@if [ "$(BASE)" == "helm" ]; then helm search repo $(CHART); fi
_PHONY: search

## download a copy of helm chart
pull:
	@if [ "$(BASE)" != "helm" ]; then exit 0; fi
	@if [ "$(BASE)" == "helm" ]; then helm pull $(REPO)/$(CHART) --untar --untardir .chart --version $(VERSION); fi
_PHONY: pull

## prepare sealed secrets for selected context
secrets:
	@for f in $(shell ls -d */); do echo "Sealing Secrets for $$f ..."; make -C $$f seal; done
_PHONY: secrets

## render a helm chart as a collection of indiviual templates
templates:
	@if [ "$(BASE)" == "helm" ]; then touch base/overrides.yaml; helm template $(CHART) --include-crds --namespace=$(NAMESPACE) --name-template=$(CHART) --output-dir .templates --repo $(URL) --values=base/overrides.yaml; fi
_PHONY: templates

## fetch the default values for a helm chart
values:
	@if [ "$(BASE)" != "helm" ]; then exit 0; fi
	@if [ "$(BASE)" == "helm" ]; then helm inspect values $(REPO)/$(CHART) --version $(VERSION) > base/$(CHART)-$(VERSION)-values.yaml; fi
_PHONY: values
