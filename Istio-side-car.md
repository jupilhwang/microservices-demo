## Istio (An open platform to connect,manage,and secure microservices)
![](img/istio.png)

### Installation
http://github.com/istio/istio/releases 에서 환경에 맞는 istio를 다운로드 한다.
![](img/istio-download.png)

압축을 풀고, bin/istioctl은 환경설정 PATH에 추가한다

### Minikube준비
istio side-car inject를 사용하기 위해서, kubernetes cluster에 Admission Controller를 설정한다
```bash
export Admission_Controller=Initializers,NamespaceLifecycle,LimitRanger,ServiceAccount,DefaultStorageClass,GenericAdmissionWebhook,ResourceQuota
minikube start --extra-config=apiserver.Admission.PluginNames=$(Admission_Controller)
```
