# Guia de Estudos DevOps – Júnior → Pleno

Este documento foi criado para estudo **linha por linha**.  
Cada tópico contém:
- **O que é**
- **O que estudar**
- **O que saber fazer na prática**

---

## 1. Linux

### 1.1 Navegação e comandos básicos
**O que é:**  
Uso do terminal para interagir com o sistema operacional Linux.

**Estude:**
- `ls`, `cd`, `pwd`
- `cp`, `mv`, `rm`
- `cat`, `less`, `head`, `tail`

**Na prática você deve saber:**
- Navegar entre diretórios
- Criar, mover e apagar arquivos
- Ler arquivos de log

---

### 1.2 Permissões
**O que é:**  
Controle de quem pode ler, escrever ou executar arquivos e diretórios.

**Estude:**
- `chmod`
- `chown`
- Permissões `rwx` (4-2-1)
- Usuário, grupo e outros

**Na prática:**
- Corrigir erros de permissão
- Tornar scripts executáveis

---

### 1.3 Usuários e processos
**O que é:**  
Gerenciamento de usuários e programas em execução no sistema.

**Estude:**
- `useradd`, `groupadd`, `passwd`
- `ps`, `top`, `htop`
- `kill`, `pkill`

**Na prática:**
- Criar usuários e grupos
- Encerrar processos travados

---

## 2. Redes

### 2.1 Conceitos básicos
**O que é:**  
Comunicação entre sistemas e aplicações.

**Estude:**
- IP (IP é o endereço de um computador na rede)
- Porta (Porta é a “porta de entrada” de um serviço dentro de um IP)
- DNS (DNS traduz nomes para IPs)
- HTTP vs HTTPS
    - HTTP (sem segurança)
        - Porta padrão: 80
        - Dados não criptografados
        - Qualquer pessoa no caminho pode ler
    - HTTPS (seguro)
        - Porta padrão: 443
        - Dados criptografados
        - Usa TLS/SSL

**Na prática:**
- Entender por que uma aplicação não responde
- Verificar portas abertas (`lsof`, `netstat`, `ss`)

---

### 2.2 Load Balancer e Firewall
**O que é:**  
Distribuição e controle de tráfego de rede.

**Estude:**
- Load Balancer (distribui o tráfego entre vários servidores)
- Firewall (controla quem pode entrar ou sair da rede)
- Security Groups (é o firewall da AWS no nível da instância)

**Na prática:**
- Liberar portas corretamente
- Entender tráfego interno vs externo

---

## 3. Git

### 3.1 Controle de versão
**O que é:**  
Ferramenta para versionar código e trabalhar em equipe.

**Estude:**
- `git clone`
- `git pull`
- `git push`
- `git branch`
- `git merge`

**Na prática:**
- Criar e usar branches
- Resolver conflitos simples

---

## 4. Docker

### 4.1 Containers
**O que é:**  
Execução de aplicações em ambientes isolados.

**Estude:**
- Container vs VM
- Imagem
- Volume

**Na prática:**
- Rodar containers
- Acessar logs
- Executar comandos dentro do container

---

### 4.2 Dockerfile
**O que é:**  
Arquivo que define como uma imagem Docker é criada.

**Estude:**
- `FROM`
- `RUN`
- `COPY`
- `CMD` / `ENTRYPOINT`

**Na prática:**
- Criar imagem de uma aplicação simples
- Buildar e rodar a imagem

---

## 5. Kubernetes

### 5.1 Conceitos principais
**O que é:**  
Orquestrador de containers.

**Estude:**
- Pod
- Deployment
- Service

**Na prática:**
- Subir uma aplicação no cluster
- Escalar pods

---

### 5.2 Configurações
**O que é:**  
Separação de configuração e código.

**Estude:**
- ConfigMap
- Secret
- Ingress

**Na prática:**
- Expor uma aplicação
- Configurar variáveis de ambiente

---

## 6. Cloud (AWS como exemplo)

### 6.1 Infraestrutura básica
**O que é:**  
Uso de recursos em nuvem.

**Estude:**
- EC2
- S3
- IAM

**Na prática:**
- Criar uma VM
- Configurar acesso e permissões

---

## 7. Infra como Código (Terraform)

### 7.1 Conceitos
**O que é:**  
Provisionamento de infraestrutura usando código.

**Estude:**
- Provider
- Resource
- State

**Na prática:**
- `terraform init`
- `terraform plan`
- `terraform apply`

---

### 7.2 Estrutura
**O que é:**  
Organização e reutilização de código.

**Estude:**
- Variables
- Outputs
- Modules

**Na prática:**
- Criar infraestrutura reutilizável
- Trabalhar com múltiplos ambientes

---

## 8. CI/CD

### 8.1 Pipeline
**O que é:**  
Automação de build, testes e deploy.

**Estude:**
- CI (Continuous Integration)
- CD (Continuous Delivery/Deployment)

**Na prática:**
- Criar pipeline simples (build → deploy)

---

## 9. Observabilidade

### 9.1 Logs e métricas
**O que é:**  
Visibilidade e monitoramento do sistema.

**Estude:**
- Logs
- Métricas
- Alertas

**Na prática:**
- Investigar falhas
- Criar alertas básicos

---

## 10. Segurança

### 10.1 Boas práticas
**O que é:**  
Proteção de sistemas e dados.

**Estude:**
- Least privilege
- Secrets
- Variáveis de ambiente

**Na prática:**
- Não expor senhas
- Usar secrets corretamente

---

## 11. Soft Skills

### 11.1 Comunicação e organização
**O que é:**  
Habilidades comportamentais no dia a dia.

**Estude:**
- Comunicação clara
- Documentação
- Organização

**Na prática:**
- Explicar problemas técnicos
- Criar documentação simples

---
