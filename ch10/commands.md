### 10.1 도커 컴포즈로 여러 개의 애플리케이션 배포하기

  * 애플리케이션 세개 실행
    * docker-compose -f ./numbers/docker-compose.yml up -d
    * docker-compose -f ./todo-list/docker-compose.yml up -d
    * docker-compose -f ./todo-list/docker-compose.yml up -d
      * 이미 실행 중인 애플리케이션이 컴포즈 파일에 기술된 내용을 충족하기 때문에 하나 더 실행되지 않음
    * docker-compose -f ./todo-list/docker-compose.yml -p todo-test up -d
      * 프로젝트 이름을 바꿔 애플리케이션을 하나 더 실행
    * docker container port todo-test-todo-web-1 80
      * 포트가 무작위로 개방되기 때문에 이 명령어를 사용해 어떤 포트가 개방됐는지 확인  
  
### 10.2 도커 컴포즈의 오버라이드 파일
  * 도커 컴포즈는 나중에 지정된 파일의 내용이 이전 파일의 내용을 오버라이드 한다.
  * 도커 컴포즈를 사용해 파일을 병합한 결과 출력
    * docker-compose -f ./todo-list/docker-compose.yml -f ./todo-list/docker-compose-v2.yml config  
  
  * 여러 환경으로 애플리케이션 실행하기
    * docker-compose -f ./numbers/docker-compose.yml -f ./numbers/docker-compose-dev.yml -p numbers-dev up -d
      * 개발 환경용 설정으로 실행하기
    * docker-compose -f ./numbers/docker-compose.yml -f ./numbers/docker-compose-test.yml -p numbers-test up -d
      * 개발 환경용 설정으로 실행하기
    * docker-compose -f ./numbers/docker-compose.yml -f ./numbers/docker-compose-uat.yml -p numbers-uat up -d
      * 개발 환경용 설정으로 실행하기
    * 프로젝트 제거 - 프로젝트 이름을 기본값에서 변경하면 종료할 때도 프로젝트 이름을 정확하게 입력해야 함 (docker-compose down 하면 제거 안됨)
      * docker-compose -f ./numbers/docker-compose.yml -f ./numbers/docker-compose-dev.yml -p numbers-dev down
        * 개발 환경용 설정으로 제거하기
      * docker-compose -f ./numbers/docker-compose.yml -f ./numbers/docker-compose-test.yml -p numbers-test down
        * 개발 환경용 설정으로 제거하기
      * docker-compose -f ./numbers/docker-compose.yml -f ./numbers/docker-compose-uat.yml -p numbers-uat down
        * 개발 환경용 설정으로 제거하기  
  
    * 위와 같은 이유로 애플리케이션 배포 및 폐기 스크립트의 작성과 자동화 방법을 익혀 두어야 함.

### 10.3 환경 변수와 비밀값을 이용해 설정 주입하기
  * todo-list-configured 디렉터리에 있는 컴포즈, 오버라이드 파일을 사용해 개발환경으로 설정된 애플리케이션을 실행
    * docker-compose -f ./todo-list-configured/docker-compose.yml -f ./todo-list-configured/docker-compose-dev.yml -p todo-dev up -d
    * curl http://localhost:8089/list
      * 실행된 애플리케이션에 요청 보내기
    * docker container logs --tail 4 todo-dev-todo-web-1
      * 애플리케이션 로그 확인하기