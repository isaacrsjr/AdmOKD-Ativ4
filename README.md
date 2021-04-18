# AdmOKD-Ativ4

Essa atividade, realizada em 3 etapas, utiliza:

- a imagem docker disponível no [repositório docker](https://hub.docker.com/repository/docker/isaacrsjr/adm_okd_ativ2)
- o projeto [Play with Kubernetes](https://labs.play-with-k8s.com/)

## Etapa 1

Para a realização da tarefa foram criados os arquivos *deployment.yml* e *service.yml*.
O *commit* no github, referente a essa atividade é [esse aqui](https://github.com/isaacrsjr/AdmOKD-Ativ4/tree/etapa1).

deployment.yml:

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-ativ4-dep
spec:
  replicas: 2
  selector:
    matchLabels:
      app: app-ativ4
  template:
    metadata:
      labels:
        app: app-ativ4
    spec:
      containers:
      - name: admokd-ativ2-container
        image: isaacrsjr/adm_okd_ativ2:v3
        ports:
          - containerPort: 5000
```

service.yml:

```yml
apiVersion: v1
kind: Service
metadata:
  name: app-ativ4-svc
spec:
  selector:
    app: app-ativ4
  ports:
  - port: 80
    targetPort: 5000
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

kubectl get service
# execução do curl <clusterIP>:80 para exibir o html do container
# a porta 80 foi definida no arquivo service.yml
```
