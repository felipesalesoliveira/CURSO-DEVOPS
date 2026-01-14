# Projeto Kubernetes End to End no EKS (Amazon Kubernetes Service)

**EKS**

## Pré-requisitos

* **kubectl** – Ferramenta de linha de comando para trabalhar com clusters Kubernetes.
  Para mais informações, consulte: *Installing or updating kubectl*.

* **eksctl** – Ferramenta de linha de comando para trabalhar com clusters EKS que automatiza várias tarefas individuais.
  Para mais informações, consulte: *Installing or updating eksctl*.

* **AWS CLI** – Ferramenta de linha de comando para trabalhar com serviços AWS, incluindo o Amazon EKS.
  Para mais informações, consulte: *Installing, updating, and uninstalling the AWS CLI*.
  Após instalar a AWS CLI, recomenda-se configurá-la.
  Veja: *Quick configuration with aws configure*.

---

## ✅ Título do Projeto

**Deploy da Aplicação do Jogo 2048 no Amazon EKS**

## ✅ Descrição do Projeto

Este é um projeto Kubernetes End-to-End (E2E) para realizar o deploy do jogo **2048** no **Amazon Elastic Kubernetes Service (EKS)**.
O projeto envolve a configuração, implantação e gerenciamento da aplicação em um cluster Kubernetes executando na AWS.

O objetivo é demonstrar como:

* Containerizar uma aplicação web
* Implantá-la no EKS
* Gerenciar o cluster Kubernetes
* Expor a aplicação para acesso dos usuários

---

## ✅ Containerização

A aplicação do jogo 2048 foi containerizada utilizando **Docker**.
Esse processo envolveu a criação de um `Dockerfile` para definir o ambiente de execução e as dependências da aplicação, resultando em uma imagem Docker pronta para deploy.

---

## ✅ Configuração do Amazon EKS

Foi configurado um cluster Amazon EKS, ajustando os recursos necessários e as configurações de rede usando serviços da AWS.
Esta etapa incluiu a configuração de autenticação e permissões para interagir com o cluster EKS.

---

## ✅ Deploy da Aplicação

A aplicação containerizada do jogo 2048 foi implantada no cluster EKS usando Kubernetes.
Foram definidos arquivos YAML de **Deployment** e **Service** para garantir o gerenciamento eficiente e a disponibilidade da aplicação.

---

## ✅ Escalabilidade e Gerenciamento

Foram explorados os recursos de escalabilidade do Kubernetes, ajustando o número de réplicas da aplicação conforme a demanda.
Isso garante que o jogo consiga lidar com diferentes volumes de tráfego de usuários.

---

## ✅ Exposição da Aplicação

Para tornar o jogo acessível aos usuários, foi criado um **Service do tipo LoadBalancer** no Kubernetes.
Opcionalmente, poderia ser implementado um **Ingress Controller** para roteamento mais avançado.

---

## Etapa 1: Criar um cluster EKS

---

## Etapa 2: Criar roles IAM

Criar uma role IAM chamada **eks-cluster-role** com **1 policy anexada**:

* `AmazonEKSClusterPolicy`

Criar outra role IAM chamada **eks-node-grp-role** com **3 policies anexadas**
(Permite que instâncias EC2 chamem serviços AWS em seu nome):

* `AmazonEKSWorkerNodePolicy`
* `AmazonEC2ContainerRegistryReadOnly`
* `AmazonEKS_CNI_Policy`

Configurações:

* Escolher a **VPC padrão**
* Escolher **2 ou 3 subnets**
* Escolher um **Security Group** com as portas abertas:

  * 22
  * 80
  * 8080
* **Cluster endpoint access**: Public

> Para VPC CNI, CoreDNS e kube-proxy, utilize as versões padrão.
> Para o CNI, a versão *latest* e *default* são diferentes, mas utilize a *default*.

Clique em **Create**.
O processo leva cerca de **10 a 12 minutos**.
Aguarde até que o cluster apareça como **Active**.

---

## Etapa 3: Adicionar Node Groups ao cluster

Adicionar os **worker nodes**, onde os pods irão rodar.

Caminho:
**Cluster > Compute > Add Node Group**

Configurações:

* Nome: `<seunome>-eks-nodegrp-1`
* Selecionar a role já criada
* Manter os valores padrão

AMI:

* Escolher a padrão (**Amazon Linux 2**)

Capacidade:

* Desired / Minimum / Maximum: **1** (alterar de 2 para 1)

Habilitar acesso SSH:

* Escolher um Security Group que permita:

  * 22
  * 80
  * 8080

Manter os valores padrão para os demais campos.

A criação do Node Group leva cerca de **2 a 3 minutos**.

---

## Etapa 4: Autenticar no cluster

**Referência**:
[https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html)

Abrir o **CloudShell**.

```bash
aws sts get-caller-identity
```

```bash
aws eks update-kubeconfig --region region-code --name my-cluster
```

Exemplo:

```bash
aws eks update-kubeconfig --region us-east-1 --name unus-eks-cluster-1
```

```bash
kubectl get nodes
```

```bash
sudo yum install nano -y
```

---

## Etapa 5: Criar um POD no EKS para o jogo 2048

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: 2048-pod
  labels:
    app: 2048-ws
spec:
  containers:
  - name: 2048-container
    image: blackicebird/2048
    ports:
      - containerPort: 80
```

```bash
kubectl apply -f 2048-pod.yaml
```

```bash
kubectl get pods
```

---

## Etapa 6: Configurar Service com Load Balancer

```yaml
apiVersion: v1
kind: Service
metadata:
  name: mygame-svc
spec:
  selector:
    app: 2048-ws
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: LoadBalancer
```

```bash
kubectl apply -f mygame-svc.yaml
```

```bash
kubectl describe svc mygame-svc
```

```bash
curl <LoadBalancer_Ingress>:<Port_number>
```

Exemplo:

```bash
curl a06aa56b81f5741268daca84dca6b4f8-694631959.us-east-1.elb.amazonaws.com:80
```

> Execute este comando **no seu computador local**, não no CloudShell.

Acesse o **Console EC2**, copie o **DNS do ELB** e cole na barra de endereços do navegador.

O jogo **2048** será exibido e estará jogável 🎮
(Aguarde de **2 a 3 minutos** para que o setup seja concluído.)

