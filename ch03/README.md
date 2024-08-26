- 도커 이미지 다운받기
  - docker image pull diamol/ch03-web-ping

- 이미지 실행
  - --name -> web-ping 이라고 이름 지정)
  - docker container run -d --name web-ping diamol/ch03-web-ping

- 로그 확인
  - docker container logs web-ping

- 타겟 변경 (TARGET이라는 환경 변수 -> google.com으로 변경)
  - docker rm -f web-ping
  - docker container run --env TARGET=google.com diamol/ch03-web-ping

- 이미지 빌드
  - docker image build --tag web-ping .

- 이미지 목록 확인
  - docker image ls 'w*'

- 빌드한 이미지 실행
  - docker container run -e TARGET=docker.com -e INTERVAL=5000 web-ping
  - 