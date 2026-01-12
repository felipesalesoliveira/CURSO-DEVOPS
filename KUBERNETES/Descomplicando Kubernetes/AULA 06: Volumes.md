# **VOLUME**
- nada mais são do que um diretório dentro do Pod que pode ser utilizado para armazenar dados.
    - EmpityDir
    - HostPath
    - Persistent Volume (PV)
    - Config Map
&nbsp;
# **STORAGECLASS**
- é um recurso do Kubernetes que define como o armazenamento persistente será criado automaticamente no cluster.
&nbsp;
# **PERSISTENT VOLUME (PV)**
- é um objeto que representa um recurso de armazenamento físico em um cluster Kubernetes.
- é utilizado para fornecer armazenamento durável.
- é o volume persistente disponível no cluster, independente de Pods.
&nbsp;
# **PERSISTENT VOLUME CLAIM (PVC)**
- é uma solicitação de armazenamento feita pelos usuários ou aplicativos no cluster Kubernetes. Ele permite que os usuários solicitem um volume específico, com base em tamanho, tipo de armazenamento e outras características.