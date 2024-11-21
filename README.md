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
