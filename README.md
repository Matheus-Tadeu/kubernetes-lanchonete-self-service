# Lanchonete Self-Service - Exemplo de Uso com Kubernetes

Este repositório contém um exemplo de aplicação "Lanchonete Self-Service" rodando em um cluster Kubernetes. Este projeto implementa uma estrutura básica para uma aplicação com backend em um ambiente Kubernetes, utilizando um banco de dados MySQL e uma aplicação com balanceamento automático.

## Pré-requisitos

Para testar e executar este projeto, você precisará:
- [Minikube](https://minikube.sigs.k8s.io/docs/start/) instalado para criar um cluster Kubernetes local.

## Configuração e Execução

### 1. Inicializar o Minikube

Primeiro, inicie o Minikube com o comando:

```bash
minikube start
```

### 2. Aplicar Configurações de Banco de Dados MySQL
Acesse o diretório mysql/ e aplique os arquivos de configuração:

```bash
kubectl apply -f mysql/
```

Isso criará:

- Um Deployment para o MySQL.
- Um PersistentVolumeClaim para armazenamento persistente.
- Um Secret para as credenciais de banco de dados.
- Um Service para expor o banco de dados dentro do cluster.


### 3. Aplicar Configurações da Aplicação Lanchonete
Acesse o diretório app/ e aplique os arquivos de configuração:

```bash
kubectl apply -f app/
```

Isso criará:

- Um Deployment para a aplicação "Lanchonete Self-Service".
- Um HorizontalPodAutoscaler para escalar automaticamente os pods com base na carga.
- Um Service para expor a aplicação dentro do cluster.
- Um Secret para as credenciais de acesso ao banco de dados.

### 4. Aguardar Inicialização dos Pods
Verifique o status dos pods para garantir que todos estejam Running:

```bash
kubectl get pods
```
Repita o comando até que todos os pods estejam em READY 1/1 e STATUS Running.

### 5. Aplicar Configurações dos Componentes

```bash
kubectl apply -f components/
```

### 6. Acessar a Aplicação
Após os serviços estarem prontos, você pode acessar a aplicação através do Minikube. Use o comando abaixo para abrir a URL da aplicação:

```bash
minikube service lanchonete-self-service
```
A aplicação será aberta no navegador na URL fornecida pelo comando. Acesse a interface Swagger para testar a API na seguinte URL:

```bash
http://<minikube-ip>:<porta>/tech-challenge-01/swagger-ui/index.html
```
Nota: <minikube-ip> e <porta> serão substituídos pelo endereço IP e porta específicos do seu ambiente.

### 7. Acessar o Kubernetes Dashboard (Opcional)
Para monitorar e gerenciar os recursos no cluster Kubernetes, você pode acessar o Kubernetes Dashboard:

```bash
minikube dashboard
```

### Notas Adicionais
- Certifique-se de ter o Minikube e kubectl configurados corretamente antes de iniciar.
- Este projeto é um exemplo básico e pode ser expandido conforme necessário.

### Conclusão
Agora, você pode acessar a aplicação "Lanchonete Self-Service" em um ambiente Kubernetes local e experimentar o uso de Kubernetes para orquestrar a aplicação e seus componentes.