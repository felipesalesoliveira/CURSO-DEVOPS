# **REPLICASET**
- quando estamos criando um Deployment no Kubernetes, automaticamente estamos criando um ReplicaSet e esse ReplicaSet é quem vai criar os Pods que estão dentro do Deployment.
&nbsp;
# **DAEMONSET**
- O DaemonSet é um objeto que garante que todos os nós do cluster executem uma réplica de um Pod, ou seja, ele garante que todos os nós do cluster executem uma cópia de um Pod.
&nbsp;
# **PROBES**
- As probes são uma forma de você monitorar o seu Pod e saber se ele está em um estado saudável ou não. Com elas é possível assegurar que seus Pods estão rodando e respondendo de maneira correta, e mais do que isso, que o Kubernetes está testando o que está sendo executado dentro do seu Pod.
    - LIVENESS PROBE (teste de integridade)
    - READNESS PROBE (teste de leitura externa)
    - STARTUP PROBE (teste de inicio)