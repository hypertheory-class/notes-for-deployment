# Todo

Upgrade Minikube

```shell
winget upgrade minikube
```

Configure Memory and CPU & Driver

```shell
minikube config set memory 8192
minikube config set cpus 2
minikube config set driver hyperv
```

Verify

```shell
minikube config view
```

Start Minikube

```shell
minikube start
```

Enable Addons

```shell
minikube addons enable ingress
minikube addons enable ingress-dns
```

MkCert - Certificates

```shell
choco install mkcert
```

In a directory (e.g. `c:\dev\certs`):

```shell
mkcert hypertheory-training.com "*.hypertheory-training.com" localhost 127.0.0.1 ::1
 ```

Trust the certs:

```shell
mkcert -install
```

## Kubernetes

Create a namespace for our application

```shell
kubectl create namespace learning-resources
```

Change to that namespace

```shell
kubectl config set-context minikube --namespace=learning-resources
```

Add the certs as a secret in that namespace:

```shell
cd c:\dev\certs

kubectl create secret tls mkcert --key hypertheory-training.com+4-key.pem --cert hypertheory-training.com+4.pem
```

## Ingress DNS

Adding:
```shell
 Add-DnsClientNrptRule -Namespace ".hypertheory-training.com"  -NameServers "$(minikube ip)"
 ```

 Removing:
 > Only do this if you need to remove
 ```shell

 Get-DnsClientNrptRule | Where-Object {$_.Namespace -eq '.hypertheory-training.com'} | Remove-DnsClientNrptRule -Force; 

 ```