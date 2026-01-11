# Deploy de Aplicação Django na AWS usando ECS e ECR
AWS

Este laboratório demonstra como realizar o deploy de uma aplicação **Django** na AWS utilizando **ECS (Elastic Container Service)** e **ECR (Elastic Container Registry)**.

O processo começa com a criação da **imagem Docker** da aplicação e o envio dessa imagem para o **ECR**. Em seguida, criamos a infraestrutura necessária e realizamos o deploy da aplicação usando o **ECS**. Por fim, validamos se a aplicação está rodando corretamente utilizando o servidor web embutido do Django.

---

## Pré-requisitos

- Conhecimento básico de **Django**
- Conceitos básicos de **Docker**
- Conta ativa na **AWS**
- Criatividade é sempre um diferencial 😃

---

## Django Web Framework

O **Django** é um framework web de alto nível escrito em Python que incentiva o desenvolvimento rápido e um design limpo e pragmático.  
É **gratuito e open source**, possui uma comunidade ativa, excelente documentação e diversas opções de suporte gratuitas e pagas.

O Django utiliza:
- **HTML / CSS / JavaScript** no frontend  
- **Python** no backend  

---

## O que são Docker e Containers?

### Docker

O **Docker** é uma plataforma aberta utilizada para **desenvolver, empacotar, distribuir e executar aplicações**.

Ele virtualiza o sistema operacional da máquina onde está sendo executado e permite que aplicações sejam empacotadas em ambientes isolados chamados **containers**.

Um **container** é uma instância executável de uma imagem Docker.  
Utilizando a **Docker CLI ou API**, é possível:
- Criar
- Iniciar
- Parar
- Mover
- Excluir containers

Containers também podem:
- Se conectar a redes
- Utilizar volumes de armazenamento
- Gerar novas imagens Docker a partir de seu estado atual

---

## O que é o AWS Elastic Container Registry (ECR)?

O **Amazon Elastic Container Registry (ECR)** é um serviço gerenciado de registro de imagens de containers.

Ele permite que os clientes utilizem:
- Docker CLI
- Ou qualquer cliente compatível

para **enviar (push)**, **baixar (pull)** e **gerenciar imagens Docker**.

O ECR oferece:
- Segurança
- Escalabilidade
- Alta disponibilidade

---

## Etapas do ECR

Nesta etapa, criaremos um **repositório no ECR** onde a imagem Docker da aplicação ficará armazenada.

### 1. Criar o Dockerfile

Adicionar o arquivo **Dockerfile** ao projeto Django.  
Ele conterá a sequência de comandos necessária para criar a imagem Docker da aplicação.

---

### 2. Build da Imagem Docker

Criar a imagem Docker com o nome `hello-world-django-app:version-1`:

```bash
docker build -t hello-world-django-app:version-1 .
```

Verificar se a imagem foi criada:

```bash
docker images | grep hello-world-django-app
```

---

### 3. Criar Repositório no AWS ECR

- Acesse o **Console da AWS**
- Procure por **ECR**
- Clique em **Create Repository**
- Escolha a visibilidade:
  - **Private** (controlado por IAM – recomendado)
  - **Public**
- Defina o nome do repositório
- (Opcional) Ative **Scan on Push** para identificar vulnerabilidades

---

### 4. Enviar a Imagem Docker para o ECR

#### a) Autenticar o Docker no ECR

```bash
aws ecr get-login-password --region region | docker login --username AWS --password-stdin aws_account_id.dkr.ecr.region.amazonaws.com
```

---

#### b) Identificar a imagem Docker

```bash
docker images
```

---

#### c) Taguear a imagem

```bash
docker tag IMAGE_ID aws_account_id.dkr.ecr.region.amazonaws.com/hello-world-django-app
```

---

#### d) Enviar a imagem para o ECR

```bash
docker push aws_account_id.dkr.ecr.region.amazonaws.com/hello-world-django-app
```

---

## O que é o AWS Elastic Container Service (ECS)?

O **Amazon ECS** é um serviço altamente escalável e de alta performance para gerenciamento de containers Docker.

Ele permite:
- Execução de aplicações em clusters EC2
- Escalabilidade automática
- Integração com serviços AWS como:
  - Security Groups
  - Elastic Load Balancer
  - EBS
  - IAM Roles
  - CloudWatch

---

## Etapas do ECS

### 1. Criar um Cluster

- Acesse o **Console da AWS**
- Procure por **ECS**
- Clique em **Create Cluster**
- Selecione a região correta

---

### 2. Criar a Instância EC2

Durante a criação do cluster:
- Configure a rede
- Configure CloudWatch Container Insights
- Configure Auto Scaling (opcional)

⚠️ Algumas configurações **não podem ser alteradas** após a criação do cluster.

---

### 3. Criar a Task Definition

- Defina:
  - Imagem do ECR
  - Port mappings
  - Recursos (CPU e memória)
- É possível definir múltiplos containers em uma única task

---

### 4. Criar um Service

O **Service** define como a task será executada:

- Cluster
- Launch type
- Task definition
- Número de instâncias

---

### 5. Executar a Task

- Execute a task dentro do cluster
- Verifique no console EC2 se a instância está rodando

---

## Validação

🎉 **Parabéns!**  
Sua aplicação Django foi implantada com sucesso na AWS utilizando **ECS e ECR**.

Para validar:
- Copie o **Public DNS** da instância EC2
- Acesse pelo navegador
- Verifique se a aplicação Django está rodando corretamente

---

## Considerações para Produção

Em ambientes produtivos, outros fatores devem ser considerados:

- Segurança
- Monitoramento
- Balanceamento de carga
- Planos de recuperação (Disaster Recovery)

Uma alternativa é utilizar o **AWS Elastic Beanstalk** para simplificar o deploy de aplicações Django.

---

## Finalização

Tudo certo? Ainda não confiante?  
👉 Repita o laboratório do zero.

**Happy Learning! 🚀**