.DEFAULT_GOAL := create

# Executa a configuração inicial necessária para o cluster
pre:
	@kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.14.8/config/manifests/metallb-native.yaml
	@kubectl wait --namespace metallb-system \
		--for=condition=ready pod \
		--selector=app=metallb \
		--timeout=90s
	@kubectl apply -f manifests/

helm:
	@helmfile apply

# Cria o cluster Kind com base no arquivo de configuração
create:
	@kind create cluster --config config.yaml

# Combina a criação do cluster e a configuração inicial
up: create pre helm

# Remove o cluster Kind
destroy:
	@kind delete cluster --name kind

passwd:
	@echo "JENKINS-PASSWORD:"
	@kubectl get secret -n jenkins jenkins -ojson | jq -r '.data."jenkins-admin-password"' | base64 -d
	@echo "SONARQUBE:"
	@echo "Dedey@30"