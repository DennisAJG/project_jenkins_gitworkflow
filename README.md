# Project Jenkins Gitworkflow com Kubernetes
## Conceitos de Gitworkflow:
https://www.atlassian.com/br/git/tutorials/comparing-workflows/gitflow-workflow

### Comandos linux para configurar o kind pra não ter estouro de arquivos no sistema 
echo fs.inotify.max_user_watches=655360 | sudo tee -a /etc/sysctl.conf
echo fs.inotify.max_user_instances=1280 | sudo tee -a /etc/sysctl.conf 
sudo sysctl -p

### Criando um cluster atraves de um YAML
kind create cluster --config config.yaml
kind delete clusters name_cluster -> usado para deletar clusters

#### Comandos basicos docker:
docker stop $(docker ps -q) -> pausa todos os containers (nodes do kind)
docker start containers_names -> start os containers 
docker network ls -> lista os networks criados
docker inspect container_id -> lista informações de um determinado container
docker network inspect name_network -> consegue ver as informações de uma network especifica 
docker exec -it container_id sh -> acessa um determinado container no terminal 
docker ps --filter "label=name_label=worker" -q -> lista os container com base em filters  (docker ps --filter "label=io.x-k8s.kind.role=worker")
docker exec container_id bash -c ""command" -> executa um comando especifico no container 
docker inspect container_id | jq -r 'name' 

##### Comandos docker automatizados:
1 - comando-docker para executar um determinado comando dentro de varios containers ao mesmo tempo
for container in $(docker ps --filter "label=name_label=worker" -q); do docker exec $container bash -c "command"; done

## Comandos kubectl:
kubectl get pods -A -> lista todos os pods de todas as namespaces em execução(Running)
kubectl get pods -w -> visualiza os pods em execução no terminal interativo 
kubectl apply -f caminho_arquivo_manifest.yaml
kubectl get cm -n kube-system -> comando usado para visualizar todos os ConfgMaps
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.14.8/config/manifests/metallb-native.yaml -> ativa o manifesto para uso do MetalLb
kubectl get ns -> visualiza todas as namespaces
kubectl get services -n ingress-nginx -> visualiza os serviçes do tipo loadbalancer do nginx ingress 
kubectl get ingress -n namespace -> visualiza o ingress de uma namespace
kubectl get ingressclass -> pode visualizar todas as classes de ingress controler 
kubectl get secret -n jenkins jenkins -ojson | jq -r '.data."jenkins-admin-password"' | base64 -d -> acessa o secret do jenkins para coletar a senha de admin 

## Conceitos de charts:
São pacotes onde vão conter manifestos kubernetes. 
Empacotador do Kubernetes (um exe no formato windows)

## Usando o heml para alguns pacotes:
### Nginx ingress controler:
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm search repo nginx
helm repo list

## Usando o helmfile:
O helmfile é um orquestrador de pacotes helms(helmcharts).

## Usando o imagepullsecret-patcher:
É usado quando para um pod usar uma imagem de um registry privado, ele precisa de um secret, só que o secret é por namespace. Então oque ele faz é pegar um secret central e replicar para todas as namespaces

