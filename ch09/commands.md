### ch9.1 컨테이너화된 애플리케이션에서 사용되는 모니터링 기술스텍

  * 도커 데몬에 아래 두 값 추가
    * "metrics-addr": "0.0.0.0:9223",
    * "experimental": true
  * 프로메테우스에 현재 컴퓨터의 ip 정보 추가
    * hostIp=$(ifconfig en0 | grep -e 'inet\s' | awk '{print $2}')
    * docker container run -e DOCKER_HOST=$hostIp -d -p 9090:9090 diamol/prometheus:2.13.1  
  
  * 애플리케이션을 실행해 측정값을 제공하는 엔드포인트에 접근
    * docker network create nat
    * docker-compose up -d
    * localhost:8010 (애플리케이션 화면)
    * localhost:8010/metrics (측정값 화면)
    * http://localhost:8011/actuator/prometheus (자바 측정값 확인)  
  
  * docker-compose-scale.yml 파일은 accesslog에 대해서 스케일링을 적용할 수 있게 돼있음. 
    * docker-compose -f docker-compose-scale.yml up -d --scale accesslog=3
    * for i in {1..10}; do curl http://localhost:8010 > /dev/null; done
      * HTTP GET 요청을 열 번 보냄
    * localhost:9090/graph에 접속 후 access_log_total을 실행 -> value로 로드밸런싱이 얼마나 고르게 부하를 분배했는지 확인할 수 있음  
  
  * 그라파나 사용
    * export HOST_IP=$(ifconfig en0 | grep -e 'inet\s' | awk '{print $2}')
      * 로컬 컴퓨터의 IP 주소를 환경 변수로 지정하기
    * docker-compose -f ./docker-compose-with-grafana.yml up -d --scale accesslog=3
      * 그라파나가 포함된 컴포즈 파일 실행
    * for i in {1..20}; do curl http://localhost:8010 > /dev/null; done
      * 측정값에 변화가 생기도록 부하를 약간 가하기
    * localhost:3000 접근