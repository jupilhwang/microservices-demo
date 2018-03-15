## Istio (An open platform to connect,manage,and secure microservices)
![](img/istio.png)

### Installation
http://github.com/istio/istio/releases 에서 환경에 맞는 istio를 다운로드 한다.
![](img/istio-download.png)

압축을 풀고, bin/istioctl은 환경설정 PATH에 추가한다

<!-- ### Minikube 준비
istio를 사용하기 위해서는, CRD, RBAC과 Initializers를 Enable시켜야 한다

- CRD (custom resource definition) : K8s 1.7+
- RBAC (roles, bindins) : K8s 1.8+ / minikube에서는 기본으로 enable되어 있지 않기 때문에 enable시켜줘야 한다

Istio sidecar auto injection : Initializer concept in K8s를 사용한다. Initializer는 Alpha feature로 기본적으로 disable되어 있다.

```sh
minikube start \
  --feature-gates=CustomResourceValidation=true \
  --extra-config=apiserver.authorization-mode=RBAC \
  --extra-config=controller-manager.ClusterSigningCertFile="/var/lib/localkube/certs/ca.crt" \
	--extra-config=controller-manager.ClusterSigningKeyFile="/var/lib/localkube/certs/ca.key" \
	--extra-config=apiserver.Admission.PluginNames=NamespaceLifecycle,LimitRanger,ServiceAccount,PersistentVolumeLabel,DefaultStorageClass,DefaultTolerationSeconds,MutatingAdmissionWebhook,ValidatingAdmissionWebhook,ResourceQuota \
	--kubernetes-version=v1.9.0
``` -->

### Istio 설정
download받은 istio파일의 install/kubernetes/istio.yaml을 적용한다.
```sh
kubectl apply -f install/kubernetes/istio.yaml
```
![](img/istio-create.png)

<!-- 
**istio sidecar auto inject**
```bash
kubectl label namespace <namespace> istio-injection=enabled
``` -->
minikube에서는 LoadBalancer를 지원하지 않기 때문에, istio-ingress는 "pending"상태이다. istio-ingress를 사용하기 위해서 여기서는 "LoadBalancer --> NodePort"로 변경해 준다.
![](img/istio-ingress-loadbalancer.png)

![](img/istio-ingress-nodeport.png)


### Istio Sample Program - bookinfo
```sh
kubectl apply -f <(istioctl kube-inject --debug -f samples/bookinfo/kube/bookinfo.yaml)
```
![](img/istio-sample-bookinfo.png)

minikube에서는 
```sh
export GATEWAY_URL=$(kubectl get po -l istio=ingress -n istio-system -o 'jsonpath={.items[0].status.hostIP}'):$(kubectl get svc istio-ingress -n istio-system -o 'jsonpath={.spec.ports[0].nodePort}')
echo $GATEWAY_URL
curl -o /dev/null -sS -w "%{http_code}" http://192.168.99.100:30881/productpage
```
![](img/istio-sample-bookinfo-curl.png)
or

웹페이지 접속 http://192.168.99.100:30881/productpage 

#### route rule with version
기본으로 review 세가지 버전이 번갈아 가면서 나오나, 아래오 같이 조정한다.

[route-rule-reviews-v3.yaml]
```yaml
apiVersion: config.istio.io/v1alpha2
kind: RouteRule
metadata:
  name: reviews-default
spec:
  destination:
    name: reviews
  precedence: 1
  route:
  - labels:
      version: v3
    weight: 100
```
v3으로 routing rule을 100% 준다.
```sh
istioctl create -f samples/kube/route-rules-reviews-v3.yaml
```
![](img/istio-bookinfo-route-rule-v3.png)

#### route rule with user burr
[route-rule-reviews-burr-v3.yaml]
```yaml
apiversion: config.istio.io/v1alpha2
kind: RouteRule
metadata:
  name: reviews-default
spec:
  destination:
    name: reviews
  match:
    httpHeaders:
      cookie:
        regex: ^(.*?;)?(user=burr)(;.*)?$
  percendence: 2
  route:
  - labels:
      version: v3
```
```sh
istioctl create -f route-rule-reviews-burr-v3.yaml
```

### Sock-shop cart
Sock-shop의 Cart부분을 git clone한다.
```sh
git clone https://github.com/microservices-demo/carts.git
```

#### Build
##### Java
```sh
mvn -DskipTests package
```
##### Docker
```sh
GROUP=weaveworksdemos COMMIT=test ./scripts/build.sh
```
##### Run
```sh
mvn spring-boot:run
```
##### Check
```sh
curl http://localhost:8081/health
```
##### Use
```sh
curl http://localhost:8081
```
##### Push
```sh
GROUP=weaveworksdemos COMMIT=test ./scripts/push.sh
```