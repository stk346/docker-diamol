### ch5.2
  * docker image tag image-gallery $dockerId/image-gallery:v1
    * 기존 이미지에 새로운 참조 부여
  * docker image ls --filter reference=image-gallery --filter reference='*/image-gallery'
    * 이미지 참조 확인
  * docker image push $dockerId/image-gallery:v1
    * 도커 레지스트리에 이미지 푸쉬
  * echo "https://hub.docker.com/r/$dockerId/image-gallery/tags"
    * 도커 허브에 푸쉬된 정보 확인
  * docker container run -d -p 5000:5000 --restart always diamol/registry
    * 도커 레지스트리 실행
  * echo $'\n127.0.0.1 registry.local' | sudo tee -a /etc/hosts
    * 로컬 컴퓨터에 registry.local 별명 추가
    * 터미널에 ping registry.local 입력 시 응답


  * image-gallery 이미지에 레지스트리 도메인 네임 추가해 이미지 참조를 부여  
    * docker image tag image-gallery registry.local:5000/gallery/ui:v1
    * docker image tag image-of-the-day registry.local:5000/gallery/api:v1
    * docker image tag access-log registry.local:5000/gallery/log:v1
  * docker image push registry.local:5000/gallery/ui:v1
    * 태그를 부여한 이미지를 푸쉬  

  * image-gallery 애플리케이션에 major.minor.patch 형식의 버전 태그를 부여
    * docker image tag image-gallery registry.local:5000/gallery/ui:latest
    * docker image tag image-gallery registry.local:5000/gallery/ui:2
    * docker image tag image-gallery registry.local:5000/gallery/ui:2.1
    * docker image tag image-gallery registry.local:5000/gallery/ui:2.1.106
