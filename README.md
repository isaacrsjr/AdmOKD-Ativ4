# AdmOKD-Ativ4

Essa atividade, realizada em 3 etapas, utiliza:

- a imagem docker disponível no [repositório docker](https://hub.docker.com/repository/docker/isaacrsjr/adm_okd_ativ2)
- o projeto [Play with Kubernetes](https://labs.play-with-k8s.com/)

## Etapa 1

Para a realização da tarefa foram criados os arquivos *deployment.yml* e *service.yml*.
O *commit* no github, referente a essa atividade é [esse aqui](https://github.com/isaacrsjr/AdmOKD-Ativ4/tree/etapa1#etapa-1).

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
git checkout etapa1

cat deployment.yml              # somente para exibição do conteúdo
kubeclt apply -f deployment.yml

kubectl get pods

cat service.yml                 # somente para exibição do conteúdo
kubeclt apply -f service.yml

kubectl get services
# execução do curl <clusterIP>:80 para exibir o html do container
# a porta 80 foi definida no arquivo service.yml
```

## Etapa 2

Para a realização da tarefa foi criado o arquivo *configmap.yml*. O arquivo *deployment* foi alterado para ler variáveis de ambiente a partir do *configmap* criado.

Essa configuração teve por base [esse link](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/#configure-all-key-value-pairs-in-a-configmap-as-container-environment-variables).

O *commit* no github, referente a essa etapa é [esse aqui](https://github.com/isaacrsjr/AdmOKD-Ativ4/tree/etapa2#etapa-2).

configmap.yml:

```yml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-ativ4-cfgmap
data:
  NAME: univates
```

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
        envFrom:
          - configMapRef:
              name: app-ativ4-cfgmap
```

Comandos Executados no Master (depos de ter feito a etapa 1):

```bash
# obtendo arquivos dos rescursos kubernetes
cd /AdmOKD-Ativ4
git checkout etapa2

cat configmap.yml               # somente para exibição do conteúdo
kubeclt create -f configmap.yml

cat service.yml                 # somente para exibição do conteúdo
kubeclt apply -f service.yml

kubectl get pods

kubectl exec -ti <pod> bash
env | grep NAME
exit
```
