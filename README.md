# mvp sample front
mvp sample front 서비스입니다.   
아래와 같이 cluster에 배포하십시오.   

# 사전준비
- k8s cluster에 연결된 PC나 VM에 접근하십시오. 
- namespace변수를 만듭니다. 아래 예 참조하여 적절히 변경하세요. 
```
$ export NS=mvp-sample
```
- container image가 저장될 [Docker image registry](https://hub.docker.com)의 Organization변수를 생성합니다. 아래 예 참조하여 적절히 변경하세요. 
```
$ export IMGORG=happykube
```

# git clone   
작업디렉토리를 만들고 git clone합니다.  
```
$ mkdir -p ~/work   
$ cd ~/work   
$ git clone https://github.com/happykube/mvp-sample-front.git
$ cd mvp-sample-front
```

# namespace 생성 & 현재 namespace 변경      
```
$ kubectl create ns ${NS}   
$ kubectl config set-context $(kubectl config current-context) --namespace ${NS}
```

# mvp-sample-front 컨테이너 이미지 만들기
- clone한 디렉토리로 이동 
```
$ cd ~/work/mvp-sample-front 
```
- Build container image 
```
$ docker build -f deploy/Dockerfile -t ${IMGORG}/mvp-sample-front:1.0.0 .
```

- Push image 
```
$ docker login 

$ docker push ${IMGORG}/mvp-sample-front:1.0.0
```

# mvp-sample-front microservice 배포
- deploy/ingress.yaml의 spec.rules.host수정
```
$ cd ~/work/mvp-sample-front/deploy   
$ vi ingress.yaml  

$ kubectl apply -f . 
```

- Pod실행여부 확인
```
$ kubectl get po
```

- Ingress주소로 웹브라우저에서 확인
```
$ kubectl get ing
```
http://{ingress url}/login으로 접근합니다.   
<img src="./img/2021-03-30-13-09-44.png" width=50% height=50%/>

# Next Action
- [mvp-sample-bizlogic](https://github.com/happykube/mvp-sample-bizlogic.git)을 배포하십시오.



