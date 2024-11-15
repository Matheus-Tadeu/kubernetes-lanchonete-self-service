# Lanchonete Self-Service - Exemplo de Uso com Kubernetes

Este reposit�rio cont�m um exemplo de aplica��o "Lanchonete Self-Service" rodando em um cluster Kubernetes. Este projeto implementa uma estrutura b�sica para uma aplica��o com backend em um ambiente Kubernetes, utilizando um banco de dados MySQL e uma aplica��o com balanceamento autom�tico.

## Pr�-requisitos

Para testar e executar este projeto, voc� precisar�:
- [Minikube](https://minikube.sigs.k8s.io/docs/start/) instalado para criar um cluster Kubernetes local.

## Configura��o e Execu��o

### 1. Inicializar o Minikube

Primeiro, inicie o Minikube com o comando:

```bash
minikube start
```

### 2. Aplicar Configura��es de Banco de Dados MySQL
Acesse o diret�rio mysql/ e aplique os arquivos de configura��o:

```bash
kubectl apply -f mysql/
```

Isso criar�:

- Um Deployment para o MySQL.
- Um PersistentVolumeClaim para armazenamento persistente.
- Um Secret para as credenciais de banco de dados.
- Um Service para expor o banco de dados dentro do cluster.


### 3. Aplicar Configura��es da Aplica��o Lanchonete
Acesse o diret�rio app/ e aplique os arquivos de configura��o:

```bash
kubectl apply -f app/
```

Isso criar�:

- Um Deployment para a aplica��o "Lanchonete Self-Service".
- Um HorizontalPodAutoscaler para escalar automaticamente os pods com base na carga.
- Um Service para expor a aplica��o dentro do cluster.
- Um Secret para as credenciais de acesso ao banco de dados.

### 4. Aguardar Inicializa��o dos Pods
Verifique o status dos pods para garantir que todos estejam Running:

```bash
kubectl get pods
```
Repita o comando at� que todos os pods estejam em READY 1/1 e STATUS Running.

### 5. Aplicar Configura��es dos Componentes

```bash
kubectl apply -f components/
```

### 6. Acessar a Aplica��o
Ap�s os servi�os estarem prontos, voc� pode acessar a aplica��o atrav�s do Minikube. Use o comando abaixo para abrir a URL da aplica��o:

```bash
minikube service lanchonete-self-service
```
A aplica��o ser� aberta no navegador na URL fornecida pelo comando. Acesse a interface Swagger para testar a API na seguinte URL:

```bash
http://<minikube-ip>:<porta>/tech-challenge-01/swagger-ui/index.html
```
Nota: <minikube-ip> e <porta> ser�o substitu�dos pelo endere�o IP e porta espec�ficos do seu ambiente.

### 7. Acessar o Kubernetes Dashboard (Opcional)
Para monitorar e gerenciar os recursos no cluster Kubernetes, voc� pode acessar o Kubernetes Dashboard:

```bash
minikube dashboard
```

### Notas Adicionais
- Certifique-se de ter o Minikube e kubectl configurados corretamente antes de iniciar.
- Este projeto � um exemplo b�sico e pode ser expandido conforme necess�rio.

### Conclus�o
Agora, voc� pode acessar a aplica��o "Lanchonete Self-Service" em um ambiente Kubernetes local e experimentar o uso de Kubernetes para orquestrar a aplica��o e seus componentes.