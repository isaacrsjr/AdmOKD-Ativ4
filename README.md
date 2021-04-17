# AdmOKD-Ativ4

Essa atividade, realizada em 3 etapas, utiliza:

- a imagem docker disponível no [repositório docker](https://hub.docker.com/repository/docker/isaacrsjr/adm_okd_ativ2)
- o projeto [Play with Kubernetes](https://labs.play-with-k8s.com/)

## Etapa 1

Para a realização da tarefa foram criados os arquivos *deployment.yml* e *service.yml*.
O *commit* no github, referente a essa atividade é [esse aqui](https://github.com/isaacrsjr/AdmOKD-Ativ4/tree/etapa1).

deployment.yml:

```yml

```

service.yml:

```yml


```

Comandos Executados no Master:

```bash
# obtendo arquivos dos rescursos kubernetes
cd /
git clone https://github.com/isaacrsjr/AdmOKD-Ativ4.git
cd AdmOKD-Ativ4

cat deployment.yml              # somente para exibição do conteúdo
kubeclt apply -f deployment.yml

kubectl get pods

cat service.yml                 # somente para exibição do conteúdo
kubeclt apply -f service.yml

# execução do curl <clusterIP>:<servicePort> para exibir o html do container
#kubectl scale deployment app-ativ4-dep --replicas=3
```
