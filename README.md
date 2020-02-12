# mvp sample front
mvp front 서비스입니다.   

아래와 같이 cluster에 배포하십시오.   
### local에 fetch   
kubectl명령으로 배포할 수 있는 terminal에서 git clone합니다.   
$ mkdir ~/work   
$ cd ~/work   
$ git clone https://gitlab.com/jenkins28/mvp-sample-front.git    
$ cd mvp-sample-front

### namespace 생성 & 현재 namespace 변경      

$ kubectl create namespace mvp-sample   
$ kubectl config set-context $(kubectl config current-context) --namespace mvp-sample

### microservice 배포
$ cd ~/work/mvp-sample-front/deploy   
$ vi ingress.yaml   
host정보를 수정합니다.     
ICP에서는 kubectl get nodes -o wide로 proxy node의 ip를 확인한후, 그 ip로 지정   
$ vi config.yaml
  $ kubectl get svc 명령으로 login, product 서비스의 이름과 포트를 확인하여 틀리면 변경     

$ kubectl apply -f . 







