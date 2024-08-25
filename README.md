# docker-textboot
도커 교과서 실습

- 실습 환경 초기화 커맨드
  - docker container rm -f $(docker container ls -aq)
- 내려받은 이미지가 차지한 디크스 용량 회수
  - docker image rm -f $(docker image ls -f reference='diamol/*' -q)
