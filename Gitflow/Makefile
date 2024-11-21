.DEFAULT_GOAL := create

# Alvo para criar o cluster
create:
	@echo "Criando cluster Kind com configuração do arquivo config.yaml..."
	@kind create cluster --config config.yaml

# Alvo para destruir o cluster
destroy:
	@echo "Excluindo cluster Kind chamado 'kind'..."
	@kind delete cluster