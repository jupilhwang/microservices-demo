## Istio (An open platform to connect,manage,and secure microservices)
![](img/istio.png)

### Installation
http://github.com/istio/istio/releases 에서 환경에 맞는 istio를 다운로드 한다.
![](img/istio-download.png)

압축을 풀고, bin/istioctl은 환경설정 PATH에 추가한다

### Minikube 준비
istio를 사용하기 위해서는, CRD, RBAC과 Initializers를 Enable시켜야 한다

- CRD (custom resource definition) : K8s 1.7+
- RBAC (roles, bindins) : K8s 1.8+ / minikube에서는 기본으로 enable되어 있지 않기 때문에 enable시켜줘야 한다

Istio sidecar auto injection : Initializer concept in K8s를 사용한다. Initializer는 Alpha feature로 기본적으로 disable되어 있다.

```bash
minikube start \
  --feature-gates=CustomResourceValidation=true \
  --extra-config=apiserver.authorization-mode=RBAC \
  --extra-config=controller-manager.ClusterSigningCertFile="/var/lib/localkube/certs/ca.crt" \
	--extra-config=controller-manager.ClusterSigningKeyFile="/var/lib/localkube/certs/ca.key" \
	--extra-config=apiserver.Admission.PluginNames=NamespaceLifecycle,LimitRanger,ServiceAccount,PersistentVolumeLabel,DefaultStorageClass,DefaultTolerationSeconds,MutatingAdmissionWebhook,ValidatingAdmissionWebhook,ResourceQuota \
	--kubernetes-version=v1.9.0
```

### Istio 설정
download받은 istio파일의 install/kubernetes/istio.yaml을 적용한다.
```bash
kubectl apply -f install/kubernetes/istio.yaml
```
![](img/istio-create.png)

<!-- 
**istio sidecar auto inject**
```bash
kubectl label namespace <namespace> istio-injection=enabled
``` -->


kubectl apply -f <(~istioctl kube-inject -f samples/sleep/sleep.yaml)
