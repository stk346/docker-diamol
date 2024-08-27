### ch8.1
  * cd exercises/numbers  

  * docker image build -t diamol/ch08-numbers-api:v2 -f ./numbers-api/Dockerfile.v2 .
    * 헬스체크 옵션이 추가된 도커파일로 이미지 빌드
  * docker container run -d -p 8081:80 diamol/ch08-numbers-api:v2
    * 헬스체크 옵션이 추가된 도커 이미지 컨테이너화
  * curl http://localhost:8081/rng
    * 4번 호출
  * docker container ls
    * 일정 시간 후 위 코드 호출하면 unhealthy로 바뀌어져 있음
