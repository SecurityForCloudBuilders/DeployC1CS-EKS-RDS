# DeployC1CS-EKS-RDS
Passo a passo de como realizar o deploy o C1CS em EKS com um banco de dados Externo (RDS).

# O que iremos precisar?

* Uma conta no Cloud One (não tem custo por 30 dias) - http://cloudone.trendmicro.com/
* Uma conta na AWS - https://portal.aws.amazon.com/billing/signup
* AWS CLI - https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html
* kubectl - https://kubernetes.io/docs/tasks/tools/install-kubectl/
* eksctl - https://github.com/weaveworks/eksctl
* helm - https://docs.aws.amazon.com/eks/latest/userguide/helm.html
* Docker

# Topologia

# Criando o Cluster EKS

* Efetue login na sua conta AWS utilizando o AWS Config.
* Tenha em mente o nome da sua chave .pem e altere ou crie uma nova, no exemplo abaixo o nome da minha chave é my_key_name.

* Crie um arquivo .yml (meuclustereks.yml) com o conteudo abaixo:

```
kind: ClusterConfig

metadata:
  name: NAME-CLUSTER
  region: us-east-1

nodeGroups:
  - name: ng-1
    instanceType: t2.medium
    desiredCapacity: 3
    ssh: # use existing EC2 key
      publicKeyName: my_key_name
    iam:
      withAddonPolicies:
        imageBuilder: true
        autoScaler: true
        externalDNS: true
        certManager: true
        appMesh: true
        appMeshPreview: true
        ebs: true
        fsx: true
        efs: true
        albIngress: true
        xRay: true
        cloudWatch: true
 ```
Aplique as configurações: eksctl create cluster -f meuclustereks.yml

A criação do cluster pode levar alguns minutos.

# Configurando o RDS

# Instalando o Smart Check com banco Externo






