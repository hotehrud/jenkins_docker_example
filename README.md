### Environment
- Mac
- Docker

#### Dockerfile
- jenkins:lts 이미지 pull
- aws-cli 설치
- npm 설치

#### Dockerfile.nginx
- nginx:1.14 이미지 pull
- nginx 내부 설정 커스텀을 위해 nginx 디렉토리를 컨테이너로 경로로 추가

#### docker-compose.yml
- 위 이미지 2개로 만들어지는 컨테이너를 한번에 제어
- links 를 통해 nginx 에서 jenkins 컨테이너로 프록시 가능

#### jenkins 이미지
```shell script
$ docker build -t mygumi/jenkins .
```

#### nginx 이미지
```shell script
$ docker build -t mygumi/jenkins_nginx . -f Dockerfile.nginx
```

#### 젠킨스 컨테이너 실행
```shell script
$ docker-compose up
```


과정 중에 경험한 이슈
1. localhost vs 0.0.0.0
(https://stackoverflow.com/questions/59179831/docker-app-server-ip-address-127-0-0-1-difference-of-0-0-0-0-ip)

2. nginx 502 error
(https://www.it-swarm.dev/ko/nginx/nginx-%EB%8F%84%EC%BB%A4-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-502-%EC%9E%98%EB%AA%BB%EB%90%9C-%EA%B2%8C%EC%9D%B4%ED%8A%B8%EC%9B%A8%EC%9D%B4-%EC%9D%91%EB%8B%B5/825614927/)

=> 1, 2번에 대한 이슈로 nginx 에서의 대안
upstream 에 app:8080 으로 지정
이 app 은 docker-compose.yml 에서 links 참고

3. Cannot connect to the Docker daemon at unix:///var/run/docker.sock. 
/var/run/docker.sock:/var/run/docker.sock
로컬에 있는 docker 를 사용하기 위함.(https://medium.com/dtevangelist/docker-in-docker-fb54252e3188)


