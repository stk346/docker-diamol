- 웹 사이트 호스팅 컨테이너
  - docker container run --detach --publish 8080:80 diamol/ch02-hello-diamol-web 

- 도커 컨테이너 보기
  - docker ps -a

- 도커 컨테이너 접근
  - docker exec -it {container id} /bin/sh
