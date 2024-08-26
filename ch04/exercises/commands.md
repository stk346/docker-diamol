### ch4.2
  - cd ch04/exercises/image-of-the-day
    - 타겟 디렉터리로 이동  
  <br>
  - docker image build -t image-of-the-day .
    - image-of-the-day 이미지 생성  
  <br>
  - docker network create nat
    - nat 네트워크 생성  
  <br>
  - docker container run --name iotd -d -p 800:80 --network nat image-of-the-day
    - image-of-the-day 이미지를 기반으로 새로운 컨테이너 생성
    - 호스트의 포트 800을 컨테이너의 포트 80에 매핑
    - nat 네트워크에 연결
    - 실행후 http://localhost:800/image접속  
  
  <br>
  
### ch4.3
- cd ch04/exercises/access-log
  - 타겟 디렉터리로 이동  
<br>
- docker image build -t access-log .
  - access-log 이미지 생성  
<br>
- docker container run --name accesslog -d -p 801:80 --network nat access-log
  - http://localhost:801/stats 
<br>

### ch4.3
- cd ch04/exercises/image-gallery  
<br>
- docker image build -t image-gallery .  
<br>
- docker container run -d -p 802:80 --network nat image-gallery
  - 이 api는 ch4.2, 4.3의 API를 사용한다.